# Laboratório 3 — Robustez e falhas controladas

## Objetivo

Observar o comportamento do sistema sob degradação controlada.

## Atividades

1. desligar temporariamente o broker MQTT;
2. observar reconnect e backlog;
3. religar o broker;
4. simular ausência de sensor ou leitura inválida;
5. analisar sinais em `health`, `event` e dashboards.

## Questões de reflexão

- Como o sistema se comporta sem broker?
- Como a persistência ajuda a preservar dados?
- Como distinguir falha de rede de falha de sensor?
