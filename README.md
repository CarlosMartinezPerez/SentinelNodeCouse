# SentinelNodeCourse

Curso aberto sobre o SentinelNode: um sistema de telemetria industrial baseado
em ESP32, ESP-IDF, MQTT, supervisor local em contêiner e dashboards para
operação e manutenção.

Este repositório foi pensado para ensinar o SentinelNode de forma progressiva,
didática e prática, do hardware ao dashboard.

---

# O que é o curso

O `SentinelNodeCourse` não é apenas um curso de firmware.

Ele mostra como construir e entender um sistema completo, incluindo:

- firmware modular em ESP-IDF;
- sensores e coleta de dados;
- configuração remota via MQTT;
- robustez operacional;
- modos `continuous` e `low_power`;
- supervisão local com backend, frontend e broker MQTT;
- persistência histórica em PostgreSQL;
- dashboards operacionais e executivos em Grafana.

Em outras palavras:

é um curso sobre arquitetura, operação e evolução de um nó industrial realista.

---

# Público-alvo

Este curso é indicado para:

- estudantes de sistemas embarcados;
- desenvolvedores que usam ESP32;
- profissionais de automação e IoT industrial;
- integradores que queiram montar soluções próprias;
- pessoas que já fizeram projetos simples com sensores e MQTT e querem subir de
  nível.

Pré-requisitos desejáveis:

- noções de C;
- noções básicas de microcontroladores;
- familiaridade básica com Linux e terminal;
- noções básicas de rede e MQTT.

---

# Objetivos formativos

Ao final do curso, o estudante deverá ser capaz de:

- compreender a arquitetura geral do SentinelNode;
- compilar, gravar e monitorar o firmware;
- interpretar os contratos MQTT do sistema;
- distinguir responsabilidades entre firmware, supervisor e dashboards;
- analisar robustez operacional e comportamento em campo;
- propor evoluções arquiteturais com critério técnico.

---

# Filosofia didática

O curso foi concebido com progressão gradual, coerência conceitual e ênfase em
arquitetura, programação em C e operação de um sistema embarcado realista.

A regra pedagógica central é simples:

primeiro compreender por que um componente existe; depois, como ele foi
implementado; por fim, como ele se comporta em operação.

Ao longo do curso, os componentes devem ser estudados sempre pela tríade:

- arquitetura;
- implementação em C;
- comportamento operacional.

---

# Estrutura programática

## Módulo 0 — Introdução e visão sistêmica

- apresentação do curso;
- problema industrial abordado;
- visão geral do SentinelNode.

## Módulo 1 — Hardware e ambiente de desenvolvimento

- ESP32 e ESP-IDF;
- sensores de referência;
- build, flash e monitor.

## Módulo 2 — Arquitetura do repositório e fluxo do sistema

- organização do projeto;
- fluxo de boot, coleta, publicação e supervisão.

## Módulo 3 — Componentes fundamentais do firmware

- configuração;
- telemetria;
- diagnósticos;
- energia;
- watchdog.

## Módulo 4 — Núcleo MQTT e contratos de comunicação

- tópicos;
- payloads;
- políticas de publicação;
- QoS e confirmação.

## Módulo 5 — Robustez operacional

- store-and-forward;
- reconexão;
- recuperação de falhas;
- comportamento degradado.

## Módulo 6 — Supervisor local

- broker;
- backend;
- frontend;
- monitor MQTT.

## Módulo 7 — Persistência histórica e dashboards

- PostgreSQL;
- Grafana;
- leitura operacional e executiva.

## Módulo 8 — Evolução do projeto e produto

- variantes de firmware;
- decisões de hardware;
- linhas futuras de evolução.

---

# Sequência didática recomendada

1. compreender o problema;
2. observar o sistema funcionando;
3. estudar a arquitetura;
4. entender os componentes;
5. dominar os contratos MQTT;
6. estudar robustez;
7. operar supervisor e dashboards;
8. refletir sobre evolução de produto.

---

# O que o aluno vai aprender

Ao longo do curso, o aluno vai entender:

- como o SentinelNode foi estruturado por componentes;
- como separar coleta, política de publicação, transporte e diagnóstico;
- como projetar contratos MQTT limpos e operacionais;
- como lidar com falhas de broker, falhas de sensor e quedas de rede;
- como implementar store-and-forward com RAM e flash;
- como supervisionar nós com uma página web local;
- como persistir dados históricos e montar dashboards úteis;
- como pensar na evolução do projeto para produto real.

---

# Organização pedagógica por componente

O núcleo do curso deve tratar cada componente em três planos simultâneos:

1. sua responsabilidade arquitetural;
2. sua implementação em C;
3. seu efeito prático no sistema em execução.

Exemplos centrais de estudo:

- `config_manager`;
- `telemetry_manager`;
- `diagnostics_manager`;
- `power_manager`;
- `watchdog_manager`;
- `time_manager`;
- `i2c_manager`;
- drivers de sensores;
- núcleo MQTT modular.

---

# O que existe neste repositório

Este repositório concentra:

- estrutura programática;
- módulos do curso;
- laboratórios práticos;
- materiais de apoio;
- referências cruzadas para o repositório principal do SentinelNode.

Estrutura inicial do repositório:

```text
SentinelNodeCourse/
├── README.md
├── modules/
├── labs/
├── diagrams/
├── slides/
└── references/
```

---

# Materiais já disponíveis

## Documentos centrais

- [Estrutura programática](docs/estrutura-programatica.md)
- [Roteiro de estudo do professor](docs/professor-study-guide.md)

## Módulos já estruturados

- [Módulo 0 — Introdução e visão sistêmica](modules/module-00-introducao.md)
- [Módulo 1 — Hardware e ambiente de desenvolvimento](modules/module-01-hardware-ambiente.md)
- [Módulo 2 — Arquitetura do repositório e fluxo do sistema](modules/module-02-arquitetura-repositorio.md)
- [Módulo 3 — Componentes fundamentais do firmware](modules/module-03-componentes-firmware.md)
- [Módulo 4 — Núcleo MQTT e contratos de comunicação](modules/module-04-mqtt-contratos.md)
- [Módulo 5 — Robustez operacional](modules/module-05-robustez-operacional.md)
- [Módulo 6 — Supervisor local](modules/module-06-supervisor-local.md)
- [Módulo 7 — Persistência histórica e dashboards](modules/module-07-dashboards-analise.md)
- [Módulo 8 — Evolução do projeto e produto](modules/module-08-evolucao-produto.md)

## Laboratórios iniciais

- [Laboratório 1 — Build, flash e monitor](labs/lab-01-build-flash-monitor.md)
- [Laboratório 2 — Tópicos MQTT e configuração remota](labs/lab-02-topicos-mqtt-e-configuracao.md)
- [Laboratório 3 — Robustez e falhas controladas](labs/lab-03-robustez-e-falhas-controladas.md)

---

# Relação com o repositório principal

O curso usa como base o projeto principal:

- firmware do nó;
- supervisor local;
- dashboards;
- documentação técnica.

O curso não substitui o repositório principal do SentinelNode.

Ele existe para ensinar o raciocínio por trás da solução.

---

# Resultado esperado para o aluno

Ao final do curso, a pessoa deve ser capaz de:

- compilar, gravar e monitorar um nó;
- entender a arquitetura do firmware;
- ler e discutir a implementação em C dos componentes principais;
- alterar parâmetros e comportamento com segurança;
- operar a supervisão local;
- interpretar dashboards e sinais de degradação;
- evoluir o projeto com mais autonomia.

---

# Estado atual do curso

Este repositório está em construção.

O foco inicial é organizar:

- a estrutura programática;
- os módulos;
- os laboratórios;
- o roteiro de estudo do professor;
- os materiais visuais futuros.

---

# Próximos passos

- transformar módulos em aulas completas;
- desenhar diagramas da arquitetura;
- preparar slides e figuras de apoio;
- expandir os laboratórios;
- consolidar critérios de avaliação.

---

# Licença e uso

Defina aqui a licença que desejar para o material do curso.

Se o curso vier a ser público, também vale incluir:

- regras de reutilização;
- créditos;
- formato de contribuição.
