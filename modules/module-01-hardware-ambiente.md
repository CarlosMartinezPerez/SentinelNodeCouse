# Módulo 1 — Hardware e ambiente de desenvolvimento

## Natureza da aula

Aula de preparação experimental e contato inicial com a ferramenta de desenvolvimento.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- identificar o hardware de referência do projeto;
- preparar o ambiente ESP-IDF;
- compilar o firmware;
- gravar o firmware na placa;
- abrir o monitor serial e observar o sistema em execução.

## Pré-requisitos

- noções básicas de terminal Linux;
- noções elementares de compilação e gravação em microcontroladores.

## Tópicos de exposição

1. ESP32 como plataforma de referência;
2. papel do BMP280, MPU6500 e medição de bateria na bancada de referência;
3. organização do ambiente com ESP-IDF 6.0.1;
4. build, flash e monitor;
5. diferença entre monitor serial e monitor MQTT.

## Comandos-base

```bash
cd /home/carlos/esp32_projects/SentinelNode
idf.py build
idf.py -p /dev/ttyACM0 flash
idf.py -p /dev/ttyACM0 monitor
```

## Demonstração prática sugerida

- compilar o projeto em sala;
- gravar a placa;
- abrir o monitor serial;
- ligar o monitor MQTT em paralelo.

## Exercício sugerido

Solicitar ao estudante que:

1. faça o build do projeto;
2. identifique a porta serial da placa;
3. grave e abra o monitor;
4. registre os primeiros sinais observados no boot.

## Perguntas para discussão

- Quais informações aparecem primeiro no boot?
- O que o monitor serial mostra que o MQTT não mostra?
- O que o MQTT mostra que o serial não organiza tão bem para operação remota?

## Resultado esperado

O estudante deve sair da aula apto a reproduzir o ciclo mínimo de desenvolvimento e observação do firmware.
