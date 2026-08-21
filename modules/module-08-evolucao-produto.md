# Módulo 8 — Evolução do projeto e produto

## Natureza da aula

Aula de síntese e projeto: transforma a compreensão do SentinelNode em decisões justificadas de evolução de firmware, hardware e operação.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- avaliar limites e extensões naturais da arquitetura atual;
- distinguir variação de configuração de nova variante de produto;
- propor evoluções sem confundir responsabilidades entre nó, supervisor e dashboard;
- justificar escolhas para diferentes cenários industriais.

## Pré-requisitos

- domínio geral dos módulos anteriores;
- capacidade de relacionar requisitos de campo a decisões técnicas.

## Tópicos de exposição

1. o SentinelNode como plataforma e não apenas como firmware de exemplo;
2. nós contínuos, nós de baixo consumo e implicações de cada modo;
3. alimentação por fonte, bateria e energia solar;
4. sensores específicos por aplicação e capacidades declaradas no inventário;
5. quando criar firmware, hardware ou configuração específicos;
6. roadmap: robustez, produto industrial, integração de dashboard e análise de vibração.

## Demonstração prática sugerida

Comparar dois cenários:

- um nó de máquina alimentado continuamente e com monitoramento frequente;
- um nó em tubulação remota, com bateria/solar e coleta espaçada.

Para cada cenário, mostrar como mudam sensores, cadência, política de publicação, alimentação e supervisão.

## Exercício sugerido

Pedir ao estudante que elabore uma proposta de implantação para um ativo industrial, contendo:

1. objetivo de medição;
2. sensores necessários;
3. modo de operação e cadência;
4. política MQTT;
5. dados que devem aparecer na página e no dashboard;
6. riscos e mecanismos de robustez necessários.

## Perguntas para discussão

- Quando separar firmwares reduz complexidade e quando fragmenta o produto prematuramente?
- Que decisões devem ser tomadas no hardware e não podem ser corrigidas apenas por software?
- Em que ponto uma análise de vibração pede processamento adicional ou aprendizado de máquina?

## Resultado esperado

O estudante deve terminar o curso apto a discutir o SentinelNode como base para uma solução industrial concreta, com escolhas técnicas justificadas e progressivas.
