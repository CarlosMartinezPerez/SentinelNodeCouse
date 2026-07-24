# Planejamento do curso SentinelNode

Data: 2026-07-24

Este documento organiza um curso público sobre o SentinelNode com progressão
didática, técnica e prática.

O objetivo do curso não é apenas mostrar código. É fazer o aluno entender:

- o problema industrial que o nó resolve;
- a arquitetura do firmware;
- a lógica MQTT;
- a supervisão local;
- a persistência histórica;
- o caminho natural até dashboards e operação real.

---

# Público-alvo

O curso serve principalmente para:

- estudantes de sistemas embarcados;
- desenvolvedores ESP32/ESP-IDF;
- integradores IoT industrial;
- profissionais de automação;
- makers avançados que queiram sair de protótipos simples e chegar a um sistema
  mais robusto.

Pré-requisitos recomendados:

- noções de C;
- noções básicas de microcontroladores;
- noções básicas de MQTT;
- alguma familiaridade com Linux e terminal.

---

# Filosofia didática

O curso deve subir em camadas:

1. problema e visão geral;
2. hardware e primeira telemetria;
3. arquitetura por componentes;
4. contratos MQTT;
5. robustez operacional;
6. supervisor local;
7. dashboards e análise;
8. extensões e produto.

A regra pedagógica mais importante:

o aluno deve sempre entender primeiro “por que isso existe” e só depois “como
isso foi implementado”.

---

# Estrutura proposta do curso

## Módulo 0 — Visão geral do projeto

Objetivo:

apresentar o SentinelNode como sistema completo.

Conteúdo:

- o que é o SentinelNode;
- problema que ele resolve;
- diferença entre protótipo IoT e nó robusto;
- visão geral do firmware, supervisor e dashboards;
- modos `continuous` e `low_power`;
- perfis `essential` e `inspection`.

Entrega didática:

- mapa geral da solução;
- explicação da terminologia do projeto.

---

## Módulo 1 — Hardware e ambiente de desenvolvimento

Objetivo:

colocar o aluno em condição de compilar, gravar e monitorar o nó.

Conteúdo:

- ESP32 e ESP-IDF 6.0.1;
- estrutura do projeto;
- componentes de hardware atuais:
  - ESP32;
  - BMP280;
  - MPU6500;
  - medição de bateria;
- toolchain;
- `idf.py build`, `flash`, `monitor`;
- monitor MQTT local.

Prática:

- fazer build;
- gravar firmware;
- observar primeira telemetria.

---

## Módulo 2 — Primeira leitura arquitetural

Objetivo:

tirar o aluno da visão “arquivo solto” e colocá-lo na visão “sistema modular”.

Conteúdo:

- como o projeto está dividido em `components/`;
- papel do `main/`;
- fluxo geral:
  - boot;
  - configuração;
  - sensores;
  - rede;
  - MQTT;
  - telemetria;
  - supervisão.

Prática:

- caminhar pelo repositório;
- localizar os componentes principais;
- identificar a separação entre coleta, política, transporte e diagnóstico.

---

## Módulo 3 — Curso componente por componente

Este é o coração do curso.

Cada aula explica:

- responsabilidade do componente;
- entradas;
- saídas;
- acoplamentos;
- decisões de projeto;
- pontos de evolução.

### 3.1 `config_manager`

- persistência de configuração;
- campos de configuração operacional;
- leitura, escrita e defaults;
- relação com NVS.

### 3.2 `telemetry_manager`

- coleta de dados;
- composição da telemetria;
- diferenças entre sensores presentes e ausentes;
- telemetria essencial.

### 3.3 `diagnostics_manager`

- saúde do sistema;
- contadores;
- boot, reset, memória, rede e sensores;
- papel no diagnóstico remoto.

### 3.4 `power_manager`

- `continuous` vs `low_power`;
- cadência real;
- deep sleep;
- implicações operacionais.

### 3.5 `watchdog_manager`

- por que watchdog existe;
- timeout;
- o que significa supervisionar laços críticos;
- cuidados para não gerar resets falsos.

### 3.6 `time_manager`

- SNTP;
- por que não publicar sem horário válido;
- efeito sobre `timestamp_iso`.

### 3.7 `i2c_manager`

- barramento;
- recuperação lógica/elétrica;
- papel na robustez.

### 3.8 Drivers de sensores

- `bmp280`
- `mpu6500`
- `battery`

Pontos:

- inicialização;
- leitura;
- validade;
- falhas típicas;
- comportamento sem sensor.

### 3.9 `telemetry_store`

- store-and-forward;
- RAM + flash;
- persistência;
- backlog;
- política de retenção.

### 3.10 Núcleo MQTT modular

Explicar o conjunto, não só um arquivo:

- `mqtt_manager`
- `node_protocol`
- `publish_policy`
- `telemetry_orchestrator`
- `publish_tracker`
- `telemetry_delivery`
- `outbox_publisher`
- `mqtt_ingress`
- `mqtt_lifecycle`

Aqui o aluno aprende:

- por que a lógica foi desacoplada;
- como o contrato MQTT entra;
- como se decide o que publicar;
- como funciona QoS, confirmação e entrega;
- como entram comandos e configurações.

---

## Módulo 4 — Contrato MQTT do SentinelNode

Objetivo:

ensinar o sistema pela interface de mensagens.

Conteúdo:

- tópicos publicados pelo nó;
- tópicos recebidos;
- payloads;
- `telemetry`, `status`, `health`, `inventory`, `event`;
- `command` e `command/response`;
- `config/set` e `config/pending`;
- `essential` vs `inspection`;
- QoS 0 vs QoS 1.

Prática:

- publicar comandos;
- reconfigurar intervalo;
- alternar perfis;
- alternar modos de operação.

---

## Módulo 5 — Robustez operacional

Objetivo:

mostrar por que o SentinelNode é mais do que um exemplo de MQTT com sensor.

Conteúdo:

- watchdog;
- backoff de reconexão;
- store-and-forward;
- persistência em flash;
- recuperação de I²C;
- confirmação MQTT;
- comportamento com broker fora;
- comportamento com sensor falhando;
- comportamento em `low_power`.

Prática:

- desligar broker;
- observar reconnect;
- simular falha de sensor;
- observar backlog e recuperação.

---

## Módulo 6 — Supervisor local

Objetivo:

apresentar a camada de operação e manutenção.

Conteúdo:

- broker MQTT em contêiner;
- backend FastAPI;
- frontend web;
- monitor MQTT;
- launcher local;
- PostgreSQL.

Prática:

- subir stack;
- abrir página;
- emitir comandos;
- reconfigurar nó;
- observar persistência histórica.

---

## Módulo 7 — Dashboards e análise operacional

Objetivo:

mostrar a transição de supervisão local para leitura histórica e executiva.

Conteúdo:

- Grafana provisionado;
- dashboards:
  - Overview;
  - Operations;
  - Inspection;
  - Executive;
- critérios operacionais;
- disponibilidade estimada;
- criticidade;
- agrupamento por área e máquina;
- correlação entre evento e telemetria.

Prática:

- ler comportamento da frota;
- comparar nós;
- interpretar sintomas de energia, rede e sensor.

---

## Módulo 8 — Evolução do produto

Objetivo:

preparar o aluno para pensar como arquiteto, não só como repetidor do curso.

Conteúdo:

- quando separar firmwares por linha de produto;
- nós contínuos vs nós de baixo consumo;
- alimentação por bateria, solar ou fonte fixa;
- quando simplificar hardware;
- custo por nó;
- uso de ESP32 clássico vs ESP32-C3;
- limites da arquitetura atual;
- o que fica no nó, no supervisor e no dashboard.

---

# Sequência recomendada de aulas

## Bloco 1 — Base

1. visão geral
2. hardware e ambiente
3. build, flash e monitor
4. leitura da primeira telemetria

## Bloco 2 — Arquitetura

5. organização do repositório
6. configuração e boot
7. sensores e coleta
8. diagnóstico
9. energia e modos de operação

## Bloco 3 — Comunicação

10. MQTT e tópicos
11. política de publicação
12. comandos e reconfiguração
13. QoS e confirmação

## Bloco 4 — Robustez

14. store-and-forward
15. watchdog
16. reconexão e backoff
17. falhas de sensor e recovery

## Bloco 5 — Operação

18. supervisor local
19. página de supervisão
20. persistência em PostgreSQL
21. dashboards Grafana

## Bloco 6 — Produto

22. análise de arquitetura
23. variantes futuras
24. boas práticas para instalação real

---

# Estratégia para você como professor

Você não precisa decorar cada linha do firmware.

Você precisa dominar:

- a responsabilidade de cada componente;
- o fluxo do sistema;
- os contratos MQTT;
- o comportamento operacional esperado;
- os limites e tradeoffs da arquitetura.

Ou seja:

o domínio conceitual vem antes do domínio textual do código.

---

# Materiais recomendados para o repositório do curso

O repositório `SentinelNodeCourse` pode nascer assim:

```text
SentinelNodeCourse/
├── README.md
├── syllabus/
│   ├── module-00-overview.md
│   ├── module-01-environment.md
│   ├── module-02-architecture.md
│   ├── module-03-components.md
│   ├── module-04-mqtt.md
│   ├── module-05-robustness.md
│   ├── module-06-supervisor.md
│   ├── module-07-dashboards.md
│   └── module-08-product-evolution.md
├── slides/
├── labs/
├── diagrams/
└── references/
```

---

# Próximo passo natural

Depois deste planejamento, os próximos artefatos ideais são:

1. README público do curso;
2. syllabus por módulo;
3. sequência de laboratórios;
4. lista de diagramas que precisam ser desenhados;
5. roteiro específico para você estudar antes de gravar ou ministrar.
