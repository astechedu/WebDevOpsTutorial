# Web Servers Installation

## Topics
 1. Inginx On Ubuntu 20.04
 
 ## myLib documentation
see documentation [here](myLib/ubuntu.md)
[a link](https://github.com/astechedu/gittutorial/ubuntu.txt)

[a link](https://github.com/astechedu/gittutorial/blob/branch/ubuntu.md)

…you can use a relative link:

[Ubuntu File](ubuntu.md)
[a relative link](path%20with%20spaces/ubuntu.md)

 
 
 
 
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

