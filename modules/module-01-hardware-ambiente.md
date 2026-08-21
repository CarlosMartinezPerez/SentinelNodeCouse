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

## Apoio de terminal Linux e ESP-IDF

Os comandos abaixo são material de consulta para a bancada. Eles permitem localizar a placa, ativar o ambiente e inspecionar configurações sem alterar o firmware. Comandos que modificam a configuração do projeto estão identificados explicitamente.

### Identificar a placa e a porta serial

```bash
lsusb
ls /dev/ttyACM* /dev/ttyUSB* 2>/dev/null
fuser -v /dev/ttyACM0
```

- `lsusb` confirma se o conversor USB da placa foi reconhecido pelo Linux;
- `ls /dev/ttyACM* /dev/ttyUSB*` mostra as portas seriais candidatas;
- `fuser` informa se outro processo está usando a porta. Ajuste `ttyACM0` quando a placa usar outra porta.

Para acompanhar conexões e desconexões USB em tempo real:

```bash
journalctl -kf
```

### Ativar e conferir o ambiente ESP-IDF

No ambiente de referência deste curso, o ESP-IDF 6.0.1 está instalado em `/home/carlos/.espressif/v6.0.1/esp-idf`.

```bash
export IDF_PATH=/home/carlos/.espressif/v6.0.1/esp-idf
. "$IDF_PATH/export.sh"
idf.py --version
command -v idf.py
```

Caso o caminho não seja conhecido, procure o script de ativação:

```bash
find /home/carlos/.espressif -type f -name export.sh 2>/dev/null
```

O `export.sh` deve ser executado em cada novo terminal que for usado com o ESP-IDF, salvo se o usuário tiver configurado sua inicialização automática no shell.

### Inspecionar e configurar o projeto

Execute os comandos abaixo a partir da raiz do projeto:

```bash
cd /home/carlos/esp32_projects/SentinelNode
idf.py --list-targets
idf.py partition-table
idf.py size
idf.py size-components
```

- `partition-table` mostra como a flash está dividida entre NVS, aplicação e áreas de dados;
- `size` e `size-components` ajudam a acompanhar o consumo de memória do firmware.

O configurador interativo é aberto por:

```bash
idf.py menuconfig
```

Nele se definem, entre outros aspectos, tamanho da flash, tabela de partições, opções de bootloader, Wi-Fi e recursos de diagnóstico. Alterações no `menuconfig` modificam a configuração de build do projeto e devem ser feitas conscientemente, idealmente com revisão no Git.

Para selecionar a família da placa, use apenas quando for realmente necessário mudar de alvo:

```bash
idf.py set-target esp32
```

Por exemplo, uma migração para ESP32-C3 usaria `idf.py set-target esp32c3`. Esse comando recria a configuração de build para o alvo selecionado; não deve ser usado como etapa rotineira de compilação do SentinelNode baseado em ESP32.

### Compilar, gravar e observar

```bash
idf.py build
idf.py -p /dev/ttyACM0 flash
idf.py -p /dev/ttyACM0 monitor
```

Para gravar e abrir o monitor em sequência:

```bash
idf.py -p /dev/ttyACM0 flash monitor
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
