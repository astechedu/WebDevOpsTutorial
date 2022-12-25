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



args:

        - buildno
        - gitcommithash



cache_from:

    Added in version 3.2 file format

A list of images that the engine uses for cache resolution.

      build:
        context: .
        cache_from:
          - alpine:latest
          - corp/web_app:3.14



labels:

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


network:

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


shm_size:

    Added in version 3.5 file format

Set the size of the /dev/shm partition for this build’s containers. Specify as an integer value representing the number of bytes or as a string expressing a byte value.

      build:
        context: .
        shm_size: '2gb'

      build:
        context: .
        shm_size: 10000000



target:

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


cgroup_parent:

Specify an optional parent cgroup for the container.

        cgroup_parent: m-executor-abcd


command:

        Override the default command.

        command: bundle exec thin -p 3000

        The command can also be a list, in a manner similar to dockerfile:

        command: ["bundle", "exec", "thin", "-p", "3000"]



config: 


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



container_name:

Specify a custom container name, rather than a generated default name.

container_name: my-web-container








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
  
  
  
  

















