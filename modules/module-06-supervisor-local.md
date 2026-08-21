# Módulo 6 — Supervisor local

## Natureza da aula

Aula sobre a camada local que transforma MQTT em uma ferramenta de operação, configuração e manutenção de nós.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- explicar o papel do supervisor no ecossistema SentinelNode;
- distinguir broker, backend, frontend, monitor e banco de dados;
- iniciar a stack local e navegar pela página de supervisão;
- usar monitor MQTT e página web de forma complementar.

## Pré-requisitos

- compreensão básica dos contratos MQTT;
- ambiente local com Docker e Docker Compose disponíveis.

## Tópicos de exposição

1. limites e propósito do supervisor: controle de nó, não dashboard industrial;
2. broker MQTT, backend FastAPI, frontend web e PostgreSQL;
3. launcher, scripts de apoio e containers;
4. descoberta de nós, seleção de foco e inventário;
5. configuração remota, comandos e confirmação operacional;
6. relação entre dados em tempo real e dados históricos persistidos.

## Demonstração prática sugerida

```bash
cd /home/carlos/esp32_projects/SentinelNode
./tools/sentinel_launcher.sh
```

- iniciar broker e supervisor pelo lançador;
- abrir o monitor MQTT e a página local;
- escolher um nó, alterar uma configuração e observar a confirmação;
- mostrar como o monitor ajuda a diagnosticar o que a página resume.

## Exercício sugerido

Pedir ao estudante que descreva o caminho de uma alteração de configuração:

1. seleção na página;
2. publicação MQTT;
3. processamento pelo firmware;
4. confirmação observável;
5. atualização da página.

## Perguntas para discussão

- Por que o ESP32 não deve concentrar a página de supervisão e o dashboard?
- Por que a página local não substitui o monitor MQTT durante manutenção?
- Quais responsabilidades pertencem ao supervisor e quais devem ficar no dashboard?

## Resultado esperado

O estudante deve conseguir levantar e usar a camada de supervisão, compreendendo sua posição entre o nó físico e a análise histórica.
