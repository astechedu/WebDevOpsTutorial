# Servers On Linux



<a name="top"></a>
Topics: 

[Nginx Mulit Domains on ubuntu 20.04](#nginx_multi_domains)
[Nginx Reverse Proxxy Stream](#nginx_reverse_proxxy)










# Nginx Multi domains
#Nginx Mulit Domains on ubuntu 20.04

How to Host Multiple Domains With Nginx Ubuntu Web Server


1. Create A record on DNS records that points to your server.



2. Log into your server via SSH.


        ssh root@your_server_ip



3. Update apt and install nginx.


        sudo apt update
        sudo apt install nginx



    
4. Enable firewall.

Check firewall status.


        sudo ufw status

        root@ultimateakash:~# sudo ufw status
    
    
 Status: inactive



If firewall's status is inactive, activate it by hitting the below command.


        sudo ufw enable

        root@ultimateakash:~# sudo ufw enable
    
  
Firewall is active and enabled on system startup



5. Update ufw application profiles.

List the ufw application profiles.


         sudo ufw app list

         root@ultimateakash:~# sudo ufw app list



Available applications:


      Nginx Full
      Nginx HTTP
      Nginx HTTPS
      OpenSSH


        sudo ufw allow OpenSSH


  Check ufw status.
  
    
            sudo ufw status

          root@ultimateakash:~# sudo ufw status
    
    
    
  Status: active


To                         Action      From
--                         ------      ----
Nginx Full                 ALLOW       Anywhere
OpenSSH                    ALLOW       Anywhere
Nginx Full (v6)            ALLOW       Anywhere (v6)
OpenSSH (v6)               ALLOW       Anywhere (v6)




6. Check nginx status


        sudo systemctl status nginx


Open your domain/server IP in the browser. You will see the default nginx installation page(/var/www/html/index.nginx-debian.html ).
Nginx has one server block enabled by default that is configured to serve documents from the /var/www/html directory.  


7. Setup Server Blocks.

Create the directory for your domains.


        sudo mkdir /var/www/example1.com

        sudo mkdir /var/www/example2.com



Assign ownership of the directory with the $USER environment variable.


        sudo chown -R $USER:$USER /var/www/example1.com

        sudo chown -R $USER:$USER /var/www/example2.com



    Grant 775 permission to www directory.

         sudo chmod -R 755 /var/www



Create a sample index.html for example1.com


         sudo nano /var/www/example1.com/index.html


  <html>
      <head>
          <title>example1.com</title>
      </head>
      <body>
          <h1>Welcome to example1.com</h1>
      </body>
  </html>



Create a sample index.html for example2.com

        sudo nano /var/www/example2.com/index.html



  <html>
      <head>
          <title>example2.com</title>
      </head>
      <body>
          <h1>Welcome to example2.com</h1>
      </body>
  </html>


press ctrl + x and press y then hit enter.

Create a config file for example1.com.


         sudo nano /etc/nginx/sites-available/example1.com


    server {
        listen 80;
        listen [::]:80;

        root /var/www/example1.com;
        index index.html index.htm index.nginx-debian.html;

        server_name example1.com www.example1.com;

        location / {
            try_files $uri $uri/ =404;
        }
    }



press ctrl + x and press y then hit enter.

Create a config file for example2.com.


         sudo nano /etc/nginx/sites-available/example2.com


    server {
        listen 80;
        listen [::]:80;

        root /var/www/example2.com;
        index index.html index.htm index.nginx-debian.html;

        server_name example2.com www.example2.com;

        location / {
            try_files $uri $uri/ =404;
        }
    }



These two lines


              root /var/www/your_domain;
              server_name your_domain www.your_domain;




press ctrl + x and press y then hit enter.

Enable this new configuration by creating a link from it to the sites-enabled directory.


         sudo ln -s /etc/nginx/sites-available/example1.com /etc/nginx/sites-enabled/

        sudo ln -s /etc/nginx/sites-available/example2.com /etc/nginx/sites-enabled/


Uncomment bucket size.

        sudo nano /etc/nginx/nginx.conf


Find server_names_hash_bucket_size directive and remove the # symbol to uncomment the line.


    http {

            ##
            # Basic Settings
            ##

            sendfile on;
            tcp_nopush on;
            tcp_nodelay on;
            keepalive_timeout 65;
            types_hash_max_size 2048;
            # server_tokens off;

            server_names_hash_bucket_size 64;



Test configuration.

        sudo nginx -t



         root@ultimateakash:~# sudo nginx -t
    
    
    nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
    nginx: configuration file /etc/nginx/nginx.conf test is successful



Reload nginx to implement the changes.

        sudo systemctl reload nginx



8. Next, open your domains in the browser. you will see our sample index.html

     http://example1.com

     http://example2.com


9. Install SSL certificates.

Install Certbot


        sudo apt install certbot python3-certbot-nginx



Obtaining SSL certificates.


        sudo certbot --nginx -d example1.com -d www.example1.com -d example2.com -d www.example2.com



you can pass multiple domains with -d option. you can even use wildcards.


      -d *.example1.com



After hitting the above command you need to pass your email also you need to provide a few answers.

Checkout the sample below.


         https://example1.com

         https://example2.com


Let’s Encrypt’s certificates are only valid for 90 days. but don't worry certbot takes care of renewals.

Check certbot's renewal service status.


        sudo systemctl status certbot.timer



    Install SSL on Nginx
    Let's Encrypt on Ubuntu
    Let's Encrypt on Nginx
    Install Nginx on Ubuntu
    Host Multiple Domains on Ubuntu




:end: 





# Reverse Proxy



Docker compose : NGINX reverse proxy with multiple containers
Docker_Icon.png




Bookmark and Share




bogotobogo.com site search:





Introduction

A reverse proxy is a server that sits between internal applications and external clients, forwarding client requests to the appropriate server. Because NGINX has a number of advanced load balancing, security, and acceleration features that most specialized applications lack, using NGINX as a reverse proxy enables us to add these features to any application.

In this post, we'll setup a reverse proxy with NGINX, and will setup two applications (one on NGINX and another on apache).

nginx-reverse-proxy-pic.png




Dockerfile - building a reverse proxy image

Here is the Dockerfile which will be used to create the reverse proxy image. It will use the nginx.conf after copying it to the proxy container:

FROM nginx:alpine
 
COPY nginx.conf /etc/nginx/nginx.conf


We're using nginx 1.19.3. To check the version, we can add the following to the Dockerfile because the alpine docker image doesn't have bash installed by default:

RUN apk update && apk add bash


Then, check its version:

$ docker build -t nginx-alpine .
$ docker run -t -i nginx-alpine /bin/bash
bash-4.4# nginx -v
nginx version: nginx/1.19.3


Once it's done, we may want to remove the line we've just added since it will increase the size of the image.

Let's build reverse proxy image:

$ docker build -t reverseproxy .
Sending build context to Docker daemon  64.51kB
Step 1/3 : FROM nginx:alpine
 ---> 4efb29ff172a
Step 2/3 : COPY nginx.conf /etc/nginx/nginx.conf
 ---> Using cache
 ---> 845ad907e486
Step 3/3 : RUN apk update && apk add bash
 ---> Using cache
 ---> 788046b5f293
Successfully built 788046b5f293
Successfully tagged reverseproxy:latest


We can check the create image:

$ docker images
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
reverseproxy                  latest              788046b5f293        3 minutes ago       25.1MB


Note that we copied the following nginx.conf to our reverse proxy container:

nginx.conf:

worker_processes 1;
 
events { worker_connections 1024; }
 
http {
 
    sendfile on;
 
    upstream docker-nginx {
        server nginx:80;
    }
 
    upstream docker-apache {
        server apache:80;
    }
 
    server {
        listen 8080;
 
        location / {
            proxy_pass         http://docker-nginx;
            proxy_redirect     off;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Host $server_name;
        }
    }
 
    server {
        listen 8081;
 
        location / {
            proxy_pass         http://docker-apache;
            proxy_redirect     off;
            proxy_set_header   Host $host;
            proxy_set_header   X-Real-IP $remote_addr;
            proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
            proxy_set_header   X-Forwarded-Host $server_name;
        }
    }
}


We set worker_processes explicitly to 1 which is the default value. It is common practice to run 1 worker process per core. For more about it, check Thread Pools in NGINX Boost Performance 9x!.

The worker_connections sets the maximum number of simultaneous connections that can be opened by a worker process (default=1024).

The sendfile is usually essential to speed up any web server via passing the pointers (without copying the whole object) straight to the socket descriptor. However, we use NGINX as a reverse proxy to serve pages from an application server, we can deactivate it.

The upstream directive in ngx_http_upstream_module defines a group of servers that can listen on different ports. So, the upstream directive is used to define a pool of servers.

Nginx can proxy requests to servers that communicate using the http(s), FastCGI, SCGI, and uwsgi, or memcached protocols through separate sets of directives for each type of proxy (Module ngx_http_upstream_module).

After defining the upstream servers, we need to tell NGINX how to listen and how to react to requests.

The most straight-forward type of proxy involves handing off a request to servers that can communicate using http. This type of proxy is known as a generic "proxy pass" and is handled by proxy_pass directive.

The proxy_pass directive is mainly found in location contexts, and it sets the protocol and address of a proxied server. When a request matches a location with a proxy_pass directive inside, the request is forwarded to the URL given by the directive.

The proxy_pass directive is what makes a configuration a reverse proxy. It specifies that all requests which match the location block (in this case the root / path) should be forwarded to a specific port on a specified host where the app is running.

In the above configuration snippet, no URI is given at the end of the server in the proxy_pass definition. For definitions that fit this pattern, the URI requested by the client will be passed to the upstream server as-is.

So, if we try to access the host machine via port 8080, NGINX will act as a reverse proxy and serve whatever is in the proxy_pass definition. In the above scenario, we have docker-nginx which is the name of one of our upstream servers, which means the nginx service will be served.

The request coming from NGINX on behalf of a client will look different than a request coming directly from a client. A big part of this is the headers that go along with the request. When NGINX proxies a request, it automatically makes some adjustments to the request headers it receives from the client:

    NGINX gets rid of any empty headers.
    The "Host" header is re-written to the value defined by the $proxy_host variable. This will be the IP address or name and port number of the upstream, directly as defined by the proxy_pass directive.





Host, X-Real-IP, and X-Forwarded-For

To adjust or set headers for proxy connections, we can use the proxy_set_header directive. The proxy_set_header allows redefining or appending fields to the request header passed to the proxied server. The syntax looks like this:

proxy_set_header field value;


In the configuration, we're passing an unchanged "Host" request header field like this:

proxy_set_header Host $host;


The above request sets the "Host" header to the $host variable, which should contain information about the original host being requested. The X-Real-IP is set to the IP address of the client so that the proxy can correctly make decisions or log based on this information.

The X-Forwarded-For (XFF) header is a list containing the IP addresses of every server the client has been proxied through up to this point.

The XFF header is a standard header for identifying the originating IP address of a client connecting to a web server through an HTTP proxy or a load balancer. When traffic is intercepted between clients and servers, server access logs contain the IP address of the proxy or load balancer only. To see the original IP address of the client, the XFF request header is used.

The XFF header is typically set by a proxy server or a load balancer to indicate who the real requester is.

This header is used for debugging, statistics, and generating location-dependent content and by design it exposes privacy sensitive information, such as the IP address of the client. Therefore the user's privacy must be kept in mind when deploying this header.

In our case, we set this to the $proxy_add_x_forwarded_for variable. This variable takes the value of the original XFF header retrieved from the client and adds the NGINX server's IP address to the end. In other words, the $proxy_add_x_forwarded_for variable is used to automatically append $remote_addr to any incoming XFF headers.


For more readable code, we could move the proxy_set_header directives out to the server or http context, allowing it to be referenced in more than one location:

worker_processes 1;
  
events { worker_connections 1024; }

http {

    sendfile on;

    upstream docker-nginx {
        server nginx:80;
    }

    upstream docker-apache {
        server apache:80;
    }
    
    proxy_set_header   Host $host;
    proxy_set_header   X-Real-IP $remote_addr;
    proxy_set_header   X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Forwarded-Host $server_name;
    
    server {
        listen 8080;
 
        location / {
            proxy_pass         http://docker-nginx;
            proxy_redirect     off;
        }
    }
 
    server {
        listen 8081;
 
        location / {
            proxy_pass         http://docker-apache;
            proxy_redirect     off;
        }
    }
}


For more on reverse proxy setup: Understanding Nginx HTTP Proxying, Load Balancing, Buffering, and Caching and Module ngx_http_proxy_module




docker-compose.yml

With Compose, we define a multi-container application in a single file, then spin our application up in a single command which does everything that needs to be done to get it running.

The main function of Docker Compose is the creation of microservice architecture, meaning the containers and the links between them.

Compared with docker commands, the docker-compose commands are not only similar, but they also behave like docker counterparts. The only difference is that docker-compose commands affect the entire multi-container architecture defined in the docker-compose.yml configuration file and not just a single container.

There are three steps to using Docker Compose:

    Define each service in a Dockerfile.
    Define the services and their relation to each other in the docker-compose.yml file.
    Use docker-compose up to start the system.


Here is our docker-compose.yml:

services:
    reverseproxy:
        image: reverseproxy
        ports:
            - 8080:8080
            - 8081:8081
        restart: always
 
    nginx:
        depends_on:
            - reverseproxy
        image: nginx:alpine
        restart: always
 
    apache:
        depends_on:
            - reverseproxy
        image: httpd:alpine
        restart: always


A services definition contains configuration which will be applied to each container started for that service, much like passing command-line parameters to docker run.

The depends_on expresses dependency between services and the docker-compose up will start services in dependency order.

Let's create and start containers in detached mode (run containers in the background).

$ docker-compose up -d
Creating network "docker-compose-nginx-reverse-proxy_default" with the default driver
Pulling apache (httpd:alpine)...
alpine: Pulling from library/httpd
188c0c94c7c5: Already exists
87dbd21cecbb: Pull complete
6a369e309fde: Pull complete
cf56700e8fe2: Pull complete
c4617a06d2a7: Pull complete
Digest: sha256:e0243332126bc05728d66c72e6ae1f2b8ab40133f3ddccc3c1d6c2286dee0ae3
Status: Downloaded newer image for httpd:alpine
Creating docker-compose-nginx-reverse-proxy_reverseproxy_1 ... done
Creating docker-compose-nginx-reverse-proxy_nginx_1        ... done
Creating docker-compose-nginx-reverse-proxy_apache_1       ... done


The docker-compose up command is a shorthand form of docker-compose build and docker-compose run.

When complete, we should have three containers deployed, two of which we cannot access directly:

$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                                      NAMES
c361bcaabe93        nginx:alpine        "/docker-entrypoint.…"   5 minutes ago       Up 5 minutes        80/tcp                                     docker-compose-nginx-reverse-proxy_nginx_1
339a938e689f        httpd:alpine        "httpd-foreground"       5 minutes ago       Up 5 minutes        80/tcp                                     docker-compose-nginx-reverse-proxy_apache_1
9d9c53455cf7        reverseproxy        "/docker-entrypoint.…"   5 minutes ago       Up 5 minutes        80/tcp, 0.0.0.0:8080-8081->8080-8081/tcp   docker-compose-nginx-reverse-proxy_reverseproxy_1



We can check our applications (one with NGINX and the other one with apache).

Navigate to http://localhost:8080, and this will hit the NGINX reverse proxy which will in turn load the NGINX web application:
localhost-8080-nginx.png

Then, navigate to http://localhost:8081, the NGINX reverse proxy will be hit and the Apache web application will be loaded:
localhost-8081-apache.png

To stop container gracefully:

$ docker-compose stop
Stopping docker-compose-nginx-reverse-proxy_nginx_1        ... done
Stopping docker-compose-nginx-reverse-proxy_apache_1       ... done
Stopping docker-compose-nginx-reverse-proxy_reverseproxy_1 ... done

The command stops the process in a running container. The main process inside the container will receive SIGTERM, and after a grace period, SIGKILL.

To remove (and stop) the container by docker-compose up, we can use docker-compose down. By default, it only removes containers and networks created by up. But with additional options it removes volumes (--volumes or -v option), and images (--rmi all or --rmi local).

$ docker-compose down
Removing docker-compose-nginx-reverse-proxy_nginx_1        ... done
Removing docker-compose-nginx-reverse-proxy_apache_1       ... done
Removing docker-compose-nginx-reverse-proxy_reverseproxy_1 ... done
Removing network docker-compose-nginx-reverse-proxy_default





git source

Source : git I




Sample II

Here is another example for a reverse proxy. We'll have two servers (site1 and site2) behind the proxy:
tree-reverse.png

Let's run the docker-compose under each directory (~/site1 and ~/site2)

$ cd site1
~/site1$ docker-compose build
~/site1$ docker-compose up -d
Creating network "site1_default" with the default driver
Creating site1_app_1 ... done

~/site1$ cd ../site2
~/site2$ docker-compose build
~/site2$ docker-compose up -d
Creating network "site2_default" with the default driver
Creating site2_app_1 ... done

~$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED              STATUS              PORTS               NAMES
85d74d179001        nginx:1.12          "nginx -g 'daemon of…"   39 seconds ago       Up 38 seconds       80/tcp              site2_app_1
58e254a1d8ca        nginx:1.12          "nginx -g 'daemon of…"   About a minute ago   Up About a minute   80/tcp              site1_app_1

~$ docker network ls
NETWORK ID          NAME                DRIVER              SCOPE
e7e0eb51475b        bridge              bridge              local
327de6abc2e9        host                host                local
45af92fa2587        none                null                local
1d02527ec4e0        site1_default       bridge              local
866efe7973ca        site2_default       bridge              local


Note that the app service is in a directory called site1, and when we run docker-compose up, a network called site1_default is created. A container is created using the app's configuration. It joins the network site1_default under the name app.

Now, let's work on the reverse proxy:

~$ cd reverse-proxy
    
~/reverse-proxy$ docker-compose build
Building proxy
Step 1/4 : FROM nginx:1.12
 ---> 92e8f1b61b09
Step 2/4 : COPY ./default.conf /etc/nginx/conf.d/default.conf
 ---> Using cache
 ---> 126ba809f42c
Step 3/4 : COPY ./backend-not-found.html /var/www/html/backend-not-found.html
 ---> Using cache
 ---> 3fd66191c774
Step 4/4 : COPY ./includes/ /etc/nginx/includes/
 ---> Using cache
 ---> d70a589d357b
Successfully built d70a589d357b

~/reverse-proxy$ docker-compose up -d
Creating reverseproxy_proxy_1

$ docker ps
CONTAINER ID        IMAGE                 COMMAND                  CREATED             STATUS              PORTS                NAMES
4ba7ece3e731        reverse-proxy_proxy   "nginx -g 'daemon of…"   8 seconds ago       Up 7 seconds        0.0.0.0:80->80/tcp   reverse-proxy_proxy_1
85d74d179001        nginx:1.12            "nginx -g 'daemon of…"   10 minutes ago      Up 10 minutes       80/tcp               site2_app_1
58e254a1d8ca        nginx:1.12            "nginx -g 'daemon of…"   11 minutes ago      Up 11 minutes       80/tcp               site1_app_1



site1-example-com.png
site2-example-com.png

Note that we need to set the domains in /etc/hosts using ip of host machine (192.168.148.101):

192.168.148.101 site1.example.com
192.168.148.101 site2.example.com


reverse-proxy/Dockerfile:

FROM nginx:1.12

#  default conf for proxy service
COPY ./default.conf /etc/nginx/conf.d/default.conf

# NOT FOUND response
COPY ./backend-not-found.html /var/www/html/backend-not-found.html

# Proxy configurations
COPY ./includes/ /etc/nginx/includes/


The docker-compose.yml files used are:

reverse-proxy/docker-compose.yml:

version: '3'
services:
  proxy:
    build: ./
    networks:
      - site1
      - site2
    ports:
      - 80:80

networks:
  site1:
    external:
      name: site1_default
  site2:
    external:
      name: site2_default


site1/docker-compose.yml:

version: '3'
services:
  app:
    image: nginx:1.12
    volumes:
      - .:/usr/share/nginx/html/
    expose:
      - "80"


site2/docker-compose.yml:

version: '3'
services:
  app:
    image: nginx:1.12
    volumes:
      - .:/usr/share/nginx/html/
    expose:
      - "80"


For other files, please check git II



Docker & K8s

    Docker install on Amazon Linux AMI
    Docker install on EC2 Ubuntu 14.04
    Docker container vs Virtual Machine
    Docker install on Ubuntu 14.04
    Docker Hello World Application
    Nginx image - share/copy files, Dockerfile
    Working with Docker images : brief introduction
    Docker image and container via docker commands (search, pull, run, ps, restart, attach, and rm)
    More on docker run command (docker run -it, docker run --rm, etc.)
    Docker Networks - Bridge Driver Network
    Docker Persistent Storage
    File sharing between host and container (docker run -d -p -v)
    Linking containers and volume for datastore
    Dockerfile - Build Docker images automatically I - FROM, MAINTAINER, and build context
    Dockerfile - Build Docker images automatically II - revisiting FROM, MAINTAINER, build context, and caching
    Dockerfile - Build Docker images automatically III - RUN
    Dockerfile - Build Docker images automatically IV - CMD
    Dockerfile - Build Docker images automatically V - WORKDIR, ENV, ADD, and ENTRYPOINT
    Docker - Apache Tomcat
    Docker - NodeJS
    Docker - NodeJS with hostname
    Docker Compose - NodeJS with MongoDB
    Docker - Prometheus and Grafana with Docker-compose
    Docker - StatsD/Graphite/Grafana
    Docker - Deploying a Java EE JBoss/WildFly Application on AWS Elastic Beanstalk Using Docker Containers
    Docker : NodeJS with GCP Kubernetes Engine
    Docker : Jenkins Multibranch Pipeline with Jenkinsfile and Github
    Docker : Jenkins Master and Slave
    Docker - ELK : ElasticSearch, Logstash, and Kibana
    Docker - ELK 7.6 : Elasticsearch on Centos 7
    Docker - ELK 7.6 : Filebeat on Centos 7
    Docker - ELK 7.6 : Logstash on Centos 7
    Docker - ELK 7.6 : Kibana on Centos 7
    Docker - ELK 7.6 : Elastic Stack with Docker Compose
    Docker - Deploy Elastic Cloud on Kubernetes (ECK) via Elasticsearch operator on minikube
    Docker - Deploy Elastic Stack via Helm on minikube
    Docker Compose - A gentle introduction with WordPress
    Docker Compose - MySQL
    MEAN Stack app on Docker containers : micro services
    MEAN Stack app on Docker containers : micro services via docker-compose
    Docker Compose - Hashicorp's Vault and Consul Part A (install vault, unsealing, static secrets, and policies)
    Docker Compose - Hashicorp's Vault and Consul Part B (EaaS, dynamic secrets, leases, and revocation)
    Docker Compose - Hashicorp's Vault and Consul Part C (Consul)
    Docker Compose with two containers - Flask REST API service container and an Apache server container
    Docker compose : Nginx reverse proxy with multiple containers
    Docker & Kubernetes : Envoy - Getting started
    Docker & Kubernetes : Envoy - Front Proxy
    Docker & Kubernetes : Ambassador - Envoy API Gateway on Kubernetes
    Docker Packer
    Docker Cheat Sheet
    Docker Q & A #1
    Kubernetes Q & A - Part I
    Kubernetes Q & A - Part II
    Docker - Run a React app in a docker
    Docker - Run a React app in a docker II (snapshot app with nginx)
    Docker - NodeJS and MySQL app with React in a docker
    Docker - Step by Step NodeJS and MySQL app with React - I
    Installing LAMP via puppet on Docker
    Docker install via Puppet
    Nginx Docker install via Ansible
    Apache Hadoop CDH 5.8 Install with QuickStarts Docker
    Docker - Deploying Flask app to ECS
    Docker Compose - Deploying WordPress to AWS
    Docker - WordPress Deploy to ECS with Docker-Compose (ECS-CLI EC2 type)
    Docker - WordPress Deploy to ECS with Docker-Compose (ECS-CLI Fargate type)
    Docker - ECS Fargate
    Docker - AWS ECS service discovery wit

:end:















