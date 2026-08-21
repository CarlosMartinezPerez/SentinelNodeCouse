# Módulo 4 — Núcleo MQTT e contratos de comunicação

## Natureza da aula

Aula sobre a interface de comunicação do sistema e sobre a modularização da lógica MQTT.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- identificar os tópicos MQTT do SentinelNode;
- explicar o contrato de cada tópico principal;
- compreender a diferença entre transporte, protocolo, política e confirmação;
- reconfigurar o nó por MQTT com segurança conceitual.

## Pré-requisitos

- noções básicas de MQTT;
- compreensão prévia da arquitetura do firmware.

## Tópicos de exposição

1. prefixo `sentinelnode/<node>/`;
2. tópicos publicados;
3. tópicos recebidos;
4. `essential` versus `inspection`;
5. QoS 0 e QoS 1;
6. `config/set` versus `config/pending`;
7. confirmação operacional por `status` e por comportamento temporal de `telemetry`.

## Demonstração prática sugerida

- observar `telemetry`, `status`, `health`, `inventory` e `event` no monitor MQTT;
- enviar `status` e `ping` por `command`;
- alterar parâmetros via `config/set`;
- observar a resposta do sistema.

## Comandos úteis

```bash
mosquitto_sub -h 127.0.0.1 -v -t 'sentinelnode/#'
mosquitto_pub -h 127.0.0.1 -t 'sentinelnode/node33/command' -m '{"cmd":"status"}'
mosquitto_pub -h 127.0.0.1 -t 'sentinelnode/node33/config/set' -m '{"telemetry_interval_seconds":10}'
mosquitto_pub -h 127.0.0.1 -t 'sentinelnode/node33/config/set' -m '{"publish_profile":"inspection"}'
```

## Exercício sugerido

Pedir ao estudante que:

1. liste os tópicos principais do sistema;
2. identifique a finalidade operacional de cada um;
3. explique por que `inspection` não deve ser o estado normal de toda a frota.

## Perguntas para discussão

- Por que o contrato MQTT precisa ser tratado como parte da arquitetura?
- O que acontece quando `status` e `telemetry` confirmam aspectos diferentes da configuração?
- Por que separar `config/pending` faz diferença em `low_power`?

## Resultado esperado

O estudante deve sair desta aula capaz de usar MQTT como lente arquitetural do SentinelNode, e não apenas como ferramenta de publish/subscribe.
