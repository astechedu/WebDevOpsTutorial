# Docker Composer Yaml File





Docker Compose Version 3.9


build:

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



dockerfile:

Alternate Dockerfile.

Compose uses an alternate file to build with. A build path must also be specified.

      build:
        context: .
        dockerfile: Dockerfile-alternate


args: 

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
  
  
  
  

















