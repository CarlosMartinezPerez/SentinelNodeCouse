# Módulo 5 — Robustez operacional

## Natureza da aula

Aula sobre falhas previsíveis em sistemas embarcados conectados e sobre as decisões que impedem que uma falha localizada interrompa a operação do nó.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- justificar watchdog, reconexão, persistência e recuperação de I²C;
- distinguir falha funcional de perda de observabilidade;
- interpretar backlog, reconexão e diagnóstico de sensores;
- relacionar cada mecanismo de robustez a um componente do firmware.

## Pré-requisitos

- compreensão da arquitetura do firmware;
- noções de MQTT e de leitura de telemetria.

## Tópicos de exposição

1. por que robustez não pode ficar concentrada em um único arquivo;
2. watchdog e supervisão de execução;
3. store-and-forward híbrido: RAM, flash e política de fila;
4. reconexão Wi-Fi/MQTT, backoff e recuperação após broker indisponível;
5. falhas de sensores, recuperação de I²C e estado degradado;
6. o que o operador observa no MQTT, na página e no dashboard.

## Demonstração prática sugerida

- interromper o broker MQTT e observar a formação e a drenagem do backlog;
- provocar uma falha temporária no barramento I²C, quando o hardware permitir;
- observar a mudança de diagnósticos sem perda de controle do nó;
- mostrar no código onde cada responsabilidade é implementada.

## Exercício sugerido

Apresentar três cenários: broker indisponível, sensor ausente e queda de Wi-Fi. Pedir que o estudante indique:

1. quais componentes participam da recuperação;
2. quais tópicos ou telas permitem observar o problema;
3. qual dado pode ser perdido e qual deve ser preservado.

## Perguntas para discussão

- Por que é preferível descartar telemetria antiga a bloquear o firmware?
- Em que situação a persistência em flash é essencial e quando ela pode ser excessiva?
- Um nó online com sensor inválido está saudável? Como comunicar isso ao operador?

## Resultado esperado

O estudante deve entender robustez como propriedade arquitetural do conjunto, e não como uma coleção de tratamentos de erro isolados.
