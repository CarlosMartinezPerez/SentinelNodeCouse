# Roteiro de estudo do professor — SentinelNodeCourse

Data: 2026-07-24

Este roteiro foi pensado para apoiar o professor na preparação de um curso
acadêmico sobre o SentinelNode.

O objetivo não é decorar o firmware linha por linha. O objetivo é construir
domínio conceitual, arquitetural e operacional suficiente para:

- explicar o sistema com segurança;
- responder perguntas técnicas com coerência;
- contextualizar decisões de projeto;
- conduzir alunos do básico ao avançado.

---

# 1. Objetivo pedagógico do professor

Ao ministrar este curso, o professor deve ser capaz de:

- apresentar o SentinelNode como sistema embarcado completo;
- explicar a divisão de responsabilidades entre nó, supervisor e dashboard;
- justificar escolhas de arquitetura;
- demonstrar o fluxo ponta a ponta da telemetria;
- explicar robustez, diagnóstico e operação;
- situar limites atuais e caminhos futuros do projeto.

O foco docente deve recair menos sobre “comandos decorados” e mais sobre:

- princípios;
- contratos;
- responsabilidades;
- tradeoffs;
- critérios de projeto.

---

# 2. O que dominar antes de ensinar

## 2.1 Camada conceitual

O professor deve saber explicar:

- qual problema o SentinelNode resolve;
- por que ele não é apenas “um ESP32 com sensores”;
- a diferença entre telemetria, diagnóstico, supervisão e análise histórica;
- a diferença entre dado bruto, interpretação operacional e decisão de processo.

## 2.2 Camada arquitetural

O professor deve saber explicar:

- a estrutura do repositório;
- a organização por componentes;
- a separação entre firmware, supervisor e dashboards;
- o desacoplamento da lógica MQTT em módulos especializados;
- a relação entre coleta, política de publicação, persistência e diagnóstico.

## 2.3 Camada operacional

O professor deve saber demonstrar:

- build;
- flash;
- monitor serial;
- monitor MQTT;
- reconfiguração por MQTT;
- uso da página de supervisão;
- leitura básica dos dashboards Grafana.

---

# 3. Sequência recomendada de estudo do professor

## Etapa A — Visão geral

Ler e consolidar:

- `README.md`
- `docs/architecture.md`
- `docs/runtime-behavior.md`

Perguntas que o professor deve conseguir responder:

- O que é o SentinelNode?
- Quais são seus modos de operação?
- O que significa `essential` vs `inspection`?
- Qual a diferença entre supervisão local e dashboard histórico?

## Etapa B — Contratos e operação

Ler e consolidar:

- `docs/mqtt.md`
- `docs/data-classification.md`
- `docs/testing-strategy.md`

Perguntas que o professor deve conseguir responder:

- Quais tópicos MQTT existem?
- O que cada payload carrega?
- Como a configuração remota acontece?
- Como QoS 0 e QoS 1 se refletem no sistema?

## Etapa C — Domínio por componentes

Estudar em sequência:

- `config_manager`
- `telemetry_manager`
- `diagnostics_manager`
- `power_manager`
- `watchdog_manager`
- `telemetry_store`
- núcleo MQTT modular

Perguntas que o professor deve conseguir responder:

- Qual a responsabilidade de cada componente?
- O que entra nele?
- O que sai dele?
- Com quais componentes ele conversa?
- O que quebra se ele falhar?

## Etapa D — Supervisor e dashboards

Estudar:

- `supervisor/backend`
- `supervisor/frontend`
- `docs/dashboard-bootstrap.md`
- `docs/dashboard-operational-questions.md`
- `docs/dashboard-roadmap.md`

Perguntas que o professor deve conseguir responder:

- O que o supervisor faz?
- O que a página resolve?
- O que o Grafana resolve melhor que a página?
- O que é cálculo derivado e o que vem do firmware?

---

# 4. Matriz de domínio docente

## Nível 1 — Obrigatório

O professor deve dominar sem consulta:

- visão geral do sistema;
- modos `continuous` e `low_power`;
- perfis `essential` e `inspection`;
- tópicos MQTT principais;
- papel dos componentes centrais;
- função da página de supervisão;
- função do PostgreSQL e do Grafana.

## Nível 2 — Recomendado

O professor deve dominar com pequena consulta eventual:

- detalhes internos de store-and-forward;
- detalhes da modularização MQTT;
- critérios operacionais de criticidade;
- disponibilidade estimada;
- relação entre eventos, telemetria e diagnóstico.

## Nível 3 — Especializado

Pode ficar apoiado em material auxiliar:

- detalhes finos de SQL dos dashboards;
- ajustes visuais do Grafana;
- nuances futuras de variantes de firmware por linha de produto.

---

# 5. Perguntas prováveis dos alunos

O professor deve se preparar para perguntas como:

- Por que usar ESP-IDF e não Arduino?
- Por que o projeto foi modularizado?
- Por que separar política de publicação de transporte MQTT?
- Por que existe `health` além de `status`?
- Por que o `inspection` não deve ficar ligado o tempo todo?
- Por que `low_power` tem overhead além do tempo de sono?
- O que justifica store-and-forward em flash?
- O que justifica usar PostgreSQL + Grafana?
- O que ficaria no dashboard e o que deveria ficar no firmware?

---

# 6. Estratégia de aula

## 6.1 Abordagem recomendada

Em aula, priorizar sempre esta ordem:

1. problema;
2. conceito;
3. arquitetura;
4. operação;
5. implementação.

Essa ordem reduz ansiedade do aluno e evita que o curso vire simples leitura de
código.

## 6.2 Regra prática

Sempre que introduzir um componente, responder:

- por que ele existe;
- que problema evita;
- qual é sua fronteira;
- que tradeoff representa.

## 6.3 Erro a evitar

Não começar pela implementação detalhada do `mqtt_manager` ou por callbacks
isolados de firmware.

Pedagogicamente, o aluno primeiro precisa ver o mapa antes de visitar as ruas.

---

# 7. Laboratórios essenciais para o professor dominar

Antes de ensinar, o professor deve conseguir executar sem hesitação:

1. build e flash do firmware;
2. leitura da telemetria no monitor MQTT;
3. alteração de intervalo por MQTT;
4. troca de `continuous` para `low_power`;
5. troca de `essential` para `inspection`;
6. leitura do `status`, `health` e `inventory`;
7. uso da página do supervisor;
8. leitura dos dashboards principais;
9. interpretação de um caso de degradação de rede;
10. interpretação de um caso de degradação de bateria ou sensor.

---

# 8. Roteiro de preparação pessoal

## Semana 1 — domínio da base

- ler documentação central;
- compilar e gravar;
- revisar tópicos MQTT;
- revisar modos de operação.

## Semana 2 — domínio arquitetural

- estudar componentes principais;
- montar mapas pessoais de responsabilidade;
- revisar desacoplamento MQTT.

## Semana 3 — domínio operacional

- praticar página de supervisão;
- praticar reconfiguração;
- praticar cenários com dashboards;
- simular perguntas de alunos.

## Semana 4 — fechamento didático

- revisar sequência das aulas;
- escrever exemplos;
- preparar exercícios;
- consolidar linguagem acadêmica e progressão conceitual.

---

# 9. Linguagem acadêmica recomendada

Como o curso terá tom acadêmico, recomenda-se:

- explicitar objetivos de aprendizagem;
- separar descrição de avaliação crítica;
- diferenciar arquitetura atual de possibilidades futuras;
- tratar decisões de projeto como hipóteses justificadas, não verdades eternas;
- sempre relacionar implementação com requisito funcional ou operacional.

Termos úteis:

- responsabilidade;
- acoplamento;
- coesão;
- robustez;
- observabilidade;
- persistência;
- escalabilidade;
- contrato;
- cadência operacional;
- interpretação derivada.

---

# 10. Critério de sucesso do professor

O professor estará bem preparado quando conseguir:

- explicar o SentinelNode sem depender do código aberto na tela;
- localizar rapidamente qualquer parte no repositório;
- defender a arquitetura atual com honestidade;
- apontar limites sem perder clareza;
- transformar comportamento observado em explicação didática.

---

# 11. Próximo passo natural

Depois deste roteiro, o mais útil é criar:

1. `syllabus/` por módulo;
2. laboratórios por módulo;
3. diagramas de apoio;
4. banco de perguntas frequentes para aula.
