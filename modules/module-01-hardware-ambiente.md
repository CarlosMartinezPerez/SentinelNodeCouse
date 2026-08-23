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

### Configurar o nó antes do primeiro flash

No SentinelNode, o aluno não deve procurar pinos, broker e defaults em vários drivers. A configuração pré-flash não secreta fica reunida em:

```text
components/config_manager/node_config.h
```

Esse arquivo contém, em seções separadas:

- identidade do nó e URI do broker MQTT;
- pinos e frequência do I²C;
- endereços de BMP280 e MPU6500;
- medição de bateria, divisor de tensão e LED de Wi-Fi;
- valores usados no primeiro boot e após `factory_reset`.

Credenciais não ficam nesse arquivo. O aluno deve criar localmente o arquivo ignorado pelo Git:

```bash
cp components/config_manager/wifi_credentials_example.h \
   components/config_manager/wifi_credentials.h
```

Depois, preenche SSID e senha em `wifi_credentials.h`. Esse arquivo não deve ser enviado ao GitHub, exibido em aula ou incluído em documentação.

### Perfil protegido da placa de referência

O perfil suportado pelo curso é ESP32 com 4 MB de flash. `sdkconfig.defaults` e `partitions.csv` fixam a arquitetura de build e a área persistente da telemetria; não são arquivos de configuração rotineira do aluno.

Após compilar, confirme o perfil com:

```bash
bash tools/verify_board_profile.sh
```

O comando verifica target `esp32`, flash de 4 MB e o layout de partições esperado. Ele não modifica arquivos. Uma troca para ESP32-C3, S3 ou outra capacidade de flash exige estudo próprio de target, GPIO, ADC, partições e testes; não é uma alteração de instalação comum.

### Inspecionar e configurar o projeto

Execute os comandos abaixo a partir da raiz do projeto:

```bash
cd /home/carlos/esp32_projects/SentinelNode
idf.py --list-targets
idf.py partition-table
idf.py size
idf.py size-components
```

- `partition-table` mostra como a flash está dividida entre NVS (Non-Volatile Storage — armazenamento não volátil), aplicação e áreas de dados;
- `size` e `size-components` ajudam a acompanhar o consumo de memória do firmware.

O configurador interativo é aberto por:

```bash
idf.py menuconfig
```

Nele se definem opções avançadas de build, bootloader e recursos do ESP-IDF. No perfil de referência, o aluno não deve alterar tamanho da flash ou tabela de partições por `menuconfig`: essas decisões já estão protegidas no repositório. Alterações avançadas devem ser feitas conscientemente, com revisão no Git e validação de build.

Para selecionar a família da placa, use apenas quando for realmente necessário mudar de alvo:

```bash
idf.py set-target esp32
```

Por exemplo, uma migração para ESP32-C3 usaria `idf.py set-target esp32c3`. Esse comando recria a configuração de build para o alvo selecionado; não deve ser usado como etapa rotineira de compilação do SentinelNode baseado em ESP32.

### Compilar, gravar e observar

```bash
idf.py build
bash tools/verify_board_profile.sh
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
