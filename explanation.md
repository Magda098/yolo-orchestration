Instructions
Clone this repository git clone https://github.com/Magda098/yolo
Change in to yolo directory cd yolo
Run docker compose docker-compose up
You can pass -d to the above command if you want to run in detached mode
If you need to go inside a container run the following command docker exec -it <container id> /bin/bash

Run docker ps to get the container ID
To view container logs docker logs <container id>

Dockerfiles

FROM node:14-alpine -specifies Alpine base image to build the image from

WORKDIR /app - A working directory to hold application code

COPY package*.json ./ - Copy package.json and package-lock.json files containing project dependencies to the working directory inside the docker image

RUN npm install - Install project dependencies

COPY . /app/ - Copy project source code to the working directory inside the docker image

RUN npm run build - Compile project for production

EXPOSE 3000/4000 - Expose port 4000 for client and 3000 for backend

CMD ["node", "server.js"] or CMD [ "serve", "-s", "build", "-l", "3000" ] - Start the server

Docker-compose

This file (docker-compose.yaml) creates three containers

yolo_client - contains the yolo client service which runs on port 3000 ,re-tagged to yolo-client:v1.1.0 

yolo_backend - contains yolo backend service which runs on port 4000,retagged to yolo-backend:v1.1.0

mongo_db - contains mvertes/alpine-mongo db which runs on port 27017 and has an attached volume called /data/db \mvertes/alpine-mongo

Networks - All containers are in yolo bridge network
