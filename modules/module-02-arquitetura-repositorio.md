# Módulo 2 — Arquitetura do repositório e fluxo do sistema

## Objetivo

Levar o estudante da leitura superficial de pastas para a compreensão do fluxo
arquitetural do sistema e preparar o terreno para o estudo posterior dos
componentes em código C e em operação.

## Eixos do módulo

### 1. Arquitetura

- organização em `components/`, `main/`, `docs/`, `supervisor/` e `tools/`;
- fronteiras entre firmware, supervisor e dashboards;
- fluxo de boot, coleta, publicação e supervisão.

### 2. Implementação em C

- convenções de organização dos componentes;
- headers, fontes e responsabilidades locais;
- como localizar funções de inicialização, leitura, publicação e diagnóstico.

### 3. Operação do sistema

- caminho da telemetria do sensor ao MQTT;
- caminho do MQTT ao supervisor e ao Grafana;
- pontos de observabilidade do sistema em execução.

## Resultados de aprendizagem

- localizar responsabilidades no repositório;
- explicar o caminho da telemetria do sensor ao dashboard;
- distinguir módulos centrais e módulos auxiliares;
- preparar-se para estudar cada componente em três planos: arquitetura, código
  e operação.
