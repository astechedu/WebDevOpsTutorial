# Docker Images

<a name="top"></a>
Topic: 
  [PHP Docker Images](#php_images)
  
  
  
  
  
[Go To Top](#top)
<a name="php_images"></a>  

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






    FROM php:7.3-fpm-alpine
    RUN docker-php-ext-install pdo pdo_mysql
    RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli

    RUN php -r "readfile('http://getcomposer.org/installer');" | php -- --install-dir=/usr/bin/ --filename=composer
    RUN apk update
    RUN apk upgrade
    RUN apk add bash
    RUN alias composer='php /usr/bin/composer'





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









