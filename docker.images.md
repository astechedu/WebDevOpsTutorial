$$\colorbox{24A0ED}{\large{\color{white}{Docker \ Images}}}$$


:link:[Home](all-file-links.md)     



<a name="top"></a>
Topic: 

  ***Docker Base Images***
  
  [MySql Base Image](#mysql_base_image)
      
  #
  ***PHP Image***
  
  [PHP Docker Images](#php_images)
    
  #
  ***Dockerfile Examples***
  
  [Dockerfile (run,env,label,WORKDIR)](#label_env_workdir_run)
  
  [Docker diff command](#docker_diff)
   
  [Docker Export, Import and .tar file](#docker_export)
   
  [Docker save/docker load ](#docker-save-load)
   
    
  
  
   
  
# 
  
***Running Docker Containers from docker images***


[Go To Top](#top)
<a name="mysql_base_image"></a>  


https://earthly.dev/blog/docker-mysql/

Only Commands: 



1 MySql 

Starting Your MySQL Container


      docker run --name mysql -d \
          -p 3306:3306 \
          -e MYSQL_ROOT_PASSWORD=change-me \
          --restart unless-stopped \
          mysql:8



You can do this at any time by using docker exec to get a shell inside the container:


      docker exec -it mysql mysql -p



Persisting Data With Volumes



Stop and remove your earlier container to avoid naming conflicts:


      docker stop mysql
      docker rm mysql


Then start a new container with the revised configuration:


        docker run --name mysql -d \
          -p 3306:3306 \
          -e MYSQL_ROOT_PASSWORD=change-me \
          -v mysql:/var/lib/mysql \
          mysql:8



         docker stop mysql
         docker rm mysql


Using Container Networks


First create a Docker network for your application:


      docker network create example-app


Specify this network when starting your MySQL container:


      docker run --name mysql -d \
          -e MYSQL_ROOT_PASSWORD=change-me \
          -v mysql:/var/lib/mysql \
          --network example-app \
          mysql:8


Connect another container to the same network:


      docker run --name api-server -d \
          -p 80:80 \
          --network example-app \
          example-api-server:latest



MySQL Configuration:

      -e
         MYSQL_DATABASE
         MYSQL_USER and MYSQL_PASSWORD
         MYSQL_RANDOM_ROOT_PASSWORD
         MYSQL_ROOT_PASSWORD
         MYSQL_ALLOW_EMPTY_PASSWORD
         MYSQL_ROOT_PASSWORD_FILE





Docker secrets or volumes to inject values as files.


      mkdir secrets
      echo "P@$$w0rd" > secrets/mysql-root-password

      docker run --name mysql -d \
          -p 3306:3306 \
          -e MYSQL_ROOT_PASSWORD_FILE=/run/secrets/mysql-root-password \
          -v ./secrets:/run/secrets \
          --restart unless-stopped \
          mysql:8



Creating a Custom Image

Here’s an example my.cnf that changes some MySQL settings:

      my.cnf[mysqld]
      innodb-ft-enable-stopword = 0
      innodb-ft-min-token-size = 1


Dockerfile

      FROM mysql:8
      COPY my.cnf /etc/mysql/conf.d/my.cnf

   
   
Build your image:

      docker build -t custom-mysql:latest .   
    
    
Now you can run your image to start a MySQL instance that automatically uses your config file:


      docker run --name custom-mysql -d \
          -p 3306:3306 \
          -e MYSQL_ROOT_PASSWORD=change-me \
          -v mysql:/var/lib/mysql \
          custom-mysql:latest    
    
      
  
#

[Go To Top](#top)
<a name="php_images"></a>  

# For PHP Frameworks Dockrfile

Dockerfile:

      FROM php:8.1.4-fpm

      RUN apt-get update && apt-get install -y \
          git \
          curl \
          zip \
          unzip

      RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
          chown -R www-data:www-data /var/www #It may be added
      WORKDIR /var/www



#

    FROM php:7.2-alpine3.8

    RUN apk update
    RUN apk add bash
    RUN apk add curl

    # INSTALL COMPOSER
    RUN curl -s https://getcomposer.org/installer | php
    RUN alias composer='php composer.phar'

    # INSTALL NGINX
    RUN apk add nginx
    
    
    
    FROM php:8.0.2-apache
    RUN apt-get update && apt-get upgrade -y
    RUN apt-get install -y mariadb-client libxml2-dev
    RUN apt-get autoremove -y && apt-get autoclean
    RUN docker-php-ext-install mysqli pdo pdo_mysql xml
    COPY --from=composer /usr/bin/composer /usr/bin/composer




#
    FROM php:7.3-fpm-alpine
    RUN docker-php-ext-install pdo pdo_mysql
    RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

    RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
    RUN apk update
    RUN apk upgrade
    RUN apk add bash
    RUN alias composer='php /usr/bin/composer'




#
How to install PHP composer inside a docker container: 

1. 
      FROM php:7.1.3-fpm

      RUN apt-get update && apt-get install -y libmcrypt-dev \
          mysql-client libmagickwand-dev --no-install-recommends \
          && pecl install imagick \
          && docker-php-ext-enable imagick \
      && docker-php-ext-install mcrypt pdo_mysql
      && chmod -R o+rw laravel-master/bootstrap laravel-master/storage




I try to work out a way to create a dev environment using docker and laravel.

I have the following dockerfile:

      FROM php:7.1.3-fpm

      RUN apt-get update && apt-get install -y libmcrypt-dev \
          mysql-client libmagickwand-dev --no-install-recommends \
          && pecl install imagick \
          && docker-php-ext-enable imagick \
      && docker-php-ext-install mcrypt pdo_mysql
      && chmod -R o+rw laravel-master/bootstrap laravel-master/storage





Laravel requires composer to call composer dump-autoload when working with database migration. Therefore, I need composer inside the docker container.
I tried:



      RUN curl -sS https://getcomposer.org/installer | php -- \
      --install-dir=/usr/bin --filename=composer




But when I call

      docker-compose up
      docker-compose exec app composer dump-autoload




In Dockerfile :

      COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer



#
     # Install Composer

      RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


      FROM php:7.1.3-fpm

      RUN apt-get update && apt-get install -y libmcrypt-dev \
          mysql-client libmagickwand-dev --no-install-recommends \
          && pecl install imagick \
          && docker-php-ext-enable imagick \
      && docker-php-ext-install mcrypt pdo_mysql





     # Install Composer

      RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer


It works for me, to test if the composer are installed i access to my container bash and execute:

      composer --version
      Composer version 1.6.5 2018-05-04 11:44:59






Dockerfile:


      #Get Composer
      FROM composer:2.0 as vendor

      WORKDIR /app

      COPY database/ database/
      COPY composer.json composer.json
      COPY composer.lock composer.lock

      RUN composer install \
          --no-interaction \
          --no-plugins \
          --no-scripts \
          --no-dev \
          --prefer-dist

      COPY . .
      RUN composer dump-autoload





Create an executable of your composer file using

      RUN curl -sS https://getcomposer.org/installer | php -- \
      --install-dir=/usr/bin --filename=composer && chmod +x /usr/bin/composer 






We have basicly the same command running with the difference,

       --install-dir=/usr/local/bin

Alternatively, you should add the composer bin files path to the $PATH variable.

       export PATH=$PATH":/usr/bin"








Another way:

Dockerfile:

        RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer




        FROM php:7.3-fpm-alpine
        RUN docker-php-ext-install pdo pdo_mysql
        RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

        RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
        RUN apk update
        RUN apk upgrade
        RUN apk add bash
        RUN alias composer='php /usr/bin/composer'







How to install PHP composer inside a docker container?

I'm trying to figure out how to set up a development environment with Docker and Laravel.


The following is my Dockerfile:

        FROM php:7.1.3-fpm

        RUN apt-get update && apt-get install -y libmcrypt-dev \
            mysql-client libmagickwand-dev --no-install-recommends \
            && pecl install imagick \
            && docker-php-ext-enable imagick \
        && docker-php-ext-install mcrypt pdo_mysql
        && chmod -R o+rw laravel-master/bootstrap laravel-master/storage



When working with database migration, Laravel requires composer to perform composer dump-autoload. As a result, composer is required inside the Docker container.

I tried this but:

        RUN curl -sS https://getcomposer.org/installer | php -- \
        --install-dir=/usr/bin --filename=composer



Later, when I call it

        docker-compose up
        docker-compose exec app composer dump-autoload


The following error is thrown:

rpc error: code = 13 desc = invalid header field value "oci runtime error: exec failed: container_linux.go:247: starting container process caused \"exec: \\\"composer\\\": executable file not found in $PATH\"\n"


I'd be grateful for any advise on how to add composer to the PATH in my dockerfile or what else I can do to get around this mistake.




# 
    FROM php:7-fpm
    WORKDIR /var/www
    RUN apt-get update && apt-get install -y libmcrypt-dev mysql-client && docker-php-ext-install mcrypt pdo_mysql
    ADD . /var/www
    RUN chown -R www-data:www-data /var/www




 #

    FROM php:fpm

    # Arguments defined in docker-compose.yml
    ARG user
    ARG uid

    # Install system dependencies
    RUN apt-get update && apt-get install -y libmcrypt-dev mysql-client

    # Install PHP extensions
    RUN docker-php-ext-install mcrypt pdo_mysql

    # Get latest Composer
    COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

    # Create system user to run Composer and Artisan Commands
    RUN useradd -G www-data,root -u $uid -d /home/$user $user
    RUN mkdir -p /home/$user/.composer && \
        chown -R $user:$user /home/$user

    # Set working directory
    WORKDIR /var/www

    # Set the user
    USER $user

    # Copy your files
    COPY . . # You can use "." as a destination since you already changed the workdir





<a name="label_env_workdir_run"></a>
# Dockeerfile env, run, label and Workdir


Dockerfile:

    FROM ubuntu:latest
    LABEL name="ajaysisaudiya"
    LABEL email="sample@gmail.com"
    ENV NAME ajaysisaudiya
    ENV PASS password


CMDS:
  
  docker build . -t myimage:1
  
  docker run myimage:1 -it bash
  
  roote@abcd3838# env




  
[Go To Top](#top)
<a name="docker_diff"></a>  
# Docker diff

    docker run --name server -p 8000:80 -d nginx:latest
    docker exec -it <containerId> /bin/bash

    <containerId># touch /tmp/ajay.html 

    docker diff <containerId>
    watch docker diff <containerId>


  
  
  
#
  
[Go To Top](#top)
<a name="docker_export"></a>  
# Docker export, immport and .tar file

    docker exec -it <containerId> /bin/bash

    <containerId># apt-get update
    <containerId># apt install git tree
     docker export <containerId> > my_ubuntu.tar
     docker export <containerId> -o my_ubuntu2.tar
     
    docker image import my_ubuntu.tar my_ubuntu_img
    ls -lh
    docker run -it my_ubuntu_img /bin/bash
  
  
#
[Go To Top](#top)
<a name="docker-save-load"></a>  
# Docker save / docker load 


    docker images
    docker image save logstash > logstash.tar
    ls
    docker image history logstash
    docker image rm logstash
    ls
    docker image load < logstash.tar
















  



:end:
