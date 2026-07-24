# Estrutura programática — SentinelNodeCourse

Data: 2026-07-24

Este documento apresenta a estrutura programática do curso SentinelNode.

O curso foi concebido com progressão gradual, coerência conceitual e ênfase em
arquitetura, operação e análise de um sistema embarcado realista.

## Objetivos gerais

Ao final do curso, o estudante deverá ser capaz de:

- compreender a arquitetura geral do SentinelNode;
- compilar, gravar e monitorar o firmware;
- interpretar os contratos MQTT do sistema;
- distinguir responsabilidades entre firmware, supervisor e dashboards;
- analisar robustez operacional e comportamento em campo;
- propor evoluções arquiteturais com critério técnico.

## Organização dos módulos

### Módulo 0 — Introdução e visão sistêmica

- apresentação do curso;
- problema industrial abordado;
- visão geral do SentinelNode.

### Módulo 1 — Hardware e ambiente de desenvolvimento

- ESP32 e ESP-IDF;
- sensores de referência;
- build, flash e monitor.

### Módulo 2 — Arquitetura do repositório e fluxo do sistema

- organização do projeto;
- fluxo de boot, coleta, publicação e supervisão.

### Módulo 3 — Componentes fundamentais do firmware

- configuração;
- telemetria;
- diagnósticos;
- energia;
- watchdog.

### Módulo 4 — Núcleo MQTT e contratos de comunicação

- tópicos;
- payloads;
- políticas de publicação;
- QoS e confirmação.

### Módulo 5 — Robustez operacional

- store-and-forward;
- reconexão;
- recuperação de falhas;
- comportamento degradado.

### Módulo 6 — Supervisor local

- broker;
- backend;
- frontend;
- monitor MQTT.

### Módulo 7 — Persistência histórica e dashboards

- PostgreSQL;
- Grafana;
- leitura operacional e executiva.

### Módulo 8 — Evolução do projeto e produto

- variantes de firmware;
- decisões de hardware;
- linhas futuras de evolução.

## Sequência didática recomendada

1. compreender o problema;
2. observar o sistema funcionando;
3. estudar a arquitetura;
4. entender os componentes;
5. dominar os contratos MQTT;
6. estudar robustez;
7. operar supervisor e dashboards;
8. refletir sobre evolução de produto.

## Avaliação formativa sugerida

- exercícios de leitura arquitetural;
- laboratórios práticos com firmware e MQTT;
- interpretação de dashboards;
- discussão crítica de tradeoffs;
- projeto final curto de extensão ou adaptação.
