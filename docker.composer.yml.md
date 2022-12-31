# Docker Composer Yaml File
:link:[Home](all-file-links.md) 

<a name="top"></a>
Topics: 

   [Build in Dockerfile](#build); [Dockerfile](#dockerfile); [args](#args); [cache_from](#cache_from)'; [Labels](#labels); [Shm_size](#shm_size)<br>
   [Config](#config); [Command](#command); [Target](#target); [Network](#depends_on); [container Name](#container_name); [Depends On](#depends_on);
   [Deploy](#deploy); [Endpoint Mode](#endpoint_mode)



Tested Containers: 

[Create mysql cotainer](#mysql); [Create postgre cotainer](#postgre); [Create mongo cotainer](#mongo); [Create redis cotainer](#redis);
[Create php cotainer](#php); [Create phpmyadmin cotainer](#phpmyadmin); [Create adminer cotainer](#adminer);
[Create php_mysql cotainer](#php_mysql); [Create php_mysql_adminer cotainer](#php_mysql_adminer); [Create php_mysql_phpmyadmin cotainer](#php_mysql_phpmyadmin); [Create mongo cotainer](#mongo); [Create mysql cotainer](#mysql); [Create postgre cotainer](#postgre);
[Create postgreSQL & adminer cotainer](#postgre); [Create mongo & mongo-express cotainer](#postgre);

[Create mongo & mongo-express cotainer](#postgre); [Create php mysql & phpmyadmin  cotainer](#postgre); [Create php and mysql cotainer](#postgre);
[Create phpmyadmin & mysql cotainer](#postgre); [Create Mysql with adminer cotainer](#postgre); 









 
 




[Got To Top](#top)
<a name="build"></a>
# Docker Compose Version 3.9



# Build:

Configuration options that are applied at build time.

build can be specified either as a string containing a path to the build context:

  version: "3.9"
  services:
    webapp:
      build: ./dir


Or, as an object with the path specified under context and optionally Dockerfile and args:

    version: "3.9"
    services:
      webapp:
        build:
          context: ./dir
          dockerfile: Dockerfile-alternate
          args:
            buildno: 1


If you specify image as well as build, then Compose names the built image with the webapp and optional tag specified in image:

      build: ./dir
      image: webapp:tag


context:

Either a path to a directory containing a Dockerfile, or a url to a git repository.

      build:
        context: ./dir



[Got To Top](#top)
<a name="dockerfile"></a>
# dockerfile

Alternate Dockerfile.

Compose uses an alternate file to build with. A build path must also be specified.

      build:
        context: .
        dockerfile: Dockerfile-alternate


[Got To Top](#top)
<a name="args"></a>
# args

Add build arguments, which are environment variables accessible only during the build process.

First, specify the arguments in your Dockerfile:

# syntax=docker/dockerfile:1

      ARG buildno
      ARG gitcommithash

      RUN echo "Build number: $buildno"
      RUN echo "Based on commit: $gitcommithash"

Then specify the arguments under the build key. You can pass a mapping or a list:

      build:
        context: .
        args:
          buildno: 1
          gitcommithash: cdc3b19

      build:
        context: .
        args:
          - buildno=1
          - gitcommithash=cdc3b19



args:

        - buildno
        - gitcommithash



[Got To Top](#top)
<a name="cache_from"></a>
# cache_from

    Added in version 3.2 file format

A list of images that the engine uses for cache resolution.

      build:
        context: .
        cache_from:
          - alpine:latest
          - corp/web_app:3.14



[Got To Top](#top)
<a name="labels"></a>
# labels

    Added in version 3.3 file format

Add metadata to the resulting image using Docker labels. You can use either an array or a dictionary.

It’s recommended that you use reverse-DNS notation to prevent your labels from conflicting with those used by other software.

      build:
        context: .
        labels:
          com.example.description: "Accounting webapp"
          com.example.department: "Finance"
          com.example.label-with-empty-value: ""

      build:
        context: .
        labels:
          - "com.example.description=Accounting webapp"
          - "com.example.department=Finance"
          - "com.example.label-with-empty-value"


[Got To Top](#top)
<a name="network"></a>

# network:

    Added in version 3.4 file format

Set the network containers connect to for the RUN instructions during build.

        build:
          context: .
          network: host

        build:
          context: .
          network: custom_network_1

        Use none to disable networking during build:

        build:
          context: .
          network: none


[Got To Top](#top)
<a name="shm_size"></a>
# shm_size:

    Added in version 3.5 file format

Set the size of the /dev/shm partition for this build’s containers. Specify as an integer value representing the number of bytes or as a string expressing a byte value.

      build:
        context: .
        shm_size: '2gb'

      build:
        context: .
        shm_size: 10000000


[Got To Top](#top)
<a name="target"></a>
# target

    Added in version 3.4 file format

Build the specified stage as defined inside the Dockerfile. See the multi-stage build docs for details.

      build:
        context: .
        target: prod

      cap_add, cap_drop

Add or drop container capabilities. See man 7 capabilities for a full list.

      cap_add:
        - ALL

      cap_drop:
        - NET_ADMIN
        - SYS_ADMIN


# cgroup_parent

Specify an optional parent cgroup for the container.

        cgroup_parent: m-executor-abcd



[Got To Top](#top)
<a name="command"></a>
# command

        Override the default command.

        command: bundle exec thin -p 3000

        The command can also be a list, in a manner similar to dockerfile:

        command: ["bundle", "exec", "thin", "-p", "3000"]


[Got To Top](#top)
<a name="config"></a>
# config


    Added in version 3.3 file format.

    config definitions are only supported in version 3.3 and higher of the compose file format.

        version: "3.9"
        services:
          redis:
            image: redis:latest
            deploy:
              replicas: 1
            configs:
              - my_config
              - my_other_config
        configs:
          my_config:
            file: ./my_config.txt
          my_other_config:
            external: true


# Long syntax (target etc.)

      version: "3.9"
      services:
        redis:
          image: redis:latest
          deploy:
            replicas: 1
          configs:
            - source: my_config
              target: /redis_config
              uid: '103'
              gid: '103'
              mode: 0440
      configs:
        my_config:
          file: ./my_config.txt
        my_other_config:
          external: true


[Got To Top](#top)
<a name="container_name"></a>
# container_name:

    Specify a custom container name, rather than a generated default name.

    container_name: my-web-container



[Got To Top](#top)
<a name="depends_on"></a>
# depends_on: 

    version: "3.9"
    services:
      web:
        build: .
        depends_on:
          - db
          - redis
      redis:
        image: redis
      db:
        image: postgres



[Got To Top](#top)
<a name="deploy"></a>
# deploy

    Added in version 3 file format.

Specify configuration related to the deployment and running of services. The following
sub-options only takes effect when deploying to a swarm with docker stack deploy, and is ignored by docker-compose up and docker-compose run, except for resources.

      version: "3.9"
      services:
        redis:
          image: redis:alpine
          deploy:
            replicas: 6
            placement:
              max_replicas_per_node: 1
            update_config:
              parallelism: 2
              delay: 10s
            restart_policy:
              condition: on-failure



[Got To Top](#top)
<a name="endpoint_mode"></a>
# endpoint_mode


      version: "3.9"

      services:
        wordpress:
          image: wordpress
          ports:
            - "8080:80"
          networks:
            - overlay
          deploy:
            mode: replicated
            replicas: 2
            endpoint_mode: vip

        mysql:
          image: mysql
          volumes:
             - db-data:/var/lib/mysql/data
          networks:
             - overlay
          deploy:
            mode: replicated
            replicas: 2
            endpoint_mode: dnsrr

      volumes:
        db-data:

      networks:
        overlay:



# labels

    version: "3.9"
    services:
      web:
        image: web
        deploy:
          labels:
            com.example.description: "This label will appear on the web service"




      version: "3.9"
      services:
        web:
          image: web
          labels:
            com.example.description: "This label will appear on all containers for the web service"

















version: '2'
services:
  db:
    image: mysql:5.7
    ports:
      - "6603:3306"
    environment:
      - MYSQL_ALLOW_EMPTY_PASSWORD=true
      - MYSQL_DATABASE=laravelProject
      - LANG=C.UTF-8
    volumes:
      - db:/var/lib/mysql
    command: mysqld --sql-mode=NO_ENGINE_SUBSTITUTION --character-set-server=utf8 --collation-server=utf8_unicode_ci

  web:
    image: arbiedev/php-nginx:7.1.8
    ports:
      - "8080:80"
    volumes:
      - ./www:/var/www
      - ./nginx.conf:/etc/nginx/sites-enabled/default

volumes:
  db:






2.

    web:
      build: path/to/your/Dockerfile/directory
      image: your-image-tag
      ports:
        - "8080:80"
      volumes:
        - ./www:/var/www
        - ./nginx.conf:/etc/nginx/sites-enabled/default


3.











4.

version: "3.9"
services:

  redis:
    image: redis:alpine
    ports:
      - "6379"
    networks:
      - frontend
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure

  db:
    image: postgres:9.4
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - backend
    deploy:
      placement:
        max_replicas_per_node: 1
        constraints:
          - "node.role==manager"

  vote:
    image: dockersamples/examplevotingapp_vote:before
    ports:
      - "5000:80"
    networks:
      - frontend
    depends_on:
      - redis
    deploy:
      replicas: 2
      update_config:
        parallelism: 2
      restart_policy:
        condition: on-failure

  result:
    image: dockersamples/examplevotingapp_result:before
    ports:
      - "5001:80"
    networks:
      - backend
    depends_on:
      - db
    deploy:
      replicas: 1
      update_config:
        parallelism: 2
        delay: 10s
      restart_policy:
        condition: on-failure

  worker:
    image: dockersamples/examplevotingapp_worker
    networks:
      - frontend
      - backend
    deploy:
      mode: replicated
      replicas: 1
      labels: [APP=VOTING]
      restart_policy:
        condition: on-failure
        delay: 10s
        max_attempts: 3
        window: 120s
      placement:
        constraints:
          - "node.role==manager"

  visualizer:
    image: dockersamples/visualizer:stable
    ports:
      - "8080:8080"
    stop_grace_period: 1m30s
    volumes:
      - "/var/run/docker.sock:/var/run/docker.sock"
    deploy:
      placement:
        constraints:
          - "node.role==manager"

networks:
  frontend:
  backend:

volumes:
  db-data:
  
  
  
  



# Docker Compose Yml (Tested Containers)


#### 1. Create mysql container

docker-compose.yml: 

      <code>
       services:
         db: 
          image: mysql:latest
          container_name: mydb
          restart: always
          environment: 
            MYSQL_ROOT_PASSWORD: ajay123
      </dode>


#### 2. Create postgre container

docker-compose.yml: 
     
        <code>
        postgre:
          image: postgres
          restart: always
          environment:
            POSTGRES_USER: ajay
            POSTGRES_PASSWORD: ajay123
         </code>


#### 3. Create mongo container

docker-compose.yml: 

      <code>
      #Use root/example as user/password credentials
      version: '3.1'
      services:
        mongo:
          image: mongo:4
          restart: always
          environment:
            MONGO_INITDB_ROOT_USERNAME: root
            MONGO_INITDB_ROOT_PASSWORD: example
        </code>
        

#### 4. Create redis container

docker-compose.yml: 

#### 5. Create php container

docker-compose.yml: 

Dockerfile: 

       <code>
        FROM php:8.0-apache
        RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
        RUN apt-get update && apt-get upgrade -y
       </code>


  docker-compose.yml

      <code>
        version: "3.5"
        services:
          web: 
            build: 
             context: ./
             dockerfile: Dockerfile
            container_name: phpserver
            depends_on: 
               - db
            volumes: 
               - ./php/src:/var/www/html
            ports: 
               - 8000:80      
         </code>

index.php:


   <code>
    <?php
    echo "php and mysql";

    $servername = "db";
    $username = "root";
    $password = "example";

    // Create connection
    $conn = new mysqli($servername, $username, $password);

    // Check connection
    if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
    }
    $conn->query('create database ajay');
    echo "Connected successfully";

    ?>
   </code>




#### 6. Create adminer container

docker-compose.yml: 


      <code>
      #Use postgres/example user/password credentials
      version: '3.1'
      services: 
        adminer:
          image: adminer
          restart: always
          ports:
            - 8080:8080
        </code>




#### 7. Create phpmyadmin container


docker-compose.yml: 

         <code>
           version: "3"
           services:
             phpmyadmin:
              image: phpmyadmin
              restart: always
              environment: 
                - PMA_HOST:db
              ports:
                - 8080:80
           </code>





 

[Got To Top](#top)
<a name="mysql"></a>
#### 8. Mysql with adminer:


Directory Structure:

 project/Dockerfile
 project/docker-compose.yml
 project/php/src/index.php




docker-compose.yml: 


      <code>
       services:
         db: 
          image: mysql:latest
          container_name: mydb
          restart: always
          environment: 
            MYSQL_ROOT_PASSWORD: ajay123


         adminer:
          image: adminer
          restart: always
          ports:
            - 8080:8080
      </dode>

 
 
      docker-compose up -d
      docker-compose down

      docker exex -it mydb bash

      abcd# mysql -u root -p
         password: ajay123

        mysql> .......

 
 
 

 
 [Got To Top](#top)
 <a name="phpmyadmin"></a>
  ### 9. phpmyadmin & mysql (Worked)
  
  Directory Structure:

   project/Dockerfile
   project/docker-compose.yml
   project/php/src/index.php



   docker-compose.yml: 
    
    
         <code>
           version: "3"
           services:
             db: 
              image: mysql:latest
              container_name: mydb
              restart: always
              environment: 
                MYSQL_ROOT_PASSWORD: example


             phpmyadmin:
              image: phpmyadmin
              restart: always
              environment: 
                - PMA_HOST:db
              ports:
                - 8080:80
           </code>


      docker-compose up -d
      docker-compose down 






[Got To Top](#top)
  <a name="php"></a>
  ### 10. php and mysql (worked)
  
  Directory Structure:

   project/Dockerfile
   project/docker-compose.yml
   project/php/src/index.php

  
      <code>
      version: "3.5"
      services:
        db: 
         image: mysql:latest
         container_name: mydb
         restart: always
         environment: 
           MYSQL_ROOT_PASSWORD: example
         ports: 
          - 3306:3306

        web: 
          build: 
           context: ./
           dockerfile: Dockerfile
          container_name: phpserver
          depends_on: 
             - db
          volumes: 
             - ./php/src:/var/www/html
          ports: 
             - 8000:80
        </code>



//Dir
php/src/index.php:

      <code>
      <?php
      echo "php and mysql";

      $servername = "db";
      $username = "root";
      $password = "example";

      // Create connection
      $conn = new mysqli($servername, $username, $password);

      // Check connection
      if ($conn->connect_error) {
        die("Connection failed: " . $conn->connect_error);
      }
      echo "Connected successfully";

      ?>
      </code>
      

      docker=compose up -d
      docker-compose down
      docker-compose restart





[Got To Top](#top)
<a name="php_mysql_phpmyadmin"></a>
### 11. php mysql & phpmyadmin 

  Directory Structure:

   project/Dockerfile
   project/docker-compose.yml
   project/php/src/index.php




Dockerfile: 

       <code>
        FROM php:8.0-apache
        RUN docker-php-ext-install mysqli && docker-php-ext-enable mysqli
        RUN apt-get update && apt-get upgrade -y
       </code>


  docker-compose.yml

      <code>
        version: "3.5"
        services:
          db: 
           image: mysql:latest
           container_name: mydb
           restart: always
           environment: 
             MYSQL_ROOT_PASSWORD: example
           ports: 
            - 3306:3306

          web: 
            build: 
             context: ./
             dockerfile: Dockerfile
            container_name: phpserver
            depends_on: 
               - db
            volumes: 
               - ./php/src:/var/www/html
            ports: 
               - 8000:80

          phpmyadmin: 
               image: phpmyadmin
               container_name: phpmyadmin
               environment: 
                  PMA_HOST: db
               ports: 
                 - 8080:80
         </code>


index.php:


   <code>
    <?php
    echo "php and mysql";

    $servername = "db";
    $username = "root";
    $password = "example";

    // Create connection
    $conn = new mysqli($servername, $username, $password);

    // Check connection
    if ($conn->connect_error) {
      die("Connection failed: " . $conn->connect_error);
    }
    $conn->query('create database ajay');
    echo "Connected successfully";

    ?>
   </code>

   docker=compose up -d
   docker-compose down
   docker-compose restart




[Got To Top](#top)
<a name="postgre"></a>
### 12. postgreSQL & adminer

Dockerfile:

No



docker-compose.yml:

      <code>
      #Use postgres/example user/password credentials
      version: '3.1'

      services:
        postgre:
          image: postgres
          restart: always
          environment:
            POSTGRES_USER: ajay
            POSTGRES_PASSWORD: ajay123

        adminer:
          image: adminer
          restart: always
          ports:
            - 8080:8080
        </code>


 
      docker=compose up -d
      docker-compose down
      docker-compose restart




[Got To Top](#top)
<a name="mongo"></a>
### 13. mongo & mongo-express 

      <code>
      #Use root/example as user/password credentials
      version: '3.1'
      services:
        mongo:
          image: mongo:4
          restart: always
          environment:
            MONGO_INITDB_ROOT_USERNAME: root
            MONGO_INITDB_ROOT_PASSWORD: example

        mongo-express:
          image: mongo-express
          restart: always
         # depends_on:
          #  - mongo
          ports:
            - 8081:8081
          environment:
            ME_CONFIG_MONGODB_ADMINUSERNAME: root
            ME_CONFIG_MONGODB_ADMINPASSWORD: example
            ME_CONFIG_MONGODB_URL: mongodb://root:example@mongo:27017/
        </code>

 
         docker=compose up -d
         docker-compose down
         docker-compose restart





:end:

