# Módulo 3 — Componentes do firmware: respostas

Este gabarito descreve os componentes a partir da implementação atual do SentinelNode. “Dados de saída” inclui tanto valores retornados por funções quanto efeitos observáveis por outros componentes, MQTT, logs ou comportamento do nó.

## 1. `config_manager`

**Responsabilidade.** Manter a configuração operacional do nó em memória e persistir os valores em NVS. Centraliza intervalo de telemetria, habilitação de sensores, RSSI, modo `continuous` ou `low_power`, perfil de publicação, QoS e intervalo de sono.

**Dados de entrada.** Valores de primeiro boot definidos em `node_config.h`; configuração carregada da NVS; alterações recebidas pelo caminho de configuração MQTT e validadas pelo protocolo.

**Dados de saída.** A estrutura `node_runtime_config_t`, consultada pelos demais componentes; resultado de validação/persistência; contagem de gravações em flash; valores de configuração apresentados em `status`, `inventory` e respostas a comando.

**Sintoma se falhar.** O nó pode iniciar com padrões inesperados, esquecer configuração após reboot, rejeitar mudanças legítimas ou, no pior caso, operar no modo, intervalo ou QoS incorretos. No terminal e na página, uma configuração enviada pode não coincidir com a configuração efetiva observada depois.

## 2. `telemetry_manager`

**Responsabilidade.** Reunir em uma estrutura única a leitura dos sensores, RSSI, horário, identificadores de boot e diagnósticos. Também coordena a tentativa de recuperação de I²C após falhas consecutivas de BMP280 ou MPU6500. Ele prepara dados; não é o componente que decide política MQTT nem realiza a publicação.

**Dados de entrada.** Leituras dos drivers BMP280, MPU6500 e bateria; RSSI e IP do Wi-Fi; tempo do `time_manager`; diagnóstico do `diagnostics_manager`; configuração de sensores habilitados; barramento do `i2c_manager` durante recovery.

**Dados de saída.** `telemetry_data_t`, contendo valores físicos, campos `*_valid`, uptime, horário, RSSI, boot, memória, reconexões e contadores de erro/recuperação.

**Sintoma se falhar.** Telemetria pode deixar de ser produzida, conter campos ausentes ou inválidos, ou deixar de refletir diagnóstico real. Falhas repetidas dos sensores podem não disparar a recuperação de I²C, levando a leituras ausentes persistentes.

## 3. `diagnostics_manager`

**Responsabilidade.** Registrar e disponibilizar o estado técnico do nó: boot, motivo de reset, memória, reconexões Wi-Fi/MQTT, falhas de sensor, tentativas de recuperação I²C e dados correlatos. Parte dos dados de boot é persistida em NVS para distinguir boots e wakes.

**Dados de entrada.** Motivo de reset do ESP-IDF; relógio de uptime; informações de heap; eventos de Wi-Fi e MQTT; resultados de drivers e do recovery I²C; NVS de diagnósticos.

**Dados de saída.** Estrutura `diagnostics_data_t` para o `telemetry_manager` e para respostas de inspeção; contadores e informações como `boot_count`, `wake_count`, `reset_reason`, erros de sensores e dados de recuperação.

**Sintoma se falhar.** O nó pode continuar coletando e publicando, mas perde capacidade de explicar a própria condição. Boot, reset, reconexões, memória e falhas de sensores tornam-se imprecisos, ausentes ou congelados. É uma degradação de observabilidade que dificulta manutenção.

## 4. `power_manager`

**Responsabilidade.** Implementar o comportamento de economia de energia. No modo `low_power`, coordena sincronização de horário, espera de amostra e entrega, janela de reconfiguração, compensação de duração de sono e entrada em deep sleep por temporizador.

**Dados de entrada.** Modo e intervalo de sono do `config_manager`; estado MQTT; indicação de amostra coletada; estado da fila do `telemetry_store`; sincronização do `time_manager`; regras do `publish_policy`.

**Dados de saída.** Configuração do despertador por timer, entrada em deep sleep e logs do ciclo de energia. Seu efeito é observável pela cadência de boots, telemetrias e estados online/offline.

**Sintoma se falhar.** Em baixo consumo, o nó pode não dormir, dormir cedo demais, não publicar a amostra antes de dormir, ou acordar em cadência diferente da configurada. Em casos de falha de decisão, pode ficar preso acordado aguardando uma condição que não chega.

## 5. `watchdog_manager`

**Responsabilidade.** Configurar e alimentar o task watchdog do ESP-IDF. Ajuda a detectar tarefas bloqueadas por tempo excessivo e, conforme a configuração, provoca reset para recuperar o firmware.

**Dados de entrada.** Configuração de timeout do watchdog e handles de tarefas que devem ser supervisionadas; chamadas periódicas de reset/alimentação do watchdog.

**Dados de saída.** Resultado das operações de registro/reset; logs de configuração ou erro; em caso de travamento real, reset supervisionado do sistema.

**Sintoma se falhar.** Se não for iniciado ou alimentado corretamente, uma tarefa pode travar indefinidamente sem reinicialização de recuperação. Se configurado de forma errada, pode produzir resets recorrentes e o `reset_reason` pode indicar watchdog.

## 6. `time_manager`

**Responsabilidade.** Inicializar SNTP, acompanhar a sincronização de horário e fornecer tempo Unix e ISO 8601. O horário válido é requisito para publicar telemetria com timestamp confiável.

**Dados de entrada.** Conectividade de rede já estabelecida; servidores SNTP configurados pelo sistema; relógio interno do ESP32.

**Dados de saída.** Estado de sincronização, timestamp Unix e string ISO; sinalização para componentes que aguardam horário antes de executar um ciclo de baixo consumo.

**Sintoma se falhar.** Após boot, as telemetrias podem não sair enquanto o firmware aguarda horário válido, ou podem aparecer sem timestamp confiável se essa proteção for removida. Dashboards históricos receberiam amostras fora de ordem ou sem tempo utilizável.

## 7. `i2c_manager`

**Responsabilidade.** Criar e manter o barramento I²C mestre compartilhado e expor seu handle aos drivers. Também oferece o reset lógico do barramento usado na recuperação após falhas.

**Dados de entrada.** Configuração física de porta, SDA, SCL e resistores internos; pedidos de inicialização e reset dos componentes que usam I²C.

**Dados de saída.** Handle do barramento I²C e códigos `esp_err_t` de inicialização/reset.

**Sintoma se falhar.** BMP280 e MPU6500 não inicializam ou passam a retornar erro; os campos de validade tornam-se falsos e contadores de erro sobem. Quando os dois sensores I²C falham repetidamente, a recuperação pode também falhar, deixando o nó em estado degradado enquanto bateria e RSSI podem continuar disponíveis.

## 8. Drivers de sensores: `bmp280`, `mpu6500` e `battery`

**Responsabilidade.** Cada driver conhece o protocolo e a conversão específica do seu hardware:

- `bmp280`: inicializa o sensor de pressão/temperatura e converte registros em °C e hPa;
- `mpu6500`: inicializa o IMU e converte aceleração em g e giro em °/s;
- `battery`: lê o ADC e converte a tensão medida em volts segundo o divisor resistivo configurado.

**Dados de entrada.** Acesso I²C e registros físicos para BMP280/MPU6500; sinal analógico no ADC para bateria; parâmetros de inicialização e sensores habilitados no `config_manager`.

**Dados de saída.** Valores de temperatura, pressão, aceleração, giroscópio e tensão; indicação de validade; códigos de erro; contadores de erro encaminhados ao diagnóstico.

**Sintoma se falhar.** O sintoma é localizado ao sensor: `bmp280_valid`, `mpu6500_valid` ou `battery_valid` fica falso, valores deixam de aparecer ou ficam inválidos, e o respectivo contador de erro aumenta. Uma falha dos sensores I²C pode levar a recovery; falha de bateria não depende do barramento I²C e não deve derrubar os demais sensores.

## 9. `telemetry_store`

**Responsabilidade.** Implementar store-and-forward para telemetria quando a conectividade MQTT não está disponível. Mantém uma fila RAM curta, migra registros para flash/NVS quando necessário e permite que o mecanismo de entrega leia e confirme a remoção de registros publicados.

**Dados de entrada.** Registros de telemetria serializados, sequência do registro, indicação de conexão MQTT e confirmações de entrega; metadados e registros persistidos na partição de telemetria.

**Dados de saída.** Próximo registro pendente para publicação, profundidade de fila RAM/flash, capacidade, contadores de descarte e de erro de persistência, além de resultados de `enqueue`, `peek` e `acknowledge`.

**Sintoma se falhar.** Durante queda do broker ou Wi-Fi, telemetrias podem ser perdidas imediatamente, a fila pode não drenar quando a conexão retorna, ou o nó pode publicar duplicatas se a confirmação de remoção for inconsistente. Os dados de backlog e persistência na inspeção ajudam a distinguir esses cenários.

## Perguntas para discussão

### Todo componente precisa ser completamente independente?

Não. Independência absoluta é impraticável em um sistema integrado: o `telemetry_manager` precisa de drivers, o `power_manager` precisa conhecer configuração e entrega, e o `i2c_manager` é deliberadamente compartilhado pelos drivers I²C. O objetivo saudável é dependência explícita, limitada e orientada por responsabilidade. Um componente deve depender de interfaces ou dados necessários à sua função, não conhecer detalhes internos irrelevantes de vários outros componentes.

### Qual o limite saudável entre coesão e acoplamento?

Coesão significa que as funções de um componente pertencem ao mesmo assunto: persistir configuração no `config_manager`, por exemplo. Acoplamento é o quanto um componente precisa conhecer ou controlar outro. O limite saudável é alta coesão e baixo acoplamento: cada componente concentra uma responsabilidade clara e se comunica por tipos, funções e contratos pequenos.

Na prática, é sinal de acoplamento excessivo quando uma mudança de política de publicação exige editar driver de sensor, ou quando o transporte MQTT decide como um sensor deve ser lido. É sinal de abstração excessiva quando se criam camadas que não escondem complexidade real e apenas tornam o fluxo difícil de seguir. O SentinelNode busca separar protocolo, política, entrega, aquisição e energia, mas sem negar dependências físicas e operacionais legítimas.

### Como distinguir falha funcional de falha de observabilidade?

Falha funcional impede ou degrada a finalidade do nó: sensor não mede, telemetria não é publicada, configuração não persiste ou deep sleep não acontece. Ela afeta diretamente a operação física ou a entrega de dados.

Falha de observabilidade prejudica a capacidade de saber o que ocorreu, sem necessariamente interromper a função principal: contador de reconexão incorreto, motivo de reset ausente, inventário desatualizado ou dashboard que não mostra um dado que ainda está sendo medido. É menos visível, mas importante porque torna a falha funcional seguinte mais difícil de diagnosticar. Alguns problemas podem começar como falha de observabilidade e, se não forem percebidos, evoluir para risco operacional.
