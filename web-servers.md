# Web Servers Installation


<a name="all-file-links.md"></a>
 <a name="top"></a>
 
Topics

 1. [Inginx On Ubuntu 20.04](#nginx_server)
 2. [Nginx Reverse Proxxy (as a proxy server) & apache2 (Origina Server)](#reverse_proxy)
 
 
 
 
 
 
 
 
 
 [Go To Top](#top)
 <a name="nginx_server"></a>
## Inginx On Ubuntu 20.04

    sudo apt-get update
    sudo apt-get install nginx
    nginx -v

    sudo systemctl status nginx
    sudo systemctl start nginx
    sudo systemctl enable nginx
    sudo systemctl stop nginx
    sudo systemctl disable nginx
    sudo systemctl reload nginx
    sudo systemctl restart nginx
    sudo ufw app list
    sudo ufw allow 'nginx http'
    sudo ufw reload
    sudo ufw allow 'nginx https'
    sudo ufw allow 'nginx full'

http://127.0.0.1


  sudo apt-get install curl
  curl –i 127.0.0.1

  sudo mkdir -p /var/www/test_domain.com/html
  sudo chown –R $USER:$USER /var/www/test_domain.com
  sudo chmod –R 755 /var/www/test_domain.com
  sudo nano /var/www/test_domain.com/html/index.html


    <html>
    <head>
    <title>Welcome to test_domain.com!</title>
    </head>
    <body>
    <h1>This message confirms that your Nginx server block is working. Great work!</h1>
    </body>
    </html>

Press CTRL+o to write the changes, then CTRL+x to exit.

    sudo nano /etc/nginx/sites-available/test_domain.com


Enter the following code:


    server    {
    listen 80;

    root /var/www/test_domain.com/html;
    index index.html index.htm index.nginx.debian.html;

    server_name test_domain.com www.test_domain.com;
    location /          {
    try_files $uri $uri/ =404;
          }
    }



    sudo ln –s /etc/nginx/sites-available/test_domain.com /etc/nginx/sites-enabled
    sudo systemctl restart nginx
    sudo nginx –t

    hostname –i
    sudo nano /etc/hosts
    
127.0.1.1 test_domain1.com www.test_domain1.com


### Important Nginx File Locations

By default, Nginx stores different configuration and log files in the following locations:

    /var/www/html – Website content as seen by visitors.
    /etc/nginx – Location of the main Nginx application files.
    /etc/nginx/nginx.conf – The main Nginx configuration file.
    /etc/nginx/sites-available – List of all websites configured through Nginx.
    /etc/nginx/sites-enabled – List of websites actively being served by Nginx.
    /var/log/nginx/access.log – Access logs tracking every request to your server.
    /var/log/ngins/error.log – A log of any errors generated in Nginx.









[Go To Top](#top)
<a name="proxy_server"></a>
# Reverse Proxy nginx (proxy server) and apache2


       Internet (Client)  <------->  Reverse Proxy ( nginx )   <------->   Original Server ( Ex. apache2 )
 

 Steps: 
  1. Enable and start nginx and apache2 
  2. Change port of apache2 in httpd file 80 to 8080
  3. Change conf in nginx 
     Config Location: /etc/nginx/nginx.conf
       location /{
          proxy_pass http://127.0.0.1:8080/;
       }

   4. sudo systemctl enable nginx.services
   5. sudo systemctl stop nginx.service
   6. Check the logs
      /var/log/nginx
      sudo cat /var/log/audit/audit.log | grep nginx | grep denied
      cd /var/log/nginx/
      ls -ltr
      less error.log
      
      Permission denied
      
      Solutions: 
      
       1. List of all the httpd SELinex boolean
       
          #getsebool -a grep httpd
          
       3. Enable the network connect boolean 
       
          #setsebool httpd_can_network_connect on -P

       4. Refress Browser












###### Install apache nginx php mysql etc
[Ubuntu File click here](ubuntu.md)















 [Go To Top](#top)








