# SentinelNodeCourse

Curso aberto sobre o SentinelNode: um sistema de telemetria industrial baseado
em ESP32, ESP-IDF, MQTT, supervisor local em contêiner e dashboards para
operação e manutenção.

Este repositório foi pensado para ensinar o SentinelNode de forma progressiva,
didática e prática, do hardware ao dashboard.

---

# O que é o curso

O `SentinelNodeCourse` não é apenas um curso de firmware.

Ele mostra como construir e entender um sistema completo, incluindo:

- firmware modular em ESP-IDF;
- sensores e coleta de dados;
- configuração remota via MQTT;
- robustez operacional;
- modos `continuous` e `low_power`;
- supervisão local com backend, frontend e broker MQTT;
- persistência histórica em PostgreSQL;
- dashboards operacionais e executivos em Grafana.

Em outras palavras:

é um curso sobre arquitetura, operação e evolução de um nó industrial realista.

---

# Para quem é este curso

Este curso é indicado para:

- estudantes de sistemas embarcados;
- desenvolvedores que usam ESP32;
- profissionais de automação e IoT industrial;
- integradores que queiram montar soluções próprias;
- pessoas que já fizeram projetos simples com sensores e MQTT e querem subir de
  nível.

Pré-requisitos desejáveis:

- noções de C;
- noções básicas de microcontroladores;
- familiaridade básica com Linux e terminal;
- noções básicas de rede e MQTT.

---

# O que o aluno vai aprender

Ao longo do curso, o aluno vai entender:

- como o SentinelNode foi estruturado por componentes;
- como separar coleta, política de publicação, transporte e diagnóstico;
- como projetar contratos MQTT limpos e operacionais;
- como lidar com falhas de broker, falhas de sensor e quedas de rede;
- como implementar store-and-forward com RAM e flash;
- como supervisionar nós com uma página web local;
- como persistir dados históricos e montar dashboards úteis;
- como pensar na evolução do projeto para produto real.

---

# Estrutura do curso

## Módulo 0 — Visão geral

- o problema
- a solução
- arquitetura geral

## Módulo 1 — Hardware e ambiente

- ESP32
- ESP-IDF
- build, flash e monitor

## Módulo 2 — Arquitetura do firmware

- organização do repositório
- separação por componentes
- fluxo do sistema

## Módulo 3 — Estudo componente por componente

- configuração
- telemetria
- diagnósticos
- energia
- watchdog
- persistência
- MQTT modular

## Módulo 4 — Contrato MQTT

- tópicos
- payloads
- comandos
- configuração remota
- QoS

## Módulo 5 — Robustez operacional

- reconnect
- backoff
- store-and-forward
- recuperação de falhas
- comportamento em `low_power`

## Módulo 6 — Supervisor local

- broker MQTT
- backend
- frontend
- monitor MQTT
- operação local

## Módulo 7 — Dashboards e análise

- PostgreSQL
- Grafana
- dashboards de overview, operations, inspection e executive

## Módulo 8 — Evolução para produto

- variantes de firmware
- diferenças entre nós contínuos e de baixo consumo
- decisões de hardware
- expansão para cenários reais

---

# Filosofia do curso

Este curso segue uma ideia simples:

primeiro entender o sistema, depois modificar o sistema.

Ou seja, o foco não é decorar código. O foco é dominar:

- responsabilidades;
- fluxos;
- contratos;
- comportamento esperado;
- limitações e tradeoffs.

Isso torna o aluno capaz de:

- manter o projeto;
- estender o projeto;
- adaptar a arquitetura para outros contextos.

---

# O que existe neste repositório

Este repositório deve concentrar:

- planejamento das aulas;
- material de apoio;
- diagramas;
- laboratórios práticos;
- referências cruzadas para o repositório principal do SentinelNode.

Estrutura inicial do repositório:

```text
SentinelNodeCourse/
├── README.md
├── modules/
├── labs/
├── diagrams/
├── slides/
└── references/
```

---

# Relação com o repositório principal

O curso usa como base o projeto principal:

- firmware do nó;
- supervisor local;
- dashboards;
- documentação técnica.

O curso não substitui o repositório principal do SentinelNode.

Ele existe para ensinar o raciocínio por trás da solução.

---

# Resultado esperado para o aluno

Ao final do curso, a pessoa deve ser capaz de:

- compilar, gravar e monitorar um nó;
- entender a arquitetura do firmware;
- alterar parâmetros e comportamento com segurança;
- operar a supervisão local;
- interpretar dashboards e sinais de degradação;
- evoluir o projeto com mais autonomia.

---

# Estado atual do curso

Este repositório está em construção.

O foco inicial é organizar:

- a estrutura programática;
- a trilha didática;
- os laboratórios;
- os materiais visuais.

---

# Próximos passos

- publicar o plano detalhado por módulo;
- criar os primeiros laboratórios;
- desenhar diagramas da arquitetura;
- preparar roteiro de estudo do professor;
- converter a documentação técnica em trilha pedagógica.

---

# Licença e uso

Defina aqui a licença que desejar para o material do curso.

Se o curso vier a ser público, também vale incluir:

- regras de reutilização;
- créditos;
- formato de contribuição.


---

# Estrutura programática e materiais

Documentos iniciais já disponíveis neste repositório:

- [Estrutura programática](docs/estrutura-programatica.md)
- [Plano de curso](docs/course-plan.md)
- [Roteiro de estudo do professor](docs/professor-study-guide.md)

Módulos já estruturados:

- [Módulo 0 — Introdução e visão sistêmica](modules/module-00-introducao.md)
- [Módulo 1 — Hardware e ambiente de desenvolvimento](modules/module-01-hardware-ambiente.md)
- [Módulo 2 — Arquitetura do repositório e fluxo do sistema](modules/module-02-arquitetura-repositorio.md)
- [Módulo 3 — Componentes fundamentais do firmware](modules/module-03-componentes-firmware.md)
- [Módulo 4 — Núcleo MQTT e contratos de comunicação](modules/module-04-mqtt-contratos.md)
- [Módulo 5 — Robustez operacional](modules/module-05-robustez-operacional.md)
- [Módulo 6 — Supervisor local](modules/module-06-supervisor-local.md)
- [Módulo 7 — Persistência histórica e dashboards](modules/module-07-dashboards-analise.md)
- [Módulo 8 — Evolução do projeto e produto](modules/module-08-evolucao-produto.md)

Laboratórios iniciais:

- [Laboratório 1 — Build, flash e monitor](labs/lab-01-build-flash-monitor.md)
- [Laboratório 2 — Tópicos MQTT e configuração remota](labs/lab-02-topicos-mqtt-e-configuracao.md)
- [Laboratório 3 — Robustez e falhas controladas](labs/lab-03-robustez-e-falhas-controladas.md)
