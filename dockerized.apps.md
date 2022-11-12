# Dockerized App For Beginners

>>>>>> Dockerize Apps <<<<<<<


### Topics: 

#### JS:     vuejs app, react app, angular app

#### PHP:    php app, laravel app, codeigniter app, cakephp app, symfony app,
      
   [Dockrized App PHP + MySql+ PHPMyAdmon Worked Click Here](#php_mysql_phpmyadmin)   
   

#### PYTHON: python app, django app, flask app

   Production:   
            [Dockrized App PHP-PFM NGINX Worked Click Here](#phpfpm_nginx)  


===> Vuejs App <==========

Dockerfile: 

      FROM node:lts-alpine

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


      docker build -t vuejs-cookbook/dockerize-vuejs-app .


      docker run -it -p 8080:8080 --rm --name dockerize-vuejs-app-1 vuejs-cookbook/dockerize-vuejs-app

      We should be able to access our Vue.js app on localhost:8080.


      Let’s refactor our Dockerfile to use NGINX:


# build stage
      FROM node:lts-alpine as build-stage
      WORKDIR /app
      COPY package*.json ./
      RUN npm install
      COPY . .
      RUN npm run build

# production stage
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

# ==== CONFIGURE =====
# Use a Node 16 base image
      FROM node:16-alpine 
# Set the working directory to /app inside the container
      WORKDIR /app
# Copy app files
      COPY . .
# ==== BUILD =====
# Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
      RUN npm ci 
# Build the app
      RUN npm run build
# ==== RUN =======
# Set the env to "production"
      ENV NODE_ENV production
# Expose the port on which the app will be running (3000 is the default that `serve` uses)
      EXPOSE 3000
# Start the app
      CMD [ "npx", "serve", "build" ]



# Build the Docker image for the current folder 
# and tag it with `dockerized-react`
      docker build . -t dockerized-react

# Check the image was created
      docker images | grep dockerized-react

# Run the image in detached mode 
# and map port 3000 inside the container with 3000 on current host
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
# Set the working directory to /app inside the container
      WORKDIR /app
# Copy app files
      COPY . .
# Install dependencies (npm ci makes sure the exact versions in the lockfile gets installed)
      RUN npm ci 
# Build the app
      RUN npm run build

# Bundle static assets with nginx
      FROM nginx:1.21.0-alpine as production
      ENV NODE_ENV production
# Copy built assets from `builder` image
      COPY --from=builder /app/build /usr/share/nginx/html
# Add your nginx.conf
      COPY nginx.conf /etc/nginx/conf.d/default.conf
# Expose port
      EXPOSE 80
# Start nginx
      CMD ["nginx", "-g", "daemon off;"]


      docker build . -t dockerized-react

# Notice we're now mapping port 80 inside the container 
# to port 3000 on the host machine!

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

# base image
      FROM node:12.2.0

# set working directory
      WORKDIR /app
# install and cache app dependencies
      COPY package.json /app/package.json
      RUN npm install
      RUN npm install -g @angular/cli@7.3.10

# add app
      COPY . /app

# start app
      CMD ng serve --host 0.0.0.0


      docker build -t angular-microservice:dev .

      docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --rm angular-microservice:dev

      docker run -d -v ${PWD}:/app -v /app/node_modules -p 4201:4200 --name foo --rm angular-microservice:dev


===> End Angular App <======

----------------------------------------------------------

===> PHP App <==========

<a name="#php_mysql_phpmyadmin">Top</a>   
# php mysql phpmyadmin                    

1. PHP + MYSQL + PHPMYADMIN    ( Worked )

Directory Structure: 

      myapp (dir) -> Dockerfile, docker-compose.yml, src(dir)->index.php

Dockerfile

      FROM php:8.0-apache
      WORKDIR /var/www/html
      RUN apt-get update -y && apt-get install -y libmariadb-dev
      RUN docker-php-ext-install mysqli 


      version: "3.7"
      services: 
        php-env:
           build: .
           volumes:
             - ./src:/var/www/html
           ports: 
             - 9000:80

        mysql_db: 
         image: mysql:latest 
         command: --default-authentication-plugin=mysql_native_password
         restart: always
         environment:
           MYSQL_ROOT_PASSWORD: root

        phpmyadmin:
          image: phpmyadmin:latest
          restart: always
          ports: 
           - 9001:80
          environment: 
           - PMA_ARBITRARY=1   
     
     
index.php

      $con = new mysqli("mysql_db","root","root")

      if($con){
        echo "Connected";
      }

http://localhost

//Run Commands

      docker-compose up -d       //Running all containers
      docker-compose down        //Stop and delete all containers


-----x------

2. 

Dockerfile:

FROM php:7.4-apache

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY start-apache /usr/local/bin
RUN a2enmod rewrite

# Copy application source

      COPY src /var/www/
      RUN chown -R www-data:www-data /var/www

      CMD ["start-apache"]



//# 000-default.conf

      <VirtualHost *:80>
        ServerAdmin webmaster@localhost
        DocumentRoot /var/www/public

        <Directory /var/www>
          Options Indexes FollowSymLinks
          AllowOverride All
          Require all granted
        </Directory>
      </VirtualHost>


      RUN apt-get update && \
          apt-get install nodejs

      ENV MYSQL_ROOT_PASSWORD=root
      ENV MYSQL_ROOT_USER=root

      docker build .

      docker tag SOURCE_IMAGE:TAG TARGET_IMAGE:TAG


The final docker-compose.yml looks like this:

      version: "3.9"
      services:
        webapp:
          build:
            context: .
            dockerfile: ./Dockerfile.development
          ports:
            - "8000:80"
          volumes:
            - ./src:/var/www
          environment:
            - APP_KEY=SomeRandomStringToAddSecurity123
            - APP_ENV=development
            - APP_DEBUG=true
            - APACHE_RUN_USER=apache-www-volume
            - APACHE_RUN_GROUP=apache-www-volume
            - UNSPLASH_ACCESS_KEY=${UNSPLASH_ACCESS_KEY}
            - UNSPLASH_SECRET_KEY=${UNSPLASH_SECRET_KEY}


# Dockerfile.development

      FROM php:7.4-apache

# Setup Apache2 config

      COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
      RUN a2enmod rewrite

      CMD ["apache2-foreground"]


      $ git add docker-compose.yml 000-default.conf Dockerfile* start-apache
      $ git commit -m "add docker and apache config"
      $ git push origin master


===> End PHP App <======

----------------------------------------------------------

===> Lavavel App <==========


# Dockerfile

      FROM php:5.5-apache

      RUN docker-php-ext-install pdo_mysql
      RUN a2enmod rewrite

      ADD . /var/www
      ADD ./public /var/www/html



      $ docker build -t laravel-app .
      $ docker run -p 80:80 laravel-app

docker-machine ip default

      $ docker run -p 80:80 -e DB_HOST=dbhost.com laravel-app


      FROM php:5.5-apache

      RUN docker-php-ext-install pdo_mysql
      RUN a2enmod rewrite

      ADD . /var/www
      ADD ./public /var/www/html

      ADD config/docker/apache.conf /etc/apache2/httpd.conf
      COPY config/docker/php.ini /usr/local/etc/php/


      $ docker build -t laravel-app .


# .dockerignore

      .git

      $ git add .dockerignore Dockerfile
      $ git commit -m ‘Dockerizing this great PHP app’



===> End Laravel App <======



----------------------------------------------------------

===> Codeigniter App <==========

      .database
      .docker
        |php
           |sites-available
             |site.conf
           |Dockerfile
        |custom.ini
        |docker-compose.yml
      .git
      app
        |app
        |public
        |tests
        |vendor
        |writable
        |.env
        |composer.json
        |composer.lock
        |spark
      .gitignore



      version: '3'
      services:
          web:
              container_name: ci4-web
              build:
                  context: ./php
              ports:
                  - 80:80
              volumes:
                  - ../app:/var/www/html/app/
                  - ./custom.ini:/usr/local/etc/php/conf.d/custom.ini
              links:
                  - mysql
              depends_on:
                - mysql
          mysql:
              container_name: db-ci4
              image: mysql:latest
              volumes:
                  - ./db:/var/lib/mysql
              command: --default-authentication-plugin=mysql_native_password
              ports:
                  - 3306:3306
              environment:
                  MYSQL_ROOT_PASSWORD: root



The Dockerfile

      FROM php:7.2-apache
      RUN apt-get update && \
          apt-get install -y
      RUN apt-get install -y curl
      RUN apt-get install -y build-essential libssl-dev zlib1g-dev libpng-dev libjpeg-dev libfreetype6-dev
      RUN apt-get install -y libicu-dev
      COPY sites-available/elioter.conf /etc/apache2/sites-enabled/elioter.conf
      RUN apt-get update
      RUN docker-php-ext-install intl
      RUN docker-php-ext-configure intl
      RUN docker-php-ext-install mysqli pdo pdo_mysql zip mbstring
      RUN a2enmod rewrite
      RUN docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/ \
          && docker-php-ext-install gd
      RUN service apache2 restart


my site.conf

      <VirtualHost *:80>
          DocumentRoot "/var/www/html/app/public/"
          ServerName ci4.local
          <Directory "/var/www/html/app/public/">
              AllowOverride all
          </Directory>
      </VirtualHost>

===> End Codeigniter App <======



----------------------------------------------------------

===> Cakephp App <==========

===> End Vuejs App <======



----------------------------------------------------------

===> Sysmfony App <==========

===> End Symfony App <======

----------------------------------------------------------

===> Python App <==========

===> End Python App <======

----------------------------------------------------------

===> Django App <==========

===> End Django App <======

----------------------------------------------------------

===> Flask App <==========

===> End Flask App <======

----------------------------------------------------------


====> PHPfpm and NGINX : Production  100% Working =====>


<a name="phpfpm_nginx"></a>    

# PHP-FPM NGINX 

//PHPFPM ajay nginx ( 100% Woring - Production)


//Directory Structure:

      myapp (project app) (dir)
       1 docker(dir) -> nginx(dir) -> Dockerfile, docker-compose.yml
       2 src (dir) -> public (dir) -> index.php


Dockerfile


      FROM php:8.0.2-fpm

      RUN apt-get update && apt-get install -y \
         git \
         curl \
         zip  \
         unzip 

      WORKDIR /var/www



      docker-composer.yml


      version: "3.8"
      services: 
        app: 
          build:
            context: ./
            dockerfile: Dockerfile
          container_name: my-app
          restart: always
          working_dir: /var/www/
          volumes: 
            - ../src:/var/www

        nginx: 
           image: nginx:1.19-alpine
           container_name: my-nginx
           restart: always
           ports: 
             - "8001:80"
           volumes: 
             - ../src:/var/www
             - ./nginx:/etc/nginx/conf.d




      server {

        listen 80;
        index index.php;
        error_log /var/log/nginx/error.log;
        access_log /var/log/nginx/acces.log;
        error_page 404 /index.php;
        root /var/www/public; 

        location ~ \.php$ {
            try_files $uri =404;
            fastcgi_pass app:9000;
            fastcgi_index index.php;
            include fastcgi_params;
            fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;      
        }
        location /.php$ {
           try_files $uri $uri/ /index.php?$query_string; 
           gzip_static on;
        }


      }

-----------------------------------------------------------