# Dockerized Node Js Apps
:link:[Home](all-file-links.md)     





<a name="top"></a>
Topics: 

1. [Dockerizing a Node.js web app](#web-app)
2. [How To Dockerize an Vue App? (Worked)](#vuejs_app)
3. [How To Dockerize an React App? (Worked)](#react_app)
4. [How To Dockerize an Angular App? with Nginx (Worked)](#angular_app)
5. [How To Dockerize an Express Web App (Worked)](#express_app)



[Go To Top](#top)
<a name="vuejs_app"></a>
## 1.

#### Vuejs App 


#First creating app in local dir (Worked)
      
      npm init vue@latest
      

Dockerfile: 

      # Fetching the latest node (node:latest or node) image on alpine linux
      FROM node:18-alpine

      # install simple http server for serving static content
      RUN npm install -g http-server

      # make the 'app' folder the current working directory
      WORKDIR /app

      # copy both 'package.json' and 'package-lock.json' (if available)
      COPY package*.json ./

      # install project dependencies
      RUN npm install

      # copy project files and folders to the current working directory (i.e. 'app' folder)
      COPY . .

      # build app for production with minification
      RUN npm run build

      EXPOSE 8080
      CMD [ "http-server", "dist" ]




   #Creating image
   
   docker build -f Dockerfile -t dockervue . 

   
   
   #Dockerignore
   .dockerignore
   
   
      node_modules
      npm-debug.log
      build
      .git
      *.md
      .gitignore


#Run docker image docreact01
docker run --name dr -p8080:8080 -d dockervue



Pulling image from dockerhub:

      docker pull astechedu/sample-vue-app-image:latest



So access the application at the address http://localhost:8080/


:end:




===> End Vuejs App <======



----------------------------------------------------------



[Go To Top](#top)
<a name="react_app"></a>
## 2.

#### React App 

#First creating app in local dir (Worked)
      create-react-app appName

Dockerfile: 

      # Fetching the latest node (node:latest or node) image on alpine linux
      FROM node:18-alpine

      # Declaring env
      ENV NODE_ENV development

      # Setting up the work directory
      WORKDIR /react-app

      # Installing dependencies
      COPY ./package.json /react-app
      RUN npm install

      # Copying all the files in our project
      COPY . .

      # Starting our application
      CMD npm start



   #Creating image
   
   docker build -f Dockerfile -t dockerreact01 . 

   
   
   #Dockerignore
   .dockerignore
   
   
      node_modules
      npm-debug.log
      build
      .git
      *.md
      .gitignore


#Run docker image docreact01
docker run --name dr -p8080:3000 -d docreact01


Pulling image from dockerhub:

      docker pull astechedu/sample-react-app-image:latest




So access the application at the address http://localhost:8080/


:end:












===> End React App <======


----------------------------------------------------------




[Go To Top](#top)
<a name="angular_app"></a>
# 3

### How To Dockerize an Angular Application with Nginx

Contents:

    * Creating an Angular Application
    * Writing a Dockerfile
    * Running the Docker Container


Creating an Angular Application in dir:

      ng new sample-angular-app
      cd sample-angular-app
      ng serve
      

Dockerfile: 

            # Stage 1: Compile and Build angular codebase

            # Use official node image as the base image
            FROM node:latest as build

            # Set the working directory
            WORKDIR /usr/local/app

            # Add the source code to app
            COPY ./ /usr/local/app/

            # Install all the dependencies
            RUN npm install

            # Generate the build of the application
            RUN npm run build


            # Stage 2: Serve app with nginx server

            # Use official nginx image as the base image
            FROM nginx:latest

            # Copy the build output to replace the default nginx contents.
            COPY --from=build /usr/local/app/dist/dockerangular01 /usr/share/nginx/html

            # Expose port 80
            EXPOSE 80



Running the Docker Container: 

            docker build -t astechedu/sample-angular-app-image:latest  

            docker image ls



            docker run -d -p 8080:80 astechedu/sample-angular-app-image:latest
            docker ps

            docker login -u <username> -p <password>
            docker push astechedu/sample-angular-app-image:latest



Pulling image from dockerhub:

      docker pull astechedu/sample-angular-app-image:latest




     #Dockerignore:
     
               .dockerignore


                  node_modules
                  npm-debug.log
                  build
                  .git
                  *.md
                  .gitignore




So access the application at the address http://localhost:8080/

:end:





#
#
Examples: 


===> Vuejs App <==========

Dockerfile: 

            FROM node:lts-alpine

            #install simple http server for serving static content
            RUN npm install -g http-server

            #make the 'app' folder the current working directory
            WORKDIR /app

            #copy both 'package.json' and 'package-lock.json' (if available)
            COPY package*.json ./

            #install project dependencies
            RUN npm install

            #copy project files and folders to the current working directory (i.e. 'app' folder)
            COPY . .

            #build app for production with minification
            RUN npm run build

            EXPOSE 8080
            CMD [ "http-server", "dist" ]


            docker build -t vuejs-cookbook/dockerize-vuejs-app .


            docker run -it -p 8080:8080 --rm --name dockerize-vuejs-app-1 vuejs-cookbook/dockerize-vuejs-app

We should be able to access our Vue.js app on localhost:8080.


Let’s refactor our Dockerfile to use NGINX:


            #build stage
            FROM node:lts-alpine as build-stage
            WORKDIR /app
            COPY package*.json ./
            RUN npm install
            COPY . .
            RUN npm run build

            #production stage
            FROM nginx:stable-alpine as production-stage
            COPY --from=build-stage /app/dist /usr/share/nginx/html
            EXPOSE 80
            CMD ["nginx", "-g", "daemon off;"]


            docker build -t vuejs-cookbook/dockerize-vuejs-app .
            docker run -it -p 8080:80 --rm --name dockerize-vuejs-app-1 vuejs-cookbook/dockerize-vuejs-app


    Microservices
    DevOps
    Continuous Delivery


===> End Vuejs App <======

----------------------------------------------------------

===> React App <==========


// .dockerignore

            node_modules
            build


// Dockerfile

            #==== CONFIGURE =====
            #Use a Node 16 base image
            FROM node:16-alpine 
            #Set the working directory to /app inside the container
            WORKDIR /app
            #Copy app files
            COPY . .
            #==== BUILD =====
            #Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
            RUN npm ci 
            #Build the app
            RUN npm run build
            #==== RUN =======
            #Set the env to "production"
            ENV NODE_ENV production
            #Expose the port on which the app will be running (3000 is the default that `serve` uses)
            EXPOSE 3000
            #Start the app
            CMD [ "npx", "serve", "build" ]



            #Build the Docker image for the current folder 
            #and tag it with `dockerized-react`
            docker build . -t dockerized-react

            #Check the image was created
            docker images | grep dockerized-react

            #Run the image in detached mode 
            #and map port 3000 inside the container with 3000 on current host
            docker run -p 3000:3000 -d dockerized-react


http://localhost:3000


Save the app through nginx:

            nginx.conf

// nginx.conf


            server {
              listen 80;

              location / {
                root /usr/share/nginx/html/;
                include /etc/nginx/mime.types;
                try_files $uri $uri/ /index.html;
              }
            }


Dockerfile: 

            FROM node:16-alpine as builder
            #Set the working directory to /app inside the container
            WORKDIR /app
            #Copy app files
            COPY . .
            #Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
            RUN npm ci 
            #Build the app
            RUN npm run build

            #Bundle static assets with nginx
            FROM nginx:1.21.0-alpine as production
            ENV NODE_ENV production
            #Copy built assets from `builder` image
            COPY --from=builder /app/build /usr/share/nginx/html
            #Add your nginx.conf
            COPY nginx.conf /etc/nginx/conf.d/default.conf
            #Expose port
            EXPOSE 80
            #Start nginx
            CMD ["nginx", "-g", "daemon off;"]


            docker build . -t dockerized-react

            #Notice we're now mapping port 80 inside the container 
            #to port 3000 on the host machine!
            docker run -p 3000:80 -d dockerized-react


===> End React App <======


----------------------------------------------------------

===> Angualr App <==========

Project Setup

Install the Angular CLI globally:

            npm install -g @angular/cli@7.3.10
            ng new angular-microservice 
            cd angular-microservice
            ng new angular-microservice –directory ./


Docker Setup:

Dockerfile

            #base image
            FROM node:12.2.0

            #set working directory
            WORKDIR /app
            #install and cache app dependencies
            COPY package.json /app/package.json
            RUN npm install
            RUN npm install -g @angular/cli@7.3.10

            #add app
            COPY . /app

            #start app
            CMD ng serve --host 0.0.0.0


            docker build -t angular-microservice:dev .

            docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --rm angular-microservice:dev

            docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --name foo --rm angular-microservice:dev


===> End Angular App <======

#
:end:

#
Website: 
   https://dev.to/dronk6/getting-started-with-docker-docker-playground-28h3


---> What's in a Dockerfile?

//1. Creating Dockerfile

FROM node:12
WORKDIR /home/node/app
COPY package.json ./
RUN yarn install
COPY . .
CMD [ "yarn", "start" ]




//2. Creating Dockerfile

FROM node:10 AS ui-build
WORKDIR /usr/src/app
COPY my-app/ ./my-app/
RUN cd my-app && npm install && npm run build

FROM node:10 AS server-build
WORKDIR /root/
COPY --from=ui-build /usr/src/app/my-app/dist ./my-app/dist
COPY api/package*.json ./api/
RUN cd api && npm install
COPY api/server.js ./api/

EXPOSE 80

CMD ["node", "./api/server.js"]


#
:end:


#

**Build your Node image

#syntax=docker/dockerfile:1

      FROM node:18-alpine
      ENV NODE_ENV=production

      WORKDIR /app

      COPY ["package.json", "package-lock.json*", "./"]

      RUN npm install --production

      COPY . .

      CMD [ "node", "server.js" ]
      

:end: 
#


[Top](#top)
<a name="web-app"></a>
**Create simple node js server

Example: 01:


package.json 


      {
        "name": "docker_web_app",
        "version": "1.0.0",
        "description": "Node.js on Docker",
        "author": "First Last <first.last@example.com>",
        "main": "server.js",
        "scripts": {
          "start": "node server.js"
        },
        "dependencies": {
          "express": "^4.16.1"
        }
      }



server.js


      'use strict';

      const express = require('express');

      // Constants
      const PORT = 8080;
      const HOST = '0.0.0.0';

      // App
      const app = express();
      app.get('/', (req, res) => {
        res.send('Hello World');
      });

      app.listen(PORT, HOST, () => {
        console.log(`Running on http://${HOST}:${PORT}`);
      });



Dockerfile

      FROM node:16

      #Create app directory
      WORKDIR /usr/src/app

      #Install app dependencies
      #A wildcard is used to ensure both package.json AND package-lock.json are copied
      #where available (npm@5+)
      COPY package*.json ./

      RUN npm install
      #If you are building your code for production
      #RUN npm ci --only=production

      #Bundle app source
      COPY . .

      EXPOSE 8080
      CMD [ "node", "server.js" ]


.dockerignore

      node_modules
      npm-debug.log


Building your image:

      docker images
      docker build . -t <your username>/node-web-app

Run the image:

      docker run -p 49160:8080 -d <your username>/node-web-app


Print the output of your app:

       #Get container ID
       docker ps

       #Print app output
       docker logs <container id>

       #Example
       Running on http://localhost:8080


If you need to go inside the container you can use the exec command:

# Enter the container

        docker exec -it <container id> /bin/bash


Test: 

To test your app, get the port of your app that Docker mapped:

      docker ps

      curl -i localhost:49160


Shut down the image:


# Kill our running container

      docker kill <container id>
      
      <container id>

Confirm that the app has stopped
      
      curl -i localhost:49160
      
curl: (7) Failed to connect to localhost port 49160: Connection refused   
  
#
:end:

#

Example 02: 

Dockerfile: 

      FROM node:18.7.0
      RUN apt-get update && apt-get install -y \
        nano \
        Vim



docker-compose.yml:

      services:
       notes:
         build:
           context: .
         ports:
           - 8080:8080
           - 9229:9229
         environment:
           - SERVER_PORT=8080
           - DATABASE_CONNECTIONSTRING=mongodb://mongo:27017/notes
         volumes:
           - ./:/code
         command: npm run debug

       mongo:
         image: mongo:4.2.8
         ports:
           - 27017:27017
         volumes:
           - mongodb:/data/db
           - mongodb_config:/data/configdb
       volumes:
         mongodb:
         Mongodb_config:

#
:end:
