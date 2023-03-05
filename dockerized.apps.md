# Dockerized App For Beginners
:link:[Home](all-file-links.md)     

<a name="top"></a>
### Topics: 

#### PHP:    php app, laravel app, codeigniter app, cakephp app, symfony app

   
1. [Dockrized App Laravel 9.x App Worked Click Here](#php_laravel)

2. [Dockrized App Symfony 6.x App Worked Click Here](#php_symfony)
   
3. [Dockrized App Composer Worked Click Here](#php_composer) 
   
4. [Dockrized App PHP + MySql+ PHPMyAdmin Worked Click Here](#php_mysql_phpmyadmin)  
   
5. [Dockrized App PHP + MySql+ Adminer Worked Click Here](#php_mysql_adminer)   

6. [Dockerized Laravel & Symfony Apps Same Code Worked 100% Click Here](#php_laravel_symfony)   
  
7. [Dockrized App PHP-PFM NGINX Worked Click Here](#phpfpm_nginx)  

8. [Dockrized App Laravel 9.x ](#php_laravel9x)

9. [Dockrized App PHP & NGINX (Working)](#nginx-php-app)



#


[Go To Top](#top)
<a name="php_laravel"></a>    
### 1. Dockerized Laravel App  ( Worked )

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
  


#
:end:



[Go To Top](#top)
<a name="php_symfony"></a>    
### 2. Dockerized Symfony App  ( Worked )

#Install Symfony in local dir:

     symfony new symfony01



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
         container_name: symfony01
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

#vim: syntax=apache ts=4 sw=4 sts=4 sr noet


        docker-compose up -d 
        docker-compose down
        docker-compose stop
        docker-compose restart



  :computer:





  
  
  #
 :end: 
  

[Go To Top](#top)
## 3. 

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


#
:end:


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




Note: 

  Send request to app (Service name or container name from container app or my-app
  fastcgi_pass app:9000;
  
#
:end:

#

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


#


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


#
:end:


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


:end:
#

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
      
#
:end:


#
[Top](#top)
<a name="nginx-php-app"></a>

*Dockerized Nginx and PHP Web App Testing (Working)


docker-compose.yml


	version: "3.5"
	services:
	  webserver:
	    image: nginx:latest
	    container_name: nginx-server
	    volumes:
	       - ./app/php/:/var/www/html/
	       - ./app/nginx/default.conf:/etc/nginx/conf.d/default.conf
	    ports:
	       - 8080:80
	  web:
	     image: php:fpm-alpine
	     container_name: webapp
	     volumes:
	       - ./app/php/:/var/www/html/




/etc/nginx/conf.d/default.conf


	server {
	    listen 80;
	    index index.php;
	    error_log /var/log/nginx/error.log;
	    access_log /var/log/nginx/acces.log;
	    error_page 404 /index.php;
	    root /var/www/html;

	    location ~ \.php$ {
		try_files $uri =404;
		fastcgi_pass webapp:9000;
		fastcgi_index index.php;
		include fastcgi_params;
		fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
	    }
	    location /.php$ {
	       try_files $uri $uri/ /index.php?$query_string;
	       gzip_static on;
	    }
	  }

Note: 

  Send request to webapp (Service name of container name) from container web or webapp
  fastcgi_pass webapp:9000;




:end:
#


===> Cakephp App <==========

===> End Vuejs App <======



#
:end:



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


#
:end:



#
[Go To Top](#top)
<a name="php_laravel9x"></a> 
***Dockerized Laravel 9 

php81

laravel9/

.docker/nginx/nginx.config
.docker/php/dockerfile
.docker/php/php.ini

docker-compose.yml


.docker/nginx/nginx.config


      server {
          listen 80;
          index index.php index.html;
          error_log  /var/log/nginx/error.log;
          access_log /var/log/nginx/access.log;
          root /var/www/public;

          location ~ \.php$ {
              try_files $uri =404;
              fastcgi_split_path_info ^(.+\.php)(/.+)$;
              fastcgi_pass backend:9000;
              fastcgi_index index.php;
              include fastcgi_params;
              fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
              fastcgi_param PATH_INFO $fastcgi_path_info;
          }

          location / {
              try_files $uri $uri/ /index.php?$query_string;
              gzip_static on;
          }
      }




Note: 

  Send request to backend (Container Name Or Service Name) from container backend
  fastcgi_pass backend:9000;
  
  

.docker/php/php.ini


      upload_max_filesize = 100M
      post_max_size = 108M


.docker/php/dockerfile


      FROM php:8.1-fpm

      ENV USER=www
      ENV GROUP=www

      # Install system dependencies
      RUN apt-get update && apt-get install -y \
          git \
          curl \
          libpng-dev \
          libonig-dev \
          libxml2-dev \
          zip \
          unzip

      # Clear cache
      RUN apt-get clean && rm -rf /var/lib/apt/lists/*

      # Install PHP extensions
      RUN docker-php-ext-install pdo_mysql mbstring exif pcntl bcmath gd

      # Install Postgre PDO
      RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo pdo_pgsql

      # Get latest Composer
      COPY --from=composer:latest /usr/bin/composer /usr/local/bin/composer

      # Setup working directory
      WORKDIR /var/www/

      # Create User and Group
      RUN groupadd -g 1000 ${GROUP} && useradd -u 1000 -ms /bin/bash -g ${GROUP} ${USER}

      # Grant Permissions
      RUN chown -R ${USER} /var/www

      # Select User
      USER ${USER}

      # Copy permission to selected user
      COPY --chown=${USER}:${GROUP} . .

      EXPOSE 9000

      CMD ["php-fpm"]



docker.compose.yml


      version: '3.8'

      networks:
        app-network:

      volumes:
        app-data:

      services:
        webserver:
          image: nginx:1.21.6-alpine
          container_name: webserver
          restart: unless-stopped
          ports:
            - "80:80"
          volumes:
            - ./:/var/www
            - .docker/nginx:/etc/nginx/conf.d
          networks:
            app-network:

        backend:
          build:
            context: .docker/php
            dockerfile: dockerfile
          container_name: backend
          volumes:
            - ./:/var/www
            - .docker/php/php.ini:/usr/local/etc/php/conf.d/local.ini
          networks:
            app-network:


#

:end:



#



====> PHPfpm and NGINX : Production  100% Working =====>



//PHPFPM ajay nginx ( 100% Woring - Production)


//Directries : 

myapp (project app) (dir)
 1 docker(dir) -> nginx(dir) -> Dockerfile, docker-compose.yml
 2 src (dir) -> public (dir) -> index.php
 
Directory Structure:




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


Send request to app (Service name or container name from container app
fastcgi_pass app:9000;





#
[Top](#top)
<a name="nginx-and-php"></a>

# Dockerized NGIN and PHP (Working)


docker-compose.yml


		version: "3.5"
		services:
		  nginx:
		    image: nginx
		    volumes:
			- ./app:/var/www/html
			- ./nginx/default.conf:/etc/nginx/conf.d/default.conf
		    ports:
		      - "8080:80"
		  php:
		    image: php:fpm-alpine
		    volumes:
			- ./app:/var/www/html



/etc/nginx/conf.d/default.conf


		server {
		    listen 0.0.0.0:80;
		    root /var/www/html;
		    location / {
			index index.php index.html;
		    }
		    location ~ \.php$ {
			include fastcgi_params;
			fastcgi_pass php:9000;
			fastcgi_index index.php;
			fastcgi_param SCRIPT_FILENAME $document_root/$fastcgi_script_name;
		    }
		}




:end:

#

# PHP MySql and Network
//When both containers in same network, No need any link between them

Mysql Container: 

docker create network mynetwork --driver bridge
docker network ls
docker inspect network mynetwork

Dockerfile:  myproject/Dockerfile

FROM php:8.0-apache
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN apt-get update && apt-get upgrade -y


Creating MySql Container: 
docker run --name mydb -e MYSQL_ALLOW_EMPTY_PASSWORD=true -v mysql:/var/lib/mysql -p 3306:3306 -d --network mynetwork  mysql:latest


PHP Container: 
docker run --name myserver --network mynetwork -p 8000:80 -v "$PWD"/src:/var/www/html -d server01




myproject/src/index.php


      <?php
      //These are the defined authentication environment in the db service

      // The MySQL service named in the docker-compose.yml.
      $host = 'db';

      // Database use name
      $user = 'MYSQL_USER';

      //database user password
      $pass = 'MYSQL_PASSWORD';

      // check the MySQL connection status
      $conn = new mysqli($host, $user, $pass);
      if ($conn->connect_error) {
          die("Connection failed: " . $conn->connect_error);
      } else {
          echo "Connected to MySQL server successfully!";
      }
      ?>

#
:end:

#

<<<< More Examples >>>>


>>>> Docker PHP, Mysql & Apache <<<<

Website:   Good site

 https://www.section.io/engineering-education/dockerized-php-apache-and-mysql-container-development-environment/



version: '3.8'
services:
    php-apache-environment:
        container_name: php-apache
        build:
            context: ./php
            dockerfile: Dockerfile
        depends_on:
            - db
        volumes:
            - ./php/src:/var/www/html/
        ports:
            - 8000:80
    db:
        container_name: db
        image: mysql
        restart: always
        environment:
            MYSQL_ROOT_PASSWORD: MYSQL_ROOT_PASSWORD
            MYSQL_DATABASE: MYSQL_DATABASE
            MYSQL_USER: MYSQL_USER
            MYSQL_PASSWORD: MYSQL_PASSWORD
        ports:
            - "9906:3306"


Dockerfile 


FROM php:8.0-apache
RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
RUN apt-get update && apt-get upgrade -y


phpmyadmin:
    image: phpmyadmin/phpmyadmin
    ports:
        - '8080:80'
    restart: always
    environment:
        PMA_HOST: db
    depends_on:
        - db
        
---------------------------------------------------


>>> Docker-Compose <<<<

*) Dockerfile

FROM: php:7.4-apache


*) docker-compose.yml file

version: "3"
services: 
 web:
  build: . 
  volumes: 
   - ./src:/var/www/html
  ports:
   - 80:80

db: 
 image: mysql
 volumes: 
  -  ./db_data:/var/lib/mysql
 environment: 
  MYSQL_ROOT_PASSWORD:12345
  MYSQL_DATABASE: docker_d
 ports: 
  - 3306:3306




----------------------------------------------------




>>>> Docker php:7.4-apache <<<<


Image Name: php:7.4-apache

docker-compose.yml  (file)

version: "3"
services: 
 web
  image: php:7.4-apache
  container_name: php
  ports: 
   - "80:80"
  volumes: 
   - ~/html:/var/www/html




-------------------------------------------------------
-------------------------------------------------------

>>>>> nginx + php <<<<<<

//Working

myproject (dir)
1. nginx (dir) -> Dockerfile, default.conf
2. php (dir)   -> Dockerfile,
3. www/html (dir) -> index.php

nginx: Dockerfile
       FROM nginx:latest   
       COPY ./default.conf /etc/nginx/conf.d/default.conf

php: Dockerfile
     FROM php:7.0-fpm  
     RUN docker-php-ext-install pdo_mysql

version: "3"
services:
 nginx:
  build: ./nginx/
  container_name: nginx-container
  ports:
   - 80:80
  links:
   - php
  volumes:
   - ./www/html/:/var/www/html/

 php:
  image: php:7.0-fpm
  container_name: php-container
  expose:
   – 9000
  volumes:
   – ./www/html/:/var/www/html/


-------------------------------------------------------
-------------------------------------------------------

>>> nginx + php <<<<<<


    nginx:    
      build: ./nginx/  
      container_name: nginx-container  
      ports:  
       - 80:80  
      links:  
       - php  
      volumes_from:  
       - app-data  

    php:    
      image: php:7.0-fpm  
      container_name: php-container  
      expose:  
       - 9000  
      volumes_from:  
       - app-data  

    app-data:    
      image: php:7.0-fpm  
      container_name: app-data-container  
      volumes:  
       - ./www/html/:/var/www/html/  
      command: "true"

----------------------------------------------------------


>>>> nginx + php + myql <<<<<<<<<<


     nginx:    
      build: ./nginx/  
      container_name: nginx-container  
      ports:  
       - 80:80  
      links:  
       - php  
      volumes_from:  
       - app-data  

     php:    
      build: ./php/  
      container_name: php-container  
      expose:  
       - 9000  
      links:  
       - mysql  
      volumes_from:  
       - app-data  

     app-data:    
      image: php:7.0-fpm  
      container_name: app-data-container  
      volumes:  
       - ./www/html/:/var/www/html/  
      command: "true"  

     mysql:    
      image: mysql:5.7  
      container_name: mysql-container  
      volumes_from:  
       - mysql-data  
      environment:  
       MYSQL_ROOT_PASSWORD: secret  
       MYSQL_DATABASE: mydb  
       MYSQL_USER: myuser  
       MYSQL_PASSWORD: password  

     mysql-data:    
      image: mysql:5.7  
      container_name: mysql-data-container  
      volumes:  
       - /var/lib/mysql  
      command: "true" 
      


#
Next Example: 

//docker-compose.yml file


version: '3.1'

srvices:
	php:
     build:
       dockerfile: Dockerfile        //Dockerfile Given below
	 ports: 
	   - 80:80
	 volume:
	   - ./src:/var/www/html
	
	db:
      image: mysql 
      command: -default-authentication-plugin=mysql_native_password
      restart: always
      environment:
        MYSQL_ROOT_PASSWORD: example





//Above included

Dockerfile

 FROM php:7.4-apache
 RUN docker-php-eat-install mysqli
 COPY ./src:/var/www/html



:end:

#





>>>> Application ( Nginx, PHP, MySql ) <<<<<<<<<<<<<<<<<<<

Website: 
    https://www.atlantic.net/vps-hosting/how-to-deploy-a-php-application-with-nginx-and-mysql-using-docker-and-docker-compose/



How to Deploy a PHP Application with Nginx and 
MySQL Using Docker and Docker Compose: 


Step 1 – Create Atlantic.Net Cloud Server: 

apt-get update -y

Step 2 – Install Docker and Docker Compose: 

 apt-get install apt-transport-https ca-certificates curl tree software-properties-common -y


curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

apt-get install docker-ce docker-compose -y


Step 3 – Directory Structure: 

/root/docker-project/
├── docker-compose.yml
├── nginx
│   ├── default.conf
│   └── Dockerfile
├── php
│   └── Dockerfile
└── www
    └── html
        └── index.php


Step 4 – Create an Nginx Container: 

mkdir ~/docker-project


cd ~/docker-project
nano docker-compose.yml


Add the following lines:

     nginx:   
      image: nginx:latest  
      container_name: nginx-container  
      ports:   
       - 80:80 


docker-compose up -d
docker ps


Now, open your web browser and access your Nginx container using the URL http://your-server-ip.

On Browser displaying

Welcome to nginx        //Output on browser



Step 5 – Create a PHP Container: 


mkdir -p ~/docker-project/www/html
nano ~/docker-project/www/html/index.php


//Add the following lines:

     <!DOCTYPE html>  
     <head>  
      <title>Hello World!</title>
     </head>  

     <body>  
      <h1>Hello World!</h1>
      <p><?php echo 'We are running PHP, version: ' . phpversion(); ?></p>
     </body>


mkdir ~/docker-project/nginx

nano ~/docker-project/nginx/default.conf



---- Nginx Config ---> 

Add the following lines:

server {  

     listen 80 default_server;  
     root /var/www/html;  
     index index.html index.php;  

     charset utf-8;  

     location / {  
      try_files $uri $uri/ /index.php?$query_string;  
     }  

     location = /favicon.ico { access_log off; log_not_found off; }  
     location = /robots.txt { access_log off; log_not_found off; }  

     access_log off;  
     error_log /var/log/nginx/error.log error;  

     sendfile off;  

     client_max_body_size 100m;  

     location ~ .php$ {  
      fastcgi_split_path_info ^(.+.php)(/.+)$;  
      fastcgi_pass php:9000;  
      fastcgi_index index.php;  
      include fastcgi_params;  
      fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;  
      fastcgi_intercept_errors off;  
      fastcgi_buffer_size 16k;  
      fastcgi_buffers 4 16k;  
    }  

     location ~ /.ht {  
      deny all;  
     }  
    } 


 Send request to php (Service name or container name from container php
 fastcgi_pass php:9000;

-- Nginx Config ------>


nano ~/docker-project/nginx/Dockerfile




Add the following lines:

    FROM nginx:latest   
    COPY ./default.conf /etc/nginx/conf.d/default.conf 


Next, edit the docker-compose.yml file:

nano ~/docker-project/docker-compose.yml



Remove the old contents and add the following contents:

---
nginx:
build: ./nginx/
container_name: nginx-container
ports:
- 80:80
links:
- php
volumes:
- ./www/html/:/var/www/html/


php:
image: php:7.0-fpm
container_name: php-container
expose:
– 9000
volumes:
– ./www/html/:/var/www/html/


cd ~/docker-project
docker-compose up -d

docker ps


Now, open your web browser and access the URL http://your-server-ip. You should see your Hello World page:


nano ~/docker-project/www/html/index.php


Change the line “Hello World! Changes are Applied”:

     <!DOCTYPE html>  
     <head>  
      <title>Hello World!</title>
     </head>  

     <body>  
      <h1>Hello World! Changes are Applied</h1>
      <p><?php echo 'We are running PHP, version: ' . phpversion(); ?></p>
     </body>


//Now, refresh your web page. 


:end:

#


Docker Laravel:

//How to create laravel development environment using docker


you should have a total of 6 services (containers) running on your machine, one for each specific need of our application, here is the full list:


    PHP 8.0 (application code)
    MySQL 5.7 (database)
    NGINX (webserver)
    phpMyAdmin (database managment)
    Redis (caching)
    MailHog (local email testing)


Also here is the link to the official Docker website with installations instructions.

https://www.docker.com/products/docker-desktop

//Step 1: Clone Laravel's git repository
git clone https://github.com/laravel/laravel.git src


Now, create a couple of files and folders we need to setup and organize our docker environment. Create two files at the root of the project, one called docker-compose.yaml and another called Dockerfile. Then create the following list of folder/subfolder.

    nginx/conf
    mysql/data
    redis/data


//Step 2: Create a custom PHP 8 image


But, according to Laravel's documentation (https://laravel.com/docs/8.x/deployment#server-requirements), there a list of PHP extensions (listed below) the framework version we will use (8.x) needs installed to properly work:


    BCMath PHP Extension
    Ctype PHP Extension
    Fileinfo PHP Extension
    JSON PHP Extension
    Mbstring PHP Extension
    OpenSSL PHP Extension
    PDO PHP Extension
    Tokenizer PHP Extension
    XML PHP Extension


To know which extensions a given PHP installation has available we just need to run the following command, php -m, after I executed it inside the PHP image we will be using (I already pulled it to my machine) and I got the following list of installed extensions.


	docker run php:8.0.3-fpm-buster php -m

[PHP Modules]
Core
ctype
curl
date
dom
fileinfo
filter
ftp
hash
iconv
json
libxml
mbstring
mysqlnd
openssl
pcre
PDO
pdo_sqlite
Phar
posix
readline
Reflection
session
SimpleXML
sodium
SPL
sqlite3
standard
tokenizer
xml
xmlreader
xmlwriter
zlib

[Zend Modules]


Comparing it with the list of extensions required by Laravel we can see we are missing only a single extension and since we will be using MySQL, we will also need to install the pdo_mysql.




To create a custom image we will need to write some code to the Dockerfile we created earlier, the code we need is below.


FROM php:8.0.3-fpm-buster

RUN docker-php-ext-install bcmath pdo_mysql

RUN apt-get update
RUN apt-get install -y git zip unzip

COPY --from=composer:latest /usr/bin/composer /usr/bin/composer

EXPOSE 9000


//Step 3: Setup the basic services (PHP, NGINX and MySQL)


Let's start defining docker setup and you will see how simple it actually is.

version: "3.7"

networks:
    app-network:
        driver: bridge

services:
    app:
        
    
    mysql:
        
    
    nginx:
        


//3.2 App (custom PHP) service

app:
        build: 
            context: ./
            dockerfile: Dockerfile
        image: laravel8-php-fpm-80
        container_name: app
        restart: unless-stopped
        tty: true
        working_dir: /var/www
        volumes: 
            - ./src:/var/www
        networks: 
            - app-network



//3.3 NGINX service


This container will be a standard NGINX container and will have the following set of configurations.

    nginx:
        image: nginx:1.19.8-alpine
        container_name: nginx
        restart: unless-stopped
        tty: true
        ports: 
            - 8100:80
        volumes: 
            - ./src:/var/www
            - ./nginx/conf:/etc/nginx/conf.d
        networks: 
            - app-network



//It's content will be the following.

server {
    listen 80;
    index index.php index.html;
    error_log /var/log/nginx/error.log;
    access_log /var/log/nginx/access.log;
    root /var/www/public;
    location ~ \.php$ {
        try_files $uri =404;
        fastcgi_split_path_info ^(.+\.php)(/.+)$;
        fastcgi_pass app:9000;
        fastcgi_index index.php;
        include fastcgi_params;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        fastcgi_param PATH_INFO $fastcgi_path_info;
    }
    location / {
        try_files $uri $uri/ /index.php?$query_string;
        gzip_static on;
    }
}


 Send request to app (Service name or container name from container app
 fastcgi_pass app:9000;
  

//3.4 MySQL service

//I will call that database laravel8, but you can call it whatever you want.



 mysql:
        image: mysql:5.7.33
        container_name: mysql
        restart: unless-stopped
        tty: true
        environment: 
            MYSQL_DATABASE: laravel8
            MYSQL_ROOT_PASSWORD: 123456
            MYSQL_PASSWORD: 123456
            MYSQL_USER: laravel8
            SERVICE_TAGS: dev
            SERVICE_NAME: mysql
        volumes: 
            - ./mysql/data:/var/lib/mysql
        networks:
            - app-network



//In laravel env

DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel8
DB_USERNAME=laravel8
DB_PASSWORD=123456


//The first version of our docker-compose.yaml file will look like this.


version: "3.7"

networks:
    app-network:
        driver: bridge

services:
    app:
        build: 
            context: ./
            dockerfile: Dockerfile
        image: laravel8-php-fpm-80
        container_name: app
        restart: unless-stopped
        tty: true
        working_dir: /var/www
        volumes: 
            - ./src:/var/www
        networks: 
            - app-network
    
    mysql:
        image: mysql:5.7.33
        container_name: mysql
        restart: unless-stopped
        tty: true
        environment: 
            MYSQL_DATABASE: laravel8
            MYSQL_ROOT_PASSWORD: 123456
            MYSQL_PASSWORD: 123456
            MYSQL_USER: laravel8
            SERVICE_TAGS: dev
            SERVICE_NAME: mysql
        volumes: 
            - ./mysql/data:/var/lib/mysql
        networks:
            - app-network
    
    nginx:
        image: nginx:1.19.8-alpine
        container_name: nginx
        restart: unless-stopped
        tty: true
        ports: 
            - 8100:80
        volumes: 
            - ./src:/var/www
            - ./nginx/conf:/etc/nginx/conf.d
        networks: 
            - app-network


//Step 4: Test our initial setup

docker-compose up



//4.1 Accessing the homepage



docker-compose [OPTIONS] exec [SERVICE NAME] [COMMAND]

//So to install our dependencies will execute.

docker-compose exec -T app composer install




docker-compose exec -T app cp .env.example .env
docker-compose exec -T app php artisan key:generate



//Now Laravel welcome page is displaying on the breowser


4.2 Running migrations


DB_CONNECTION=mysql
DB_HOST=mysql
DB_PORT=3306
DB_DATABASE=laravel8
DB_USERNAME=laravel8
DB_PASSWORD=123456


docker-compose exec -T app php artisan config:clear
docker-compose exec -T app php artisan migrate

//4.3 Installing additional composer packages

docker-compose exec -T app composer require laravel/socialite


//Step 5: Setup additional services (Redis, phpMyAdmin and MailHog)


//5.1 Adding Redis (caching)


redis:
        image: redis:6.2.1-buster
        container_name: redis
        restart: unless-stopped
        tty: true
        volumes: 
            - ./redis/data:/data
        networks: 
            - app-network


docker-compose exec -T app composer require predis/predis


CACHE_DRIVER=redis
REDIS_HOST=redis
REDIS_CLIENT=predis

docker-compose exec -T app php artisan config:clear



//web.php

use Illuminate\Support\Facades\Redis;

Route::get('/store', function() {
    Redis::set('foo', 'bar');
});

Route::get('/retrieve', function() {
    return Redis::get('foo');
});



docker-compose down
docker-compose up

After hitting the /store route we should see nothing on the screen since we are just storin our key value pair and returning nothing, but after hitting the /retrieve route we should see on the screen the value we stored for the foo key, which is bar. 


//5.2 Adding MailHog (local mail testing)


mailhog:
        image: mailhog/mailhog:v1.0.1
        container_name: mailhog
        restart: unless-stopped
        ports: 
            - 8025:8025
        networks: 
            - app-network



MAIL_FROM_ADDRESS=isaac@isaacsouza.dev



docker-compose exec -T app php artisan config:clear


docker-compose exec -T app php artisan make:mail TestMail



//It will create a file called TestMail.php inside the app/Mail folder and in it we will the following //line of code to its build method.

/**
 * Build the message.
 *
 * @return $this
 */
public function build()
{
    return $this->view('mail.test');
}




// resources/views/email/test.blade.php

testing mailhog



//web.php

<?php

use App\Mail\TestMail;
use Illuminate\Support\Facades\Mail;

Route::get('/send-email', function() {
    Mail::to('isaac@isaacsouza.dev')->send(new TestMail);
});



docker-compose down
docker-compose up


5.3 Adding phpMyAdmin (MySQL managment)


phpmyadmin:
        image: phpmyadmin:5.1.0-apache
        container_name: phpmyadmin
        restart: unless-stopped
        ports: 
            - 8200:80
        environment:
            PMA_HOST: mysql
            PMA_PORT: 3306
            PMA_USER: laravel8
            PMA_PASSWORD: 123456
        networks:
            - app-network


docker-compose down
docker-compose up

#
:end:

#

>>>>> Docker Run PHP Scirpt in Container <<<<<<


//Working in docker plyagound
//Create index.php in root where you are right now

docker run --rm --name corephp -v "$PWD":/usr/src/yapp -w /usr/src/yapp php:7.1-cli php index.php

//PHP file in app folder

docker run --rm --name corephp -v "$PWD":/usr/src/yapp -w /usr/src/yapp php:7.1-cli php ./app/index.php

:end:



