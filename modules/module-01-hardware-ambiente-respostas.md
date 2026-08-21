# Módulo 1 — Hardware e ambiente de desenvolvimento: respostas

Este material apresenta respostas-modelo para orientar a discussão. O monitor serial e o MQTT são complementares: um não substitui o outro.

## Perguntas para discussão

### Quais informações aparecem primeiro no boot?

Antes da aplicação, o terminal mostra mensagens do ROM bootloader e do bootloader do ESP-IDF: motivo de reset, modo de boot, tamanho e modo de acesso à flash, tabela de partições e carregamento da imagem de firmware. Em seguida, a aplicação informa identificação do projeto, versão do firmware, versão do ESP-IDF e inicialização dos subsistemas.

No SentinelNode, os primeiros registros úteis da aplicação normalmente permitem acompanhar carregamento da configuração persistida, diagnóstico de boot, ativação do watchdog, inicialização de Wi-Fi, obtenção de IP, sincronização de tempo, barramento I²C, sensores, armazenamento de telemetria e cliente MQTT. A ordem e o conteúdo exatos podem variar conforme o modo de operação e a configuração do nó.

### O que o monitor serial mostra que o MQTT não mostra?

O monitor serial mostra o processo interno de inicialização e os detalhes locais de falha. Ele permite ver mensagens do bootloader, pilha Wi-Fi, motivos de erro retornados por APIs, inicialização de drivers, logs de I²C, eventos de reconexão e erros que ocorrem antes de o nó ter rede ou cliente MQTT ativo.

Portanto, é o instrumento principal para depurar a placa durante desenvolvimento, gravação e investigação de uma falha física ou de firmware. Se o nó não consegue conectar-se ao Wi-Fi ou ao broker, o MQTT pode não mostrar nada; o serial ainda mostra por que a inicialização não chegou a essa etapa.

### O que o MQTT mostra que o serial não organiza tão bem para operação remota?

O MQTT organiza a observação por nó e por contrato de comunicação. Ele permite acompanhar telemetria, estado, inventário, eventos e respostas a comandos de diversos nós a partir de um único ponto, sem conexão física USB com cada equipamento. Também permite que a página de supervisão, o banco de dados e os dashboards consumam a mesma informação.

Para operação remota, essa organização facilita comparar nós, verificar cadência de telemetria, identificar quem está online, enviar configuração e registrar histórico. O serial é detalhado e imediato, mas permanece ligado a uma porta física e tende a misturar informações de baixo nível que não são necessárias para a operação normal de uma frota.
