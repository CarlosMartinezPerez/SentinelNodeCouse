# Módulo 7 — Persistência histórica e dashboards

## Natureza da aula

Aula sobre a passagem da telemetria instantânea para dados persistidos, indicadores derivados e leitura histórica da frota.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- distinguir página de supervisão de dashboard histórico;
- explicar o papel do PostgreSQL e do Grafana;
- identificar dado bruto, dado persistido e métrica derivada;
- interpretar os dashboards do SentinelNode com cautela operacional.

## Pré-requisitos

- domínio dos tópicos principais MQTT;
- familiaridade elementar com tabelas e séries temporais.

## Tópicos de exposição

1. fluxo MQTT → persistência → consulta → painel;
2. origem dos dados: telemetria, status, inventário e eventos;
3. dashboards Overview, Operations, Inspection e Executive;
4. metadados de nó, criticidade, saúde e disponibilidade estimada;
5. limites das métricas derivadas e importância de contexto de instalação;
6. diferença entre uma tendência observada e um diagnóstico confirmado.

## Demonstração prática sugerida

- abrir os dashboards provisionados pelo Grafana;
- filtrar por nó e comparar node33 e node18;
- relacionar uma série de bateria, RSSI ou temperatura ao payload MQTT de origem;
- consultar a API de análise da frota e interpretar seus campos.

## Exercício sugerido

Entregar uma captura de dashboard e pedir que o estudante separe em três grupos:

- informações medidas diretamente pelo nó;
- informações persistidas sem cálculo adicional;
- informações inferidas pelo supervisor.

## Perguntas para discussão

- Uma estimativa de disponibilidade baseada em amostras equivale a uma medição direta de disponibilidade?
- Por que uma tendência de bateria pode ser útil sem ser uma previsão confiável de autonomia?
- Que metadados de instalação tornam um dashboard mais útil em uma fábrica real?

## Resultado esperado

O estudante deve ser capaz de ler o dashboard como instrumento de apoio à operação, reconhecendo tanto sua utilidade quanto seus limites inferenciais.
