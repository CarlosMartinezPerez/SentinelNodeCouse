# Módulo 3 — Componentes fundamentais do firmware

## Objetivo

Estudar os componentes fundamentais do firmware por uma tríade constante:
responsabilidade arquitetural, implementação em C e comportamento operacional.

## Componentes centrais do módulo

- `config_manager`;
- `telemetry_manager`;
- `diagnostics_manager`;
- `power_manager`;
- `watchdog_manager`;
- `time_manager`;
- `i2c_manager`;
- drivers de sensores.

## Eixos do módulo

### 1. Arquitetura

Para cada componente, estudar:

- por que ele existe;
- qual problema resolve;
- de quem recebe dados;
- para quem entrega dados;
- qual é sua fronteira de responsabilidade.

### 2. Implementação em C

Para cada componente, estudar:

- headers e fontes principais;
- funções públicas e funções internas;
- structs, enums e convenções locais;
- relação entre API do componente e seu uso pelos demais módulos.

### 3. Operação do sistema

Para cada componente, estudar:

- o que ele produz ou controla em tempo de execução;
- como seu efeito aparece no monitor serial, no MQTT ou na supervisão;
- quais sintomas aparecem quando ele falha ou degrada.

## Método recomendado de aula

Cada aula de componente deve responder quatro perguntas:

1. qual é sua responsabilidade no sistema?
2. como isso foi implementado em C?
3. como isso aparece em operação real?
4. como ele se relaciona com os demais componentes?

## Resultados de aprendizagem

- explicar a função de cada componente;
- ler e comentar a implementação em C com segurança;
- relacionar código e comportamento observado;
- compreender por que a modularização favorece manutenção e evolução.
