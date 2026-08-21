# Módulo 2 — Arquitetura do repositório e fluxo do sistema

## Natureza da aula

Aula de leitura arquitetural e organização sistêmica do projeto.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- navegar pelo repositório com critério;
- distinguir responsabilidades entre diretórios e componentes;
- explicar o fluxo de informações do sistema;
- preparar-se para estudar o firmware por módulos.

## Pré-requisitos

- familiaridade básica com a estrutura de um projeto em C;
- conclusão do módulo de ambiente e primeira execução.

## Tópicos de exposição

1. organização geral do repositório;
2. função de `components/`, `main/`, `docs/`, `supervisor/` e `tools/`;
3. boot e inicialização;
4. coleta de sensores;
5. publicação MQTT;
6. persistência, supervisão e dashboards.

## Demonstração prática sugerida

- abrir o repositório e percorrer as pastas principais;
- mostrar como uma informação sai do sensor e chega ao dashboard;
- usar um quadro ou terminal para mapear dependências.

## Exercício sugerido

Pedir ao estudante que monte um pequeno mapa textual com:

- onde nasce a telemetria;
- onde ela é publicada;
- onde ela é persistida;
- onde ela é visualizada.

## Perguntas para discussão

- Por que a arquitetura do repositório importa para manutenção?
- O que se perde quando tudo fica concentrado em poucos arquivos?
- Em que medida a estrutura de pastas já antecipa a arquitetura do sistema?

## Resultado esperado

O estudante deve sair desta aula sabendo localizar responsabilidades no projeto e enxergar o SentinelNode como um sistema articulado, não como um conjunto solto de arquivos.
