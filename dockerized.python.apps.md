# Dockerized Python
:link:[Home](all-file-links.md)     


<a name="top"></a>  
Topics: 

  1. [Dockrized Python](#doc_python)<br>
  2. [Dockrized Django (Worked)](#doc_django)<br>
  3. [Dockrized Flask](#doc_flash)<br>
  4. [Containerize a Python service](#python_flash)
  5. [Create a Simple Docker Container with a Python Web Server](#py-flask)
  6. [Dockerized Django App](#dj-app)
  7. [Dockerized MERN App](#mern-app)
  
#


[Go To Top](#top)
<a name="doc_python"></a>  







#

[Go To Top](#top)
<a name="doc_django"></a>  
# Django (Worked)

   Install Django in local dir: 
   
      pip install django
   
   
Add the following content to the Dockerfile.

        FROM python:3.8

        RUN apt-get update \
          && apt-get install -y --no-install-recommends \
            #postgresql-client \
          && rm -rf /var/lib/apt/lists/*

        WORKDIR /usr/src/app
        COPY requirements.txt ./
        RUN pip install -r requirements.txt
        COPY . .

        EXPOSE 8000
        CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


requirements.txt: 

      requiremasgiref==3.6.0
      backports.zoneinfo==0.2.1
      Django==4.1.4
      sqlparse==0.4.3
      ents.txt:


.dockerignore:

#Byte-compiled / optimized / DLL files

    __pycache__/

    **/migrations
    src/media
    src/db.sqlite3
    Procfile
    .git


#Building docker image:

    docker build . -t astechutube/sample-django-app

#Running Container:

    docker run --name django01 -p 8080:8000 -d astechutube/sample-django-app



#Pull this image from Docker Hub 

    docker pull astechutube/sample-django-app


So access the application at the address http://localhost:8080/


:end:






[Go To Top](#top)
<a name="doc_flash"></a>  


I don't like ignoring warnings, as one day you will oversee an important one.

Here is a good explanation on best docker practices with python. Search for Example with virtualenv and you'll find this:

# temp stage (Now Working)

      FROM python:3.9-slim as builder

      WORKDIR /app

      ENV PYTHONDONTWRITEBYTECODE 1
      ENV PYTHONUNBUFFERED 1

      RUN apt-get update && \
          apt-get install -y --no-install-recommends gcc

      RUN python -m venv /opt/venv
      ENV PATH="/opt/venv/bin:$PATH"

      COPY requirements.txt .
      RUN pip install -r requirements.txt


      # final stage
      FROM python:3.9-slim

      COPY --from=builder /opt/venv /opt/venv

      WORKDIR /app

      ENV PATH="/opt/venv/bin:$PATH"




[Top](#top)
<a name="python_flash"></a>
# Containerize a Python service


We have now the following structure:

    app
    ├─── requirements.txt
    └─── src
         └─── server.py

     
server.py

    from flask import Flask
    server = Flask(__name__)

    @server.route("/")
     def hello():
        return "Hello World!"

    if __name__ == "__main__":
       server.run(host='0.0.0.0') 


requirements.txt


Flask==1.1.1


Dockrfile: 


    #set base image (host OS)
    FROM python:3.8

    #set the working directory in the container
    WORKDIR /code

    #copy the dependencies file to the working directory
    COPY requirements.txt .

    #install dependencies
    RUN pip install -r requirements.txt

    #copy the content of the local src directory to the working directory
    COPY src/ .

    #command to run on container start
    CMD [ "python", "./server.py" ] 
    
    
    
Multi-stage builds:


    #first stage
    FROM python:3.8 AS builder
    COPY requirements.txt .

    #install dependencies to the local user directory (eg. /root/.local)
    RUN pip install --user -r requirements.txt

    #second unnamed stage
    FROM python:3.8-slim
    WORKDIR /code

    #copy only the dependencies installation from the 1st stage image
    COPY --from=builder /root/.local /root/.local
    COPY ./src .

    #update PATH environment variable
    ENV PATH=/root/.local:$PATH

    CMD [ "python", "./server.py" ]



CMD:

    docker images
    docker ps
    docker run -d -p 5000:5000 myimage
    
curl http://localhost:5000
    
   
#
:end:    
#


[Top](#py-flask)
<a name="py-flask"></a>

# Create a Simple Docker Container with a Python Web Server

Create index.html:

    <!DOCTYPE html>
    <html>
    <body>
    Hello World
    </body>
    </html>


Create server.py:


     #!/usr/bin/python3
     from http.server import BaseHTTPRequestHandler, HTTPServer
     import time
     import json
     from socketserver import ThreadingMixIn
     import threadinghostName = “0.0.0.0”
     serverPort = 80class Handler(BaseHTTPRequestHandler):
     def do_GET(self):
     #curl http://<ServerIP>/index.html
     if self.path == “/”:
     #Respond with the file contents.
     self.send_response(200)
     self.send_header(“Content-type”, “text/html”)
     self.end_headers()
     content = open(‘index.html’, ‘rb’).read()
     self.wfile.write(content)else:
     self.send_response(404)returnclass ThreadedHTTPServer(ThreadingMixIn, HTTPServer):
     “””Handle requests in a separate thread.”””if __name__ == “__main__”:
     webServer = ThreadedHTTPServer((hostName, serverPort), Handler)
     print(“Server started http://%s:%s" % (hostName, serverPort))try:
     webServer.serve_forever()
     except KeyboardInterrupt:
     passwebServer.server_close()
     print(“Server stopped.”)  
     ```


Put Everything into a Docker Container:

    Create Dockerfile:

        FROM python:3
        ADD index.html index.html
        ADD server.py server.py
        EXPOSE 8888
        ENTRYPOINT ["python3", "server.py"]
        cd into the folder you created.
        Run docker build -f Dockerfile . -t web-server-test
        Run docker run — rm -p 8000:80 — name web-server-test web-server-test

    
#
:end:
#

[Top](#top)
<a name="dj-app"></a>

# Dockerized Django App

Dockerfile

    FROM python:3.6-alpine
    ENV PYTHONDONTWRITEBYTECODE 1
    ENV PYTHONUNBUFFERED 1
    RUN mkdir /code
    WORKDIR /code
    RUN pip install --upgrade pip
    COPY requirements.txt /code/
    RUN pip install -r requirements.txt
    COPY . /code/
    EXPOSE 8000
    CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


Dockrfile: 


    FROM python:3
    #Here, we set the environmental variable that shows the output from python that is sent straight to the terminal without buffering it first.
      ENV PYTHONUNBUFFERED 1
    #Here, we set the container's working directory for this path to /app.
      WORKDIR /app
    #Here, we copy each file from our local project directory into the container.
      ADD ./app
    #Here, it runs the pip install command for all packages consolidated listed in the requirements.txt file.
      RUN pip install -r requirements.txt



docker-compose.yml


    version: '3.7'
    services:
       web:
           build: .
           command: python manage.py runserver localhost:8000
           ports:
               - 8000:8000





Dockrfile:


    FROM python:3.9-alpine
    WORKDIR /app
    #Set environment variables
    ENV PYTHONDONTWRITEBYECODE 1
    ENV PYTHONUNBUFFERED 1
    #Install psycopg2 dependencies
    RUN apk update \
        && apk add postgresql-dev gcc python3-dev musl-dev
    #Install dependencies
    COPY requirements.txt /app/requirements.txt
    RUN pip install --upgrade pip
    RUN pip install --no-cache-dir -r requirements.txt
    #Copy project
    COPY . .



#
:end:

#


[Top](#top)
<a name="mern-app"></a>

#Dockerized MERN APP

Dockerfile:


      #Dockerfile for React client
      #Build react client
      FROM node:10.16-alpine
      #Working directory be app
      WORKDIR /usr/src/app
      COPY package*.json ./
      ###  Installing dependencies
      RUN npm install --silent
      #Copy local files to app folder
      COPY . .
      EXPOSE 3000
      CMD ["npm","start"]


CMD: 

    docker build -t react-app .
    docker run -p 3000:3000 react-app
    
    
    
    #Dockerfile for Node Express Backend
    FROM node:10.16-alpine
    #Create App Directory
    RUN mkdir -p /usr/src/app
    WORKDIR /usr/src/app
    #Install Dependencies
    COPY package*.json ./
    RUN npm install --silent
    #Copy app source code
    COPY . .
    #Exports
    EXPOSE 5000
    CMD ["npm","start"]


docker build -t node-app .




docker-compose.yml


      version: '3.7'

      services:
        server:
          build:
            context: ./server
            dockerfile: Dockerfile
          image: myapp-server
          container_name: myapp-node-server
          command: /usr/src/app/node_modules/.bin/nodemon server.js
          volumes:
            - ./server/:/usr/src/app
            - /usr/src/app/node_modules
          ports:
            - "5000:5000"
          depends_on:
            - mongo
          env_file: ./server/.env
          environment:
            - NODE_ENV=development
          networks:
            - app-network
        mongo:
          image: mongo
          volumes:
            - data-volume:/data/db
          ports:
            - "27017:27017"
          networks:
            - app-network
        client:
          build:
            context: ./client
            dockerfile: Dockerfile
          image: myapp-client
          container_name: myapp-react-client
          command: npm start
          volumes:
            - ./client/:/usr/app
            - /usr/app/node_modules
          depends_on:
            - server
          ports:
            - "3000:3000"
          networks:
            - app-network

      networks:
          app-network:
              driver: bridge

      volumes:
          data-volume:
          node_modules:
          web-root:
            driver: local




Creating the Build:

To create the build for the entire application, we need to run the following 
command: docker-compose build


Starting the Services:

We can start the multi-container system using the following simple command: docker-compose up

At last, we can open http://localhost:3000 to see our React Frontend.

The backend server is live on http://localhost:5000

And MongoDB is running on http://localhost:27017







#
:end:
