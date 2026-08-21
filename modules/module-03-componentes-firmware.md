# Módulo 3 — Componentes fundamentais do firmware

## Natureza da aula

Aula nuclear do curso, centrada na leitura modular do firmware.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- explicar a responsabilidade dos componentes centrais do firmware;
- ler a implementação em C de cada componente em nível intermediário;
- relacionar código e comportamento observado em operação;
- distinguir dependências diretas e indiretas entre módulos.

## Pré-requisitos

- compreensão da arquitetura geral do repositório;
- noções básicas de C e leitura de headers/source files.

## Tópicos de exposição

1. `config_manager`;
2. `telemetry_manager`;
3. `diagnostics_manager`;
4. `power_manager`;
5. `watchdog_manager`;
6. `time_manager`;
7. `i2c_manager`;
8. drivers de sensores;
9. `telemetry_store`.

## Estratégia pedagógica

Cada componente deve ser ensinado em três planos:

1. arquitetura:
   - por que existe;
   - qual problema resolve;
   - com quem conversa.
2. implementação em C:
   - funções públicas;
   - funções internas;
   - structs e enums;
   - relação entre `.h` e `.c`.
3. operação:
   - o que aparece no MQTT;
   - o que aparece no serial;
   - o que se altera na supervisão e no dashboard.

## Demonstração prática sugerida

- abrir um componente em sala, por exemplo `telemetry_manager`;
- mostrar o header e a fonte;
- localizar a função de entrada, a agregação interna e o efeito no payload publicado.

## Exercício sugerido

Escolher um componente e pedir ao estudante que responda:

- qual é sua responsabilidade;
- que dados entram nele;
- que dados saem dele;
- qual sintoma operacional apareceria se ele falhasse.

## Perguntas para discussão

- Todo componente precisa ser completamente independente?
- Qual o limite saudável entre coesão e acoplamento?
- Como distinguir falha funcional de falha de observabilidade?

## Resultado esperado

O estudante deve sair desta aula apto a estudar o firmware de maneira disciplinada, sem se perder em detalhes antes de compreender a responsabilidade de cada módulo.
