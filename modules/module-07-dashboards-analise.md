# Módulo 7 — Persistência histórica e dashboards

## Objetivo

Explicar como dados operacionais se transformam em análise histórica e apoio à
manutenção, distinguindo origem do dado, cálculo derivado e leitura
operacional.

## Eixos do módulo

### 1. Arquitetura

- papel do PostgreSQL e do Grafana;
- diferença entre página de supervisão e dashboards históricos;
- camada de análise derivada no supervisor.

### 2. Implementação

- organização das consultas SQL;
- provisionamento de dashboards;
- uso de metadados, criticidade e disponibilidade estimada.

### 3. Operação do sistema

- leitura dos dashboards Overview, Operations, Inspection e Executive;
- interpretação de criticidade, correlação e disponibilidade;
- distinção entre dado bruto, dado persistido e métrica derivada.

## Resultados de aprendizagem

- interpretar a leitura histórica da frota;
- distinguir dado bruto de métrica derivada;
- explicar o que vem do firmware e o que é calculado no supervisor;
- usar dashboards para manutenção e tomada de decisão.
