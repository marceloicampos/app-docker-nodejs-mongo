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

    docker build -t my-app:1.0 .

The dot " . " at the end of the command denotes location of the Dockerfile
