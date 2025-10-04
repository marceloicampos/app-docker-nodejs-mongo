# Orientações para Agentes de IA do Copilot

Este documento fornece orientações para agentes de IA que trabalham neste repositório.

## Visão Geral da Arquitetura

-   **Stack:** A aplicação é composta por um backend em Node.js/Express, um frontend simples em HTML/CSS/JS (`app/index.html`) e um banco de dados MongoDB.
-   **Containerização:** Todo o ambiente é projetado para ser executado com Docker e Docker Compose. O `compose.yaml` gerencia os serviços de banco de dados (`mongodb` e `mongo-express`), enquanto o `Dockerfile` constrói a imagem da aplicação Node.js. Existem também arquivos de compose específicos para ambientes, como `compose_homol.yaml` e `compose_prod.yaml`.
-   **Fluxo de Dados:** O frontend (`app/index.html`) faz chamadas de API para o backend (`app/server.js`) nos endpoints `/get-profile` e `/update-profile`. O backend, por sua vez, se conecta ao MongoDB para ler e escrever dados na coleção `users` do banco `my-db`.

## Fluxos de Trabalho Críticos

### Configuração do Ambiente

O fluxo de trabalho principal depende se a aplicação Node.js está rodando localmente ou dentro de um contêiner Docker. A principal diferença está na string de conexão com o MongoDB.

**Padrão Chave: Troca da String de Conexão**

O arquivo `app/server.js` contém duas variáveis para a URL do MongoDB:

-   `mongoUrlLocal`: Usada para executar o `server.js` diretamente na máquina local.
-   `mongoUrlDocker`: Usada quando a aplicação está rodando dentro de um contêiner Docker.

**Antes de executar ou construir, certifique-se de que a chamada `MongoClient.connect` está usando a variável correta para o seu ambiente.**

### Executando Localmente (App fora do Docker)

1.  Inicie o MongoDB e o Mongo Express: `docker-compose -f compose.yaml up`.
2.  **Ação Manual:** Acesse o Mongo Express em `http://localhost:8081` e crie manualmente o banco de dados `my-db` e a coleção `users`.
3.  Certifique-se de que `app/server.js` está usando `mongoUrlLocal`.
4.  Instale as dependências e inicie o servidor:
    ```bash
    npm --prefix ./app install
    npm --prefix ./app start
    ```

### Executando com Docker

1.  **Ação Manual:** Em `app/server.js`, comente a linha de conexão com `mongoUrlLocal` e descomente a linha com `mongoUrlDocker`.
2.  Construa a imagem da aplicação:
    ```bash
    docker build -t marceloicampos/app-docker-nodejs-mongo:homol .
    ```
3.  Inicie o ambiente completo usando o compose de homologação:
    ```bash
    docker-compose -f compose_homol.yaml up
    ```

## Convenções do Projeto

-   **ID de Usuário Fixo:** A lógica da aplicação está codificada para manipular apenas um perfil de usuário, identificado por `{ userid: 1 }`.
-   **Uso de `upsert`:** A operação de atualização de perfil (`/update-profile`) utiliza `{ upsert: true }`, o que significa que criará o documento do usuário se ele não existir.
-   **Arquivos de Compose por Ambiente:** Utilize `compose_homol.yaml` ou `compose_prod.yaml` para simular ambientes de teste ou produção, pois eles orquestram o contêiner da aplicação junto com o banco de dados.
