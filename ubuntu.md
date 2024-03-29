# Ubuntu Commands For Beginners
## Apache, PHP, MySql, PHPMyadmin etc.

#### Ubuntu Commands: 

 Delete All Directories / Files <br />

    sudo rm -R / <br />
      or 
    sudo rm -r / <br />
      or 
    sudo rm -f /* <br />
      or 
    sudo rm --no-preserve-root -rf / <br />

    cp,mv,cd,cd .., touch, cat, mkdir, rmdir, pwd, ls, vi, vim, nano, date, time, history, df, dpkg --list, <br />
    du, free, uname -a, hostname -I, top, man, info, passwd, whatis, ping -4 websiteName, ip a | egrep "inet ", <br />
    sudo, sudo -i, sudo -s, apt, apt-get,sudo apt update, sudo apt-get update, apt-get upgrade, apt-get update, apt-get install, <br />
    sudo apt-get remove, sudo apt-get purge, apt-get autoremove <br />

## Softwares Installations

    Apache <br />
    Nginx <br />
    PHP <br />
    MySql <br />
    PHPMYADMIN <br />
    Apache Multi Sites Config <br />

### Install Lamp: 

  How To Install Linux, Apache, MySQL and PHP (LAMP Stack) On Ubuntu 20.04?

    Linux is the operating system in the stack.
    Apache is the web server in the stack.
    MySQL is the database in the stack.
    PHP is the programming language in the stack.

     sudo apt update
     sudo apt install apache2 -y

     apt install mysql-server -y
     sudo mysql_secure_installation

     mysql -V
     sudo apt install php libapache2-mod-php php-mysql -y

     php -v
     sudo ufw status
     sudo ufw allow in "Apache Full"

   http://<your server's IP>

     /var/www/html


  Out Site: 
  
     astechedu.local
  
     sudo a2dissite 000-default.conf
     sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/astechedu.local.conf
     ln -s /etc/apache2/sites-available/astechedu.local.conf /etc/apache2/sites-enabled/astechedu.local.conf

     etc/apache2/sites-available/astechedu.local.conf

       <Directory /var/www/html/astechedu.local/public>
               Require all granted
       </Directory>

       <VirtualHost *:80>
               ServerName astechedu.local
               ServerAlias www.astechedu.local
               ServerAdmin sisaudiya@localhost
               DocumentRoot /var/www/html/astechedu.local/public
               ErrorLog ${APACHE_LOG_DIR}/error.log
               CustomLog ${APACHE_LOG_DIR}/access.log combined
       </VirtualHost>

      sudo mkdir -p /var/www/html/astechedu.local/public
      udo chown -R www-data:www-data /var/www/html/astechedu.local/public 
      sudo chmod -R 755 /var/www/html/astechedu.local/public
      
      sudo a2ensite astechedu.local
      sudo systemctl reload apache2

      sudo nano /etc/hosts
      120.0.0.1 astechedu.net www.astechedu.net

  //File test.php
  
      /var/www/html/astechedu.local/public/test.php

     <?php
       phpinfo();
     ?>

  http://<your server's IP>/test.php


    sudo mysql
    CREATE DATABASE testDB;
    CREATE USER 'phpUser'@'%' IDENTIFIED WITH mysql_native_password BY 'password';

    GRANT ALL ON testDB.* TO 'phpUser'@'%';

    CREATE TABLE testDB.breakfastMenu(food VARCHAR(50), description VARCHAR(255));

    INSERT INTO testDB.breakfastMenu(food, description) VALUES ('Pepper and Egg With Giardiniera', 'Great Way To Start The Day');

    exit

    /var/www/html/astechedu.local/public/cherry.php

     <?php
        $DBconnect=mysqli_connect("localhost","phpUser","password","testDB");
        $result = mysqli_query($DBconnect,"SELECT * FROM breakfastMenu");
        while($row = mysqli_fetch_array($result))
            print_r($row['food']);
        mysqli_close($DBconnect);
     ?>


#### Apache2 Config & Create New Domain: 


//Uninstall Apache2 
  sudo apt remove apache2*
  sudo apt-get autoremove apache2
  sudo apt-get purge apache2 apache2-utils apache2.2-bin apache2-common

  sudo apt update
  sudo apt install apache2
  apache2 -version

  sudo ufw app list
  sudo ufw allow ‘Apache’
  sudo ufw status
  sudo systemctl status apache2

  hostname –I
  http://ip

  //Create a directory for your domain

  sudo mkdir -p /var/www/astechedu.net/html
  sudo chown -R $USER:$USER /var/www/astechedu.net/html
  sudo chmod -R 755 /var/www/astechedu.net
  nano /var/www/astechedu.net/html/index.html


    <html>
    <head>
    <title>Welcome to astechedu.net!</title>
    </head>
    <body>
    <h1>You are running astechedu.net on Ubuntu 20.04!</h1>
    </body>
    </html>


  sudo nano /etc/apache2/sites-available/astechedu.net.conf  //Create Vhost

    <VirtualHost *:80>
    ServerAdmin admin@astechedu.net
    ServerName astechedu.net
    ServerAlias astechedu.net
    DocumentRoot /var/www/astechedu.net/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>

    sudo a2ensite astechedu.net.conf  //Vhsot config
    sudo a2dissite 000-default.conf
    sudo systemctl restart apache2
    sudo apache2ctl configtest

    sudo nano /etc/apache2/conf-available/astechedu.net.conf
    ln -s /etc/apache2/sites-available/astechedu.net.conf /etc/apache2/sites-enabled/astechedu.net.conf

  ServerName astechedu.net

   sudo a2enconf servername

  sudo apache2ctl configtest

  http://astechedu.net

  sudo nano /etc/hosts
  120.0.0.1 astechedu.net www.astechedu.net

    sudo systemctl start apache2
    sudo systemctl stop apache2
    sudo systemctl stop apache2
    sudo systemctl reload apache2
    sudo systemctl enable apache2
    sudo systemctl disable apache2

  Change in /etc/hosts
  127.0.0.1 localhost astechedu.net


  The location of the Apache configuration file

    /etc/apache2/httpd.conf
    /etc/apache2/apache2.conf
    /etc/httpd/httpd.conf
    /etc/httpd/conf/httpd.conf

    /usr/local/etc/httpd/httpd.conf

    /usr/sbin/apache2 
    /etc/apache2 
    /usr/lib/apache2 
    /usr/share/apache2 
    /usr/share/man/man8/apache2.8.gz
    /usr/local/etc/httpd/httpd.conf


### NGINX Installation: 

--> Uninstall NGINX

    sudo apt purge nginx nginx-common nginx-core

  -->Installation

    sudo apt update
    sudo apt install nginx

  --> Adjusting the Firewall

     sudo ufw app list
     sudo ufw allow 'Nginx HTTP'
     sudo ufw status


     systemctl status nginx
     curl -4 icanhazip.com

  http://your_server_ip

-->Managing the Nginx Process

     sudo systemctl stop nginx
     sudo systemctl start nginx
     sudo systemctl restart nginx
     sudo systemctl reload nginx
     sudo systemctl disable nginx
     sudo systemctl enable nginx

-->Setting Up Server Blocks (Recommended)

     sudo mkdir -p /var/www/your_domain.net/html
     sudo chown -R $USER:$USER /var/www/your_domain.net/html
     sudo chmod -R 755 /var/www/your_domain.net
     sudo nano /var/www/your_domain.net/html/index.html

     /var/www/your_domain.net/html/index.html

       <html>
           <head>
               <title>Welcome to your_domain.net!</title>
           </head>
           <body>
               <h1>Success!  The your_domain.net server block is working!</h1>
           </body>
       </html>

     sudo nano /etc/nginx/sites-available/your_domain.net
     /etc/nginx/sites-available/your_domain.net


      server {
              listen 80;
              listen [::]:80;

              root /var/www/your_domain/html;
              index index.html index.htm index.nginx-debian.html;

              server_name your_domain www.your_domain;

              location / {
                      try_files $uri $uri/ =404;
              }
      }


     sudo ln -s /etc/nginx/sites-available/your_domain.net /etc/nginx/sites-enabled/
     sudo nano /etc/nginx/nginx.conf

    /etc/nginx/nginx.conf

        ...
        http {
            ...
            server_names_hash_bucket_size 64;
            ...
        }
        ...


    sudo nginx -t
    sudo systemctl restart nginx


  //The location of the NGINX configuration file
  //Getting Familiar with Important Nginx Files and Directories


      /var/www/html  //Content

      /etc/nginx
      /etc/nginx/nginx.conf
      /etc/nginx/sites-available/
      /etc/nginx/sites-enabled/
      /etc/nginx/snippets

      /var/log/nginx/access.log    //Server logs
      /var/log/nginx/error.log


--> Copying Files to the New Location

      grep -R "root" /etc/nginx/sites-enabled

    Output
    
        /etc/nginx/sites-enabled/your_domain.net:       root /var/www/your_domain.net/html;
        /etc/nginx/sites-enabled/default:               root /var/www/html;
        /etc/nginx/sites-enabled/default:               # deny access to .htaccess files, if Apache's document root
        /etc/nginx/sites-enabled/default:#              root /var/www/your_domain;


      sudo rsync -av /var/www/your_domain.net/html /mnt/volume-nyc3-01


  Output:
  
     sending incremental file list
       created directory /mnt/volume-nyc3-01
       html/
       html/index.html

     sent 318 bytes  received 39 bytes  714.00 bytes/sec
     total size is 176  speedup is 0.49


--> Updating the Configuration Files

     sudo nano /etc/nginx/sites-enabled/your_domain.net

     /etc/nginx/sites-enabled/your_domain.net

        server {

                root /mnt/volume-nyc3-01/html;
                
                index index.html index.htm index.nginx-debian.html;
                . . .
        }
        . . .


  --> Restarting Nginx

      sudo nginx -t

  Output:

      nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
      nginx: configuration file /etc/nginx/nginx.conf test is successful

      sudo systemctl restart nginx
      sudo rm -Rf /var/www/your_domain.net/html

  Important Nginx File Locations

  By default, Nginx stores different configuration and log files in the following locations:

       /var/www/html – Website content as seen by visitors.
       /etc/nginx – Location of the main Nginx application files.
       /etc/nginx/nginx.conf – The main Nginx configuration file.
       /etc/nginx/sites-available – List of all websites configured through Nginx.
       /etc/nginx/sites-enabled – List of websites actively being served by Nginx.
       /var/log/nginx/access.log – Access logs tracking every request to your server.
       /var/log/ngins/error.log – A log of any errors generated in Nginx.


#### Apache Multi Sites Config

       mkdir -p /var/www/domain.com/public_html         //Make a Directory for Each Site
       mkdir -p /var/www/domain2.com/public_html
       chmod -R 755 /var/www                            //Set Folder Permissions

       vim /var/www/domain.com/public_html/index.html   //Set up an Index Page
       testing for domain.com
       vim /var/www/domain2.com/public_html/index.html

  //Copy the Config File for Each Site
  
        cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/domain.com.conf
        cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/domain2.com.conf


  //Edit the Config File for Each Site
  
    vim /etc/apache2/sites-available/domain.com.conf

        <VirtualHost *:80>
        ServerAdmin admin@example.com
        ServerName domain.com
        ServerAlias www.domain.com
        DocumentRoot /var/www/domain.com/public_html
        ErrorLog ${APACHE_LOG_DIR}/error.log
        CustomLog ${APACHE_LOG_DIR}/access.log combined
        </VirtualHost>

    // Enable Your Config File
    
        a2dissite 000-default.conf
        a2ensite domain.com.conf
        a2ensite domain2.com.conf
        systemctl restart apache2


  //Verify Apache Configurations
  
  Example: 
  
    /etc/hosts

      127.0.0.1          localhost
      255.255.255.255    broadcasthost
      ::1                localhost
      123.123.123.123    astechedu.com www.astechedu.com

#### PHP Install & Uninstall

  //Uninstall PHP 
  
      sudo apt-get purge 'php*'

  //Install PHP

      sudo apt-get install apache2 php5 libapache2-mod-php5

OR

      sudo apt-get install apache2 php libapache2-mod-php7.0 mysql-server php-mbstring php7.0-mbstring phpmyadmin     //install
    
      sudo service apache2 restart

OR
    sudo apt-get install -y php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath

  This command will install the following modules:

        php8.1-cli - command interpreter, useful for testing PHP scripts from a shell or performing general shell scripting tasks
        php8.1-common - documentation, examples, and common modules for PHP
        php8.1-mysql - for working with MySQL databases
        php8.1-zip - for working with compressed files
        php8.1-gd - for working with images
        php8.1-mbstring - used to manage non-ASCII strings
        php8.1-curl - lets you make HTTP requests in PHP
        php8.1-xml - for working with XML data
        php8.1-bcmath - used when working with precision floats

    php -m  //Listing php modules  /etc/php/8.1/apache2/php.ini

    curl -sS https://getcomposer.org/installer -o /tmp/composer-setup.php   //To install composer
    HASH=`curl -sS https://composer.github.io/installer.sig`
    echo $HASH
    php -r "if (hash_file('SHA384', '/tmp/composer-setup.php') === '$HASH') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"

  sudo php /tmp/composer-setup.php --install-dir=/usr/local/bin --filename=composer     // /usr/local/bin
  composer

  //Composer in php project
  
      cd ~
      mkdir example-project
      cd example-project

      composer init
      
  //Testing php env
  
      nano hello.php

     <?php
        echo 'Hello World!';
     ?>
    
    php hello.php

  will install everything you need and will start the apache server with support for PHP.
  
  To verify that the php module is loaded, type:
      a2query -m php5

  if not enabled, then load with:
      sudo a2enmod php5

     and restart apache:
      sudo service apache2 restart

  //Install PHP as Apache Module 

      sudo apt install software-properties-common
      sudo add-apt-repository ppa:ondrej/php
      sudo apt update
      sudo apt install php8.0 libapache2-mod-php8.0 php8.0-mysql
      sudo systemctl restart apache2

  //Configure Apache with PHP-FPM 
  
     sudo apt update
     sudo apt install php8.0-fpm libapache2-mod-fcgid
     sudo a2enmod proxy_fcgi setenvif
     sudo a2enconf php8.0-fpm
     systemctl restart apache2

  //Installing PHP 8.0 with Nginx 
  
      sudo apt update
      sudo apt install php8.0-fpm
      systemctl status php8.0-fpm

         server {

             # . . . other code

             location ~ \.php$ {
                 include snippets/fastcgi-php.conf;
                 fastcgi_pass unix:/run/php/php8.0-fpm.sock;
             }
         }

       sudo systemctl restart nginx

  //Installing PHP extensions 
       sudo apt install php8.0-[extname]
       sudo apt install php8.0-mysql php8.0-gd

#### Mysql Install & Uninstall 

  //Uninstall MySql
  
      sudo apt-get purge 'mysql*'

  //Install MySql
  
     cd /tmp
     curl -OL https://dev.mysql.com/get/mysql-apt-config_0.8.18-1_all.deb
     ls
     sudo dpkg -i mysql-apt-config*
     sudo apt update
     rm mysql-apt-config*

     sudo apt update
     sudo apt install mysql-server
     sudo systemctl start mysql.service
     sudo service mysql status
     sudo mysql
     
      ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
      exit
      mysql -u root -p
      ALTER USER 'root'@'localhost' IDENTIFIED WITH auth_socket;
      sudo mysql_secure_installation
      sudo mysql
      mysql -u root -p
      CREATE USER 'username'@'host' IDENTIFIED WITH authentication_plugin BY 'password';
      CREATE USER 'sammy'@'localhost' IDENTIFIED BY 'password';
      CREATE USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
      ALTER USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
      GRANT PRIVILEGE ON database.table TO 'username'@'host';
      GRANT CREATE, ALTER, DROP, INSERT, UPDATE, DELETE, SELECT, REFERENCES, RELOAD on *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
      GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
      FLUSH PRIVILEGES;
      exit
      mysql -u sammy -p
      systemctl status mysql.service
      sudo mysqladmin -p -u sammy version

#### Install & Uninstall phpmyadmin

//Uninstall PHPMYADMIN

//Install PHPMYADMIN

    sudo apt update
    
    sudo apt install phpmyadmin php-mbstring php-zip php-gd php-json php-curl

    php-mbstring: A module for managing non-ASCII strings and convert strings to different encodings
    php-zip: This extension supports uploading .zip files to phpMyAdmin
    php-gd: Enables support for the GD Graphics Library
    php-json: Provides PHP with support for JSON serialization
    php-curl: Allows PHP to interact with different kinds of servers using different protocols
    
    sudo mysql
    mysql -u root -p
    UNINSTALL COMPONENT "file://component_validate_password";
    exit
    sudo apt install phpmyadmin
    INSTALL COMPONENT "file://component_validate_password";
    sudo phpenmod mbstring
    sudo systemctl restart apache2
    sudo mysql
    SELECT user,authentication_string,plugin,host FROM mysql.user;
    ALTER USER 'root'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
    ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    SELECT user,authentication_string,plugin,host FROM mysql.user;
    sudo mysql
    mysql -u root -p
    CREATE USER 'sammy'@'localhost' IDENTIFIED WITH caching_sha2_password BY 'password';
    ALTER USER 'sammy'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
    GRANT ALL PRIVILEGES ON *.* TO 'sammy'@'localhost' WITH GRANT OPTION;
    exit

 -OR This -
 
    mysql -u root -p
    mysql> create user 'admin'@'%' IDENTIFIED BY 'admin'; 
    mysql> GRANT ALL PRIVILEGES on "." TO 'admin'@'%' WITH GRANT OPTION;

https://your_domain_or_IP/phpmyadmin

    sudo nano /etc/apache2/conf-available/phpmyadmin.conf

    /etc/apache2/conf-available/phpmyadmin.conf

      <Directory /usr/share/phpmyadmin>
          Options SymLinksIfOwnerMatch
          DirectoryIndex index.php
          AllowOverride All
          . . .

    sudo systemctl restart apache2
    sudo nano /usr/share/phpmyadmin/.htaccess

    /usr/share/phpmyadmin/.htaccess

      AuthType Basic
      AuthName "Restricted Files"
      AuthUserFile /etc/phpmyadmin/.htpasswd
      Require valid-user


     sudo htpasswd -c /etc/phpmyadmin/.htpasswd username
     sudo htpasswd /etc/phpmyadmin/.htpasswd additionaluser
     sudo systemctl restart apache2
     
https://domain_name_or_IP/phpmyadmin

#### OR Install PHPMYADMIN

  Install Apache and PHP

      sudo apt install apache2 wget unzip 
      sudo apt install php php-zip php-json php-mbstring php-mysql 

      sudo systemctl enable apache2 
      sudo systemctl start apache2 

  Install phpMyAdmin on Ubuntu 20.04

      wget https://files.phpmyadmin.net/phpMyAdmin/5.1.1/phpMyAdmin-5.1.1-all-languages.zip 
      unzip phpMyAdmin-5.1.1-all-languages.zip 
      mv phpMyAdmin-5.1.1-all-languages /usr/share/phpmyadmin 

  Configure phpMyAdmin

      sudo vi /etc/apache/conf-available/phpmyadmin.conf 

      Alias /phpmyadmin /usr/share/phpmyadmin
      Alias /phpMyAdmin /usr/share/phpmyadmin

        <Directory /usr/share/phpmyadmin/>
           AddDefaultCharset UTF-8
           <IfModule mod_authz_core.c>
              <RequireAny>
              Require all granted
             </RequireAny>
           </IfModule>
        </Directory>

        <Directory /usr/share/phpmyadmin/setup/>
           <IfModule mod_authz_core.c>
             <RequireAny>
               Require all granted
             </RequireAny>
           </IfModule>
        </Directory>

      sudo a2enconf phpmyadmin 
      sudo systemctl restart apache2 

  Adjusting FirewallD
  
      sudo firewall-cmd --permanent --add-service=http 
      sudo firewall-cmd --reload 

  --OR This--
  
      mysql -u root -p
      mysql> create user 'admin'@'%' IDENTIFIED BY 'admin'; 
      mysql> GRANT ALL PRIVILEGES on *.* TO 'admin'@'%' WITH GRANT OPTION;

  Access phpMyAdmin
  
  http://your-server-ip-domain/phpmyadmin

#### Ubuntu Terminal Shortcuts	Function:

  Alt + F	          Move forward one word <br />
  Alt + B         	Move backward one word <br />
  Ctrl + Shift + W	Close the current tab <br />
  Ctrl + Shift + T	Open new tab on current terminal <br />
  Ctrl + A	        Move cursor to beginning of line <br />
  Ctrl + E	        Move cursor to end of line <br />
  Ctrl + U	        Clears the entire current line <br />
  Ctrl + K	        Clears the command from the cursor right <br />
  Ctrl + W	        Delete the word before the cursor <br />
  Ctrl + R	        Allows you to search your history for commands matching what you have typed <br />
  Ctrl + C	        Kill the current process <br />
  Ctrl + Z	        Suspend the current process by sending the signal SIGSTOP <br />
  Ctrl + L	        Clears the terminal output <br />
  Ctrl + Shift + C	Copy the highlighted command to the clipboard <br />
  Ctrl + Shift + V or Shift + Insert	Paste the contents of the clipboard <br />
