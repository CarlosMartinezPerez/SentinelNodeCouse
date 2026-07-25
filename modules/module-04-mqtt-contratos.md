# Módulo 4 — Núcleo MQTT e contratos de comunicação

## Objetivo

Compreender a comunicação do sistema por meio de sua arquitetura MQTT, de sua
implementação em C e de seu comportamento operacional.

## Eixos do módulo

### 1. Arquitetura

- papel do núcleo MQTT no SentinelNode;
- separação entre transporte, protocolo, política e entrega;
- responsabilidades de `mqtt_manager`, `node_protocol`, `publish_policy`,
  `telemetry_orchestrator`, `publish_tracker` e módulos correlatos.

### 2. Implementação em C

- organização dos componentes MQTT no repositório;
- callbacks, filas, políticas e controle de publicação;
- tratamento de `config/set`, `config/pending`, `command` e respostas.

### 3. Operação do sistema

- tópicos publicados e recebidos;
- efeito prático de `essential` e `inspection`;
- QoS 0 e QoS 1 em operação;
- confirmação operacional, status efetivo e reconfiguração remota.

## Conteúdo contratual

- tópicos publicados;
- tópicos recebidos;
- `telemetry`, `status`, `health`, `inventory`, `event`;
- `command` e `command/response`;
- `config/set` e `config/pending`.

## Resultados de aprendizagem

- ler e interpretar os payloads principais;
- explicar a arquitetura modular da comunicação MQTT;
- reconfigurar o nó remotamente;
- distinguir contrato, implementação e efeito operacional.
