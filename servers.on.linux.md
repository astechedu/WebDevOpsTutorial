# Servers On Linux


[Home](all-file-links.md)

[Got To Bottom](#botton)
<a name="top"></a>


Topics: 

   [Nginx Mulit Domains on ubuntu 20.04](#nginx_multi_domains)

   [Docker compose : NGINX reverse proxy with multiple containers](#nginx_reverse_proxxy)








[Got To Top](#top)
<a name="nginx_multi_domains"></a>
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






[Got To Top](#top)
<a name="nginx_reverse_proxxy"></a>
# Reverse Proxy



Docker compose : NGINX reverse proxy with multiple container


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


      docker build -t nginx-alpine .
      docker run -t -i nginx-alpine /bin/bash
      bash-4.4# nginx -v
      nginx version: nginx/1.19.3


Once it's done, we may want to remove the line we've just added since it will increase the size of the image.

Let's build reverse proxy image:


        $ docker build -t reverseproxy .


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



#docker-compose.yml



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


      docker-compose up -d


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


          docker-compose stop

          docker-compose down


Removing docker-compose-nginx-reverse-proxy_nginx_1        ... done
Removing docker-compose-nginx-reverse-proxy_apache_1       ... done
Removing docker-compose-nginx-reverse-proxy_reverseproxy_1 ... done
Removing network docker-compose-nginx-reverse-proxy_default





#Sample II

Here is another example for a reverse proxy. We'll have two servers (site1 and site2) behind the proxy:
tree-reverse.png

Let's run the docker-compose under each directory (~/site1 and ~/site2)

   cd site1

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



:end:




[Got To Top](#top)











