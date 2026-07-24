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

# Para quem é este curso

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

# Estrutura do curso

## Módulo 0 — Visão geral

- o problema
- a solução
- arquitetura geral

## Módulo 1 — Hardware e ambiente

- ESP32
- ESP-IDF
- build, flash e monitor

## Módulo 2 — Arquitetura do firmware

- organização do repositório
- separação por componentes
- fluxo do sistema

## Módulo 3 — Estudo componente por componente

- configuração
- telemetria
- diagnósticos
- energia
- watchdog
- persistência
- MQTT modular

## Módulo 4 — Contrato MQTT

- tópicos
- payloads
- comandos
- configuração remota
- QoS

## Módulo 5 — Robustez operacional

- reconnect
- backoff
- store-and-forward
- recuperação de falhas
- comportamento em `low_power`

## Módulo 6 — Supervisor local

- broker MQTT
- backend
- frontend
- monitor MQTT
- operação local

## Módulo 7 — Dashboards e análise

- PostgreSQL
- Grafana
- dashboards de overview, operations, inspection e executive

## Módulo 8 — Evolução para produto

- variantes de firmware
- diferenças entre nós contínuos e de baixo consumo
- decisões de hardware
- expansão para cenários reais

---

# Filosofia do curso

Este curso segue uma ideia simples:

primeiro entender o sistema, depois modificar o sistema.

Ou seja, o foco não é decorar código. O foco é dominar:

- responsabilidades;
- fluxos;
- contratos;
- comportamento esperado;
- limitações e tradeoffs.

Isso torna o aluno capaz de:

- manter o projeto;
- estender o projeto;
- adaptar a arquitetura para outros contextos.

---

# O que existe neste repositório

Este repositório deve concentrar:

- planejamento das aulas;
- material de apoio;
- diagramas;
- laboratórios práticos;
- referências cruzadas para o repositório principal do SentinelNode.

Estrutura sugerida:

```text
SentinelNodeCourse/
├── README.md
├── syllabus/
├── labs/
├── diagrams/
├── slides/
└── references/
```

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
- alterar parâmetros e comportamento com segurança;
- operar a supervisão local;
- interpretar dashboards e sinais de degradação;
- evoluir o projeto com mais autonomia.

---

# Estado atual do curso

Este repositório está em construção.

O foco inicial é organizar:

- o syllabus;
- a trilha didática;
- os laboratórios;
- os materiais visuais.

---

# Próximos passos

- publicar o plano detalhado por módulo;
- criar os primeiros laboratórios;
- desenhar diagramas da arquitetura;
- preparar roteiro de estudo do professor;
- converter a documentação técnica em trilha pedagógica.

---

# Licença e uso

Defina aqui a licença que desejar para o material do curso.

Se o curso vier a ser público, também vale incluir:

- regras de reutilização;
- créditos;
- formato de contribuição.
