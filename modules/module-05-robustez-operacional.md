# Módulo 5 — Robustez operacional

## Objetivo

Estudar os mecanismos que permitem ao SentinelNode operar de forma resiliente,
relacionando arquitetura, implementação em C e comportamento em campo.

## Eixos do módulo

### 1. Arquitetura

- por que robustez não deve ficar concentrada em um único arquivo;
- papel de watchdog, store-and-forward, backoff e recovery;
- relação entre robustez local e observabilidade remota.

### 2. Implementação em C

- organização da persistência híbrida RAM + flash;
- lógica de reconexão e retentativa;
- supervisão por watchdog;
- recuperação de I²C e tratamento de falha de sensor.

### 3. Operação do sistema

- comportamento com broker indisponível;
- comportamento com falha de sensor;
- backlog, reconexão e recuperação;
- interpretação de sinais de degradação no MQTT e nos dashboards.

## Resultados de aprendizagem

- justificar a presença dos mecanismos de robustez;
- analisar cenários degradados com base no código e nos sintomas observados;
- relacionar implementação e recuperação operacional.
