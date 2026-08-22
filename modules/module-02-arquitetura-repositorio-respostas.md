# Módulo 2 — Arquitetura do repositório e fluxo do sistema: respostas

Este material apresenta respostas-modelo. O estudante pode usar outros nomes de componentes, desde que preserve a separação entre aquisição, comunicação, persistência, supervisão e visualização.

## Exercício sugerido

### Mapa textual do fluxo da telemetria

```text
Sensores físicos
    ↓
Componentes de aquisição do firmware
    ↓
Estrutura de telemetria e orquestração de coleta
    ↓
Política de publicação e cliente MQTT
    ↓
Broker MQTT: sentinelnode/<node>/telemetry
    ↓
Supervisor local
    ├── página de supervisão: leitura recente, configuração e manutenção
    └── persistência no PostgreSQL
            ↓
        Grafana: histórico, tendências e análise da frota
```

Em termos de responsabilidades:

- a telemetria nasce das leituras dos sensores no firmware, por componentes como BMP280, MPU6500, bateria e RSSI;
- ela é organizada e publicada no tópico MQTT `sentinelnode/<node>/telemetry`;
- o supervisor consome a mensagem e registra os dados históricos no PostgreSQL;
- a página de supervisão mostra a situação recente e permite operar o nó, enquanto os dashboards Grafana visualizam o histórico e indicadores derivados.

Em condições de falha de rede, a telemetria também pode passar pela fila de store-and-forward do próprio nó antes de alcançar o broker. Essa fila é uma proteção operacional; ela não substitui a persistência histórica do PostgreSQL.

## Perguntas para discussão

### Por que a arquitetura do repositório importa para manutenção?

Porque ela torna visível onde cada responsabilidade vive. Ao encontrar um problema de leitura de sensor, o mantenedor pode procurar os componentes de aquisição; diante de uma falha de protocolo, pode examinar a camada MQTT; para uma inconsistência visual, pode investigar o supervisor. Essa previsibilidade reduz tempo de diagnóstico, diminui o risco de alterar uma área errada e torna o projeto mais acessível a novos integrantes.

Além disso, uma estrutura coerente ajuda a limitar dependências. Um componente não precisa conhecer toda a aplicação: deve conhecer apenas as interfaces necessárias para cumprir sua função. Isso torna refatorações e testes mais seguros.

### O que se perde quando tudo fica concentrado em poucos arquivos?

Perdem-se clareza, capacidade de teste e segurança para evoluir. Um arquivo central tende a acumular leitura de sensores, regras de operação, MQTT, persistência, logs e decisões de interface. Com o tempo, uma alteração aparentemente simples passa a ter efeitos difíceis de prever, pois as dependências ficam implícitas.

Também se perde a possibilidade de discutir o sistema em partes. Em vez de perguntar “qual é a política de publicação?”, a equipe precisa procurar essa política misturada com callbacks de rede e código de driver. O resultado costuma ser manutenção lenta, duplicação de lógica e maior probabilidade de regressões.

### Em que medida a estrutura de pastas já antecipa a arquitetura do sistema?

A estrutura de pastas é uma primeira declaração de responsabilidades. No SentinelNode, `components/` abriga blocos reutilizáveis do firmware; `main/` compõe a aplicação; `supervisor/` concentra a camada local de operação, banco e interface; `tools/` reúne utilitários de desenvolvimento e operação; `docs/` guarda contratos e decisões que não devem ficar apenas no código.

Ela não garante, por si só, bom desacoplamento: um componente pode continuar dependendo indevidamente de outro. Mas, quando acompanha interfaces claras e disciplina de dependências, a organização física do repositório orienta a leitura, facilita revisões e antecipa como o sistema foi dividido conceitualmente.
