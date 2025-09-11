# app-docker-nodejs-mongo

### Demo app - developing with Docker, NodeJS and MongoDB

This demo app shows a simple user profile app set up using

-   index.html with pure js and css styles
-   nodejs backend with express module
-   mongodb for data storage
-   all components are docker-based

### With Docker Compose

#### To start the application

Step 1: go to main folder and start mongodb and mongo-express inside main folder with

    docker compose up

_Access the mongo-express under http://localhost:8081 from your browser login root password 123456_

Step 2: in mongo-express UI - create a new database "my-db"

Step 3: in mongo-express UI - create a new collection "users" in the database "my-db"

Step 4: go to /app folder install dependencies and start node server inside /app folder with

    npm install

and use the following command

    node server.js

or after npm install go to the main folder and use

    npm --prefix ./app start

Step 5: access the nodejs application from browser

_Access http://localhost:3000 from browser_

#### To build a docker image from the application

    	docker build -t marceloicampos/my-app:1.0 .

The dot "." at the end of the command denotes location of the Dockerfile

    	docker images ls
    	docker run --name my-app-1.0 -d marceloicampos/my-app:1.0
    	docker ps
    	docker ps -a
    	docker stop my-app-1.0
    	docker start my-app-1.0
    	docker logs my-app-1.0
    	docker exec -it my-app-1.0 /bin/sh
    	Linux cmd >>> "ls -lha /home/app"
    	Linux cmd >>> "exit"

Then Stop the Container. Note: run just one time, after do start and stop

    	docker stop my-app-1.0

#### To push a docker image to Docker Hub

create repository on Docker Hub "my-app" and

    	docker login
    	docker push marceloicampos/my-app:1.0

#### Credits

https://gitlab.com/nanuchi/techworld-js-docker-demo-app

ORDER

1. CONSTRUIR O APP
2. CONSTRUIR O AMBIENTE DE DEV COM DOCKER COMPOSE
3. SUBIR O APP COM SERVIÇOS DE FORMA LOCAL E CONECTAR O APP AOS SERVIÇOS DO DOCKER LOCAL
4. BUILD SOMENTE DO APP
5. SUBIR O BUILD DO APP PARA REPOSITÓRIO
6. CONSTRUIR AMBIENTE DE HOMOLOGAÇÃO COM DOCKER COMPOSE E APP EM REPOSITÓRIO
7. SUBIR O APP COM SERVIÇOS EM HOMOLOGAÇÃO E CONECTAR O APP AOS SERVIÇOS DO DOCKER EM HOMOLOGAÇÃO

docker-compose -f compose_homol.yaml up
