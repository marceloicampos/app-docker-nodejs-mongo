# app-docker-nodejs-mongo

### Demo app - developing with Docker, NodeJS and MongoDB

This demo app shows a simple user profile app set up using

-   HTML, pure JavaScript and CSS
-   NODEJS backend with express module
-   MONGODB for data storage
-   all components are docker-based

#### To start the application

Step 1: go to main folder /app-docker-nodejs-mongo and start mongodb and mongo-express inside main folder with

    docker-compose -f compose.yaml up

_Access the mongo-express under http://localhost:8081 from your browser login root password 123456_

Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"

Step 4: go to /app folder install and dependencies and start node server inside /app folder with

    npm install

and use the following command to start node server

    node server.js

or after npm install go to the main folder and use

    npm --prefix ./app start

Step 5: access the nodejs application from browser and try to update the profile with tests

_Access http://localhost:3000 from browser_

#### To stop the application

    CRTL + C (to stop server.js)
    docker-compose -f compose.yaml down (to stop compose)

#### To build a docker image from the application

    docker build -t marceloicampos/app-docker-nodejs-mongo .
	
The dot "." at the end of the command denotes location of the Dockerfile

#### To inspect image from build

    docker images ls
    docker run --name my-app_homol -d marceloicampos/app-docker-nodejs-mongo
    docker container ls
    docker container ls -a
    docker container stop my-app_homol
    docker container start my-app_homol
    docker container logs my-app_homol
    docker container exec -it my-app_homol /bin/sh
    linux cmd >>> "cat /home/app/index.html"
    linux cmd >>> "cat /home/app/server.js"
    linux cmd >>> "ls -lha /home/app"
    linux cmd >>> "exit"

Then Stop the Container. Note: 'run' just one time, after do 'start' and 'stop'

    docker container stop my-app_homol

#### To push a docker image to Docker Hub

create repository on Docker Hub "app-docker-nodejs-mongo" and

    docker login
    docker push marceloicampos/app-docker-nodejs-mongo

#### Test image marceloicampos/app-docker-nodejs-mongo with docker compose

    docker-compose -f compose_homol.yaml up
    docker-compose -f compose_homol.yaml down

#### Credits

https://gitlab.com/nanuchi/techworld-js-docker-demo-app

ORDER

1. CONSTRUIR O APP
2. CONSTRUIR O AMBIENTE DE DESENVOLVIMENTO COM DOCKER COMPOSE
3. SUBIR O APP COM SERVIÇOS DE FORMA LOCAL E CONECTAR O APP AOS SERVIÇOS DO DOCKER LOCAL
4. FAZER O BUILD SOMENTE DO APP
5. SUBIR O BUILD DO APP PARA REPOSITÓRIO
6. CONSTRUIR O AMBIENTE DE HOMOLOGAÇÃO COM DOCKER COMPOSE E APP EM REPOSITÓRIO
7. SUBIR O APP COM SERVIÇOS EM HOMOLOGAÇÃO E CONECTAR O APP AOS SERVIÇOS DO DOCKER EM HOMOLOGAÇÃO
