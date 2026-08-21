# Módulo 2 — Arquitetura do repositório e fluxo do sistema

## Natureza da aula

Aula de leitura arquitetural e organização sistêmica do projeto.

## Objetivos de aprendizagem

Ao final desta aula, o estudante deverá ser capaz de:

- navegar pelo repositório com critério;
- distinguir responsabilidades entre diretórios e componentes;
- explicar o fluxo de informações do sistema;
- preparar-se para estudar o firmware por módulos.

## Pré-requisitos

- familiaridade básica com a estrutura de um projeto em C;
- conclusão do módulo de ambiente e primeira execução.

## Tópicos de exposição

1. organização geral do repositório;
2. função de `components/`, `main/`, `docs/`, `supervisor/` e `tools/`;
3. boot e inicialização;
4. coleta de sensores;
5. publicação MQTT;
6. persistência, supervisão e dashboards.

## Preparação: GitHub, Git e cópia local do SentinelNode

Esta seção permite que um estudante sem experiência prévia acompanhe o módulo com uma cópia local do projeto. O objetivo inicial é **ler, compilar e executar** o SentinelNode; não é necessário alterar ou publicar código nesta etapa.

### 1. Criar uma conta no GitHub

1. Acesse [github.com](https://github.com) no navegador e escolha **Sign up**.
2. Cadastre um endereço de e-mail que o estudante possa acessar, crie uma senha forte e escolha um nome de usuário público.
3. Confirme o e-mail solicitado pelo GitHub.
4. Faça login e complete apenas as informações de perfil que desejar. Nome e foto não são exigidos para estudar o projeto.

O GitHub é o serviço remoto que hospeda o repositório. O Git, usado no terminal, é a ferramenta que mantém o histórico de arquivos no computador. São conceitos relacionados, mas distintos.

### 2. Instalar e identificar o Git no Linux

Em Debian, Ubuntu e derivados, instale o Git com:

```bash
sudo apt update
sudo apt install git
git --version
```

Defina a identificação que aparecerá em futuros commits. Use o mesmo e-mail confirmado no GitHub caso pretenda publicar contribuições:

```bash
git config --global user.name "Nome do estudante"
git config --global user.email "email-do-estudante@exemplo.com"
git config --global --list
```

Esses comandos não enviam nada à internet; apenas configuram a autoria local dos commits.

### 3. Escolher uma pasta de trabalho

Crie ou use uma pasta destinada a projetos. No ambiente de referência do curso, ela é `~/esp32_projects`:

```bash
mkdir -p ~/esp32_projects
cd ~/esp32_projects
pwd
```

`pwd` mostra a pasta atual. Conferir esse caminho antes de clonar evita criar o projeto em um local inesperado.

### 4. Clonar o repositório

O repositório principal do projeto está em:

```text
https://github.com/CarlosMartinezPerez/SentinelNode.git
```

Para obter uma cópia local por HTTPS:

```bash
git clone https://github.com/CarlosMartinezPerez/SentinelNode.git
cd SentinelNode
```

Para estudar, clonar por HTTPS é suficiente. O GitHub não pedirá senha enquanto o estudante apenas lê e atualiza uma cópia de repositório público. Para enviar alterações a um repositório próprio no futuro, será preciso usar uma chave SSH ou token de acesso pessoal; senhas da conta GitHub não são usadas pelo Git para esse fim.

### 5. Confirmar a cópia e explorar sem risco

Na raiz do projeto, execute:

```bash
git status
git remote -v
git log --oneline -5
ls
```

- `git status` informa se há alterações locais;
- `git remote -v` mostra a origem remota usada no clone;
- `git log --oneline -5` mostra os cinco commits mais recentes;
- `ls` permite reconhecer os diretórios principais antes de abri-los no editor.

Para atualizar a cópia local em outra aula, entre na pasta do projeto, confirme primeiro que não há alterações próprias e então execute:

```bash
git status
git pull --ff-only
```

`git pull --ff-only` atualiza somente quando o histórico local pode avançar sem criar uma mesclagem automática. Se `git status` mostrar arquivos modificados, o estudante deve parar, entender o que mudou e pedir orientação antes de atualizar.

### 6. Abrir o projeto no VS Code

Ainda na raiz do repositório:

```bash
code .
```

O ponto final significa “a pasta atual”. No VS Code, comece por `README.md`, `docs/architecture.md`, `main/` e `components/`. A navegação inicial deve ser de leitura: não há necessidade de editar arquivos de credenciais, configurações de Wi-Fi ou tabelas de partição.

### 7. Primeiro fluxo seguro de estudo

Um ciclo recomendado para o aluno iniciante é:

1. atualizar o repositório com `git pull --ff-only`;
2. ler a documentação e localizar os componentes citados na aula;
3. compilar e observar a execução;
4. registrar dúvidas e observações;
5. só depois criar uma alteração pequena em uma cópia ou branch de estudo.

O aluno não deve usar `git push`, `git reset --hard`, `git clean -fd` ou comandos de remoção recursiva sem compreender seus efeitos. Eles não são necessários para acompanhar este módulo.

## Demonstração prática sugerida

- abrir o repositório e percorrer as pastas principais;
- mostrar como uma informação sai do sensor e chega ao dashboard;
- usar um quadro ou terminal para mapear dependências.

## Exercício sugerido

Pedir ao estudante que monte um pequeno mapa textual com:

- onde nasce a telemetria;
- onde ela é publicada;
- onde ela é persistida;
- onde ela é visualizada.

## Perguntas para discussão

- Por que a arquitetura do repositório importa para manutenção?
- O que se perde quando tudo fica concentrado em poucos arquivos?
- Em que medida a estrutura de pastas já antecipa a arquitetura do sistema?

## Resultado esperado

O estudante deve sair desta aula sabendo localizar responsabilidades no projeto e enxergar o SentinelNode como um sistema articulado, não como um conjunto solto de arquivos.
