# Dockerized Node Js Apps
:link:[Home](all-file-links.md)     





<a name="top"></a>
Topics: 

1. [Dockerized Vue App](#vuejs_app)
2. [Dockerized React App Worked](#react_app)
3. [How To Dockerize an Angular Application with Nginx Worked](#angular_app)
4. [Dockerized Express Web App Worked](#express_app)







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

:end:



















===> End React App <======


----------------------------------------------------------




[Go To Top](#top)
<a name="angular_app"></a>
# 3
# How To Dockerize an Angular Application with Nginx

##### ===> Angualr App <==========

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


:end:



