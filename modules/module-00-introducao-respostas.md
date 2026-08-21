# Módulo 0 — Introdução e visão sistêmica: respostas

Este material apresenta respostas-modelo. Elas não são as únicas formulações possíveis; o importante é que o estudante relacione requisitos técnicos, arquitetura e operação.

## Exercício sugerido

### Diferença entre um nó sensor simples e um nó sensor com arquitetura operacional completa

Um nó sensor simples lê um ou mais sensores e transmite valores, normalmente como prova de conceito. Em geral, concentra-se na aquisição e na comunicação imediata, sem prever de modo sistemático falhas de rede, indisponibilidade do broker, recuperação do barramento ou acompanhamento remoto do estado do equipamento.

Um nó com arquitetura operacional completa continua medindo, comunicando e informando seu estado dentro de limites previsíveis mesmo diante de falhas parciais. Além de sensores e MQTT, ele incorpora configuração persistente, diagnóstico, recuperação, política de publicação, retenção temporária de dados, supervisão por watchdog e interfaces de operação e análise. O SentinelNode é estudado nessa segunda perspectiva.

## Perguntas para discussão

### Em que momento um projeto embarcado deixa de ser só um protótipo e passa a ser um sistema?

Quando deixa de depender de condições ideais e passa a possuir comportamento definido para situações reais de operação. Isso inclui inicialização previsível, configuração identificável, tratamento de falhas, recuperação de comunicação, observabilidade remota, atualização controlada e critérios para afirmar se o nó está saudável ou degradado. Não é uma mudança determinada apenas pelo tamanho do código: é uma mudança de responsabilidade operacional.

### Quais riscos aparecem quando comunicação, diagnóstico e persistência são ignorados?

Sem comunicação resiliente, uma falha de Wi-Fi ou do broker pode interromper a entrega de dados sem que alguém perceba. Sem diagnóstico, o nó pode permanecer conectado enquanto um sensor está ausente, o I²C está travado ou as leituras não são confiáveis. Sem persistência, configurações podem se perder após reinicialização e telemetrias produzidas durante indisponibilidade da rede podem desaparecer. O resultado é um sistema aparentemente funcional, mas difícil de manter, auditar e confiar em campo.

### Por que pensar em operação desde o início muda a arquitetura do firmware?

Porque requisitos de operação definem responsabilidades que precisam existir desde a base: quem registra configuração, quem publica estado, quem decide quando reenviar dados, quem recupera uma falha e como a interface externa confirma uma ação. Se essas decisões são deixadas para depois, é comum concentrar regras em um único módulo de MQTT ou espalhá-las por tarefas sem contrato claro. Ao projetar para operação desde o início, o firmware tende a separar aquisição, protocolo, política de publicação, persistência, diagnóstico e supervisão, tornando mudanças futuras mais seguras e compreensíveis.
