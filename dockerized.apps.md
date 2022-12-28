# Dockerized App For Beginners
:link:[Home](all-file-links.md)     

<a name="top"></a>
### Topics: 

#### PHP:    php app, laravel app, codeigniter app, cakephp app, symfony app

   
1. [Dockrized App Laravel App Worked Click Here](#php_laravel)  
   
   [Dockrized App Composer Worked Click Here](#php_composer) 
   
   [Dockrized App PHP + MySql+ PHPMyAdmin Worked Click Here](#php_mysql_phpmyadmin)  
   
   [Dockrized App PHP + MySql+ Adminer Worked Click Here](#php_mysql_adminer)   

   [Dockerized Laravel & Symfony Apps Same Code Worked 100% Click Here](#php_laravel_symfony)   


  Production: 
  
            [Dockrized App PHP-PFM NGINX Worked Click Here](#phpfpm_nginx)  



------------------------------------------------------------------------------------




===> PHP App <==========

[Go To Top](#top)
## 1. 

<a name="php_laravel"></a>    
### Dockerized Laravel App  ( Worked )

#Install Laravel in local dir:

     composer create-project --prefer-dist laravel/laravel
     
     OR
     
     laravel new laravel02



  Dockerfile:
  
       FROM php:8.1-apache

        RUN apt update && apt install -y \
            git \
            curl \
            zip \
            unzip

       # RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer 


        WORKDIR /var/www/html
        COPY . .
        RUN chown -R www-data:www-data /var/www


docker-compose.yml: 

      version: "3"
      services: 
        web:
         build: 
          context: ./
          dockerfile: Dockerfile
         container_name: laravel01
         volumes: 
           - ./000-default.conf:/etc/apache2/sites-available/000-default.conf
         ports: 
          - 8080:80


  
  000-default.conf: 

        <VirtualHost *:80>
         ServerAdmin webmaster@localhost
         DocumentRoot /var/www/html/public
         #LogLevel info ssl:warn
         ErrorLog ${APACHE_LOG_DIR}/error.log
         CustomLog ${APACHE_LOG_DIR}/access.log combined
         # after it has been globally disabled with "a2disconf".
         #Include conf-available/serve-cgi-bin.conf
      </VirtualHost>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet


        docker-compose up -d 
        docker-compose down
        docker-compose stop
        docker-compose restart



  :computer:
  
  
  
  
  
  
  
  

[Go To Top](#top)
## 2. 

<a name="php_composer"></a>    
### Composer Installation  ( Worked )

  Dockerfile

      FROM php:7.3-fpm-alpine
      RUN docker-php-ext-install pdo pdo_mysql
      RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

      RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
      RUN apk update
      RUN apk upgrade
      RUN apk add bash
      RUN alias composer='php /usr/bin/composer'

       docker.compose.yml

      version: "3.3"
      services: 
        phpcomposer: 
          build: .
          volumes: 
            - .:/var/www
          working_dir: /var/www


  //Command run in docker container or in local host dir  
      docker run composer create-project symfony/symfony




[Go To Top](#top)
## 2.

<a name="phpfpm_nginx"></a>    
### PHP-FPM NGINX 

====> PHPfpm and NGINX : Production  100% Worked =====>

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


[Go To Top](#top)
##### 3. PHP + MYSQL + PHPMYADMIN    ( Worked )

<a name="php_mysql_phpmyadmin"></a>   
##### php mysql phpmyadmin                    


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

[Go To Top](#top)
<a name="php_mysql_adminer"></a>    
## 4. PHP + MYSQL + ADMINER   ( Worked )

   Directory Structure: 
   
      myapp(dir) --> docker-compose.yml, Dockerfile, src(dir) -> index.php   
   
Dockerfile

      FROM php:7.4-apache
      RUN docker-php-ext-install mysqli

docker-compose.yml

      version: "3.1"
      services: 
        php:
           build: .
             context: .
             dockerfile: Dockerfile
           ports:
             - 80:80
           volumes:
             - ./src:/var/www/html

        db: 
          image: mysql 
          command: --default-authentication-plugin=mysql_native_password
          restart: always
          environment:
            MYSQL_ROOT_PASSWORD: ajay123
          volumes:
            - mysql-data:/var/lib/mysql

        adminer:
          image: adminer
          restart: always
          ports: 
           - 8080:8080
      volumes: 
        mysql-data:   


  index.php:
  
           <?php

              echo "PHP + Mysql + Adminer";

           ?>

## 5. 

Dockerfile:

FROM php:7.4-apache

COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
COPY start-apache /usr/local/bin
RUN a2enmod rewrite

##### Copy application source

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


##### Dockerfile.development

      FROM php:7.4-apache

##### Setup Apache2 config

      COPY 000-default.conf /etc/apache2/sites-available/000-default.conf
      RUN a2enmod rewrite

      CMD ["apache2-foreground"]


      $ git add docker-compose.yml 000-default.conf Dockerfile* start-apache
      $ git commit -m "add docker and apache config"
      $ git push origin master


===> End PHP App <======

----------------------------------------------------------

===> Lavavel App <==========

[Go To Top](#top)
## 6.

##### Dockerfile

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


##### .dockerignore

      .git

      $ git add .dockerignore Dockerfile
      $ git commit -m ‘Dockerizing this great PHP app’



===> End Laravel App <======



----------------------------------------------------------

[Go To Top](#top)
##### 7. 

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

[Go To Top](#top)
<a name="php_laravel_symfony"></a>
===> Sysmfony App <==========



Dockerfile: 

        FROM 8.0-apache

        RUN apt-get update && apt-get install -y \
            git \
            curl \
            zip \
            unzip

        RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer \
            chown -R www-data:www-data /var/www
        WORKDIR /var/www



docker-compose.yml:


         version: "3"
           web: 
            build: 
              context: ./
              dockerfile: Dockerfile
             container_name: laravel03
             ports:
              - 8080:80




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
-----------------------------------------------------------
