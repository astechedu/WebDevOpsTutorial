
# Linux Basic Commands:
  
<a name="top"></a>
Topics: <br /> 

   1. [Linux Cell Scripting click here](#linux_cell_scripting)   <br />
   2. [CentOS Basic Commands click here](#centos_basic_commands)   <br />
   3. [Install PHP On Ubuntu click here](#install_php)  <br /> 
   4. [Install Composer On Ubuntu click here](#install_composer)  <br />
   5. [Install Apache2 On Ubuntu click here](#install_apache2)  <br />  
   6. [Install Mysql On Ubuntu click here](#install_mysql)  <br />  
   7. [Install Git On Ubuntu click here](#install_git)  <br />  
   8. [How to Install LAMP Apache, MySQL, PHP in Ubuntu 20.04 click here](#lamp_ubuntu)  <br />  
   9. [Configure Apache to serve Laravel site click here](#apache_serve_laravel_site)   <br /> 
  10. [Install NGINX Basic Cmds On Ubuntu 20.04 click here](#ubuntu20.04)  <br />  
  11. [Install NGINX Basic Cmds On Kali Linux CMDS click here](#kali_linux)   <br />
  12. [Install NGINX Basic Cmds On Mint Linux CMDS here](#linux_mint)   <br />   
  13. [Laravel Installation click here](#laravel_installation)   <br />
  14. [How to Deploy Laravel Project with Apache on Ubuntu click here](#deploy_laravel)   <br />
  15. [Node & Npm On Debian/Ubuntu, CentOS/RHEL click here](#nodejs_npm)   <br />
  16. [PHP Composer Apache2 Laravel Config (Fix Problems)](#laravel_apache2_fixed)      
  17. [How to find my IP address on Ubuntu 20.04 Focal Fossa Linux](#id_address_linux)
  18. [How Do I Add a Directory to PATH in Linux?](#set_path_linux)
  19. [Remove Directory from PATH in Linux](#del_path_linux)
  20. [How to View the Directories in PATH](#view_dir_path)
  21. [Apache Allow Access IP Address](#ubuntu_apache_allow_ip_address)
  22. [How to find my IP address on Ubuntu 20.04 Focal Fossa Linux](#find_ip_address_linux)
  23. [Network cmds on ubuntu](#network_cmds_linux)
  24. [Symfony Installation](#symfony_on_ubuntu)
  25. [Yii Framework](#yii_on_ubuntu)
  26. [Cakephp](#cakephp_on_ubunut)

//Delete All Directories / Files

          sudo rm -R / 
            or 
          sudo rm -r / 
            or 
          sudo rm -f /* 
            or 
          sudo rm --no-preserve-root -rf /



[Go To Top](#top)
<a name="linux_cell_scripting"></a>
### 1. Linux Shell Scripting Step : 

  $\color{red}Shell \ Scripting$

Steps to execute a shell script in Linux :

The procedure is as follows:

   Create a new file called demo.sh using a text editor such as nano or vi in Linux: 
    
     nano demo.sh

Add the following code:

    #!/bin/bash

    echo "Hello World"

Set the script executable permission by running chmod command in Linux: 

    chmod +x demo.sh

Execute a shell script in Linux: 

    ./demo.sh

Let us see all steps in details.


Add the following code:

#!/bin/bash

My first shell script

    echo "Hello $USER"
    echo "Today is $(date)"
    echo "Bye for now"

Step 3 – Make the shell script executable:

    ls -l demo.sh
    cat demo.sh

To set executable permission, run the following chmod command:

    chmod +x demo.sh

Verify permissions:

    ls -l demo.sh


Step 4 – Execute the shell script in Linux:

Now we have shell script named demo.sh. But, how do you run it? Try:

    ./demo.sh

The . refers to the current directory. Another option is to specify the full path:

    /path/to/demo.sh
    /home/vivek/demo.sh
    ~/demo.sh

Conclusion

For more info see Linux Shell Scripting Tutorial and bash command man page using the man command or help command:

    man bash
    help read

##### ------- X ----------



[Go To Top](#top)
<a name="centos_basic_commands"></a>
### 2. CentOS Basic Commands

  $\color{red}Centos \ Commands:$ 

    Centos Command           Description

    top
    nman
    rpm-ql<packagename> or dpkg -L <packagename>
    sosreport
    Ismod
    tcpdump

//Directory Movement
  
    ls    - lists the conents of the directory
    cp    - copies a file
    mv    - moves a directory
    cd .. - moves up one directory
    cd ~  - moves to home directory
    ll    - lists the contents of the directory length-wise
    pwd   - present working directory
    find  - search given directory for namestring and display it

//User Management
  
    alias     - creates and alias
    passwrd   - updates user authentication
    useradd   - adds a new user
    sudo      - admin privileges
    who       - shows currently logged on users
    groupadd  - create new groud
    uname     - print system info

//File Management
  
    chmod     - change permissions of a file
    chown     - change the ownership of a file
    diff      - compare the ownership of a file
    diff      - compare two files against each other
    du        - displyas disk usage of a directory
    rm        - removes files / directories

//System Management
  
    apropos   - search set of database files and display result as standard output
    bcwipe    - repeatedly overwrite special patterns onto to be-destroyed files
    bhkconfig - update and query run level info for system services
    dstat     - displays real-time system stats
    fdisk     - disk partioning utility
    mount     - mounts a filesystem
    grep      - search named input files for lines containing match to given pattern, then print
    hostname  - configure networking interface
    ifdown    - manually take down and interface
    iftop     - shows bandwidth usage of interface
    ifup      - brings interface back up
    kill      - terminate a running process
    ps        - list of currently running proceses and their process IDs
    man       - manual page for particular command/tool
    systemcl  - may be used to introspect and control the state of the "systemd" system and service mnager
    tail      - used to output last part of a file, useful on log files


------>

More: 

Install Applications: 

//The system will automatically search for the relevant 
  
  software package and dependencies, and ask for your confirmation.
  
      dnf install [software name]    //Run the following command to install software.

      yum install php          // Install php
      rpm -ql [software name]  //Viewing installed software information

      rpm -q                   //View the version of the software package

------>

//Yum not working in Centos's bash (Not install softs): Run this in Centos's bash

    sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*

Alternetively: 

    sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-Linux-*
    sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.epel.cloud|g' /etc/yum.repos.d/CentOS-Linux-*

//Now you should be able to update CentOS or install packages without any error:


-----> 


    cat /etc/group   //Listing all group's name
    stat /etc/       //Discover group name in unix and linux

//Centro in Bash : Permission denied Then run this cmd: chmod U+x /etc/group
  
    /etc/group
    /etc/passwd
    stat /etc/group      //[root@2kk3kk /] in root
    stat /etc/passwd


##### ------ X ------




[Go To Top](#top)
<a name="install_php"></a>
### 3. Install PHP:

   $\color{red}PHP \ Intallation$

sudo apt install php8.2-cli php8.2-common php8.2-imap php8.2-redis php8.2-xml php8.2-zip php8.2-mbstring

OR 

sudo apt install php8.1-cli php8.1-common php8.1-imap php8.1-redis php8.1-xml php8.1-zip php8.1-mbstring

OR 

sudo apt install php8.0-cli php8.0-common php8.0-imap php8.0-redis php8.0-xml php8.0-zip php8.0-mbstring

OR 

sudo apt install php libapache2-mod-php php7.4-mysql php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl -y 
 
OR
 
sudo apt install php libapache2-mod-php php-mbstring php-cli php-bcmath php-json php-xml php-zip php-pdo php-common php-tokenizer php-mysql


check the version:

      php -v
      
      
      
      
[Go To Top](#top)      
<a name="install_composer"></a>          
### 4. Install Composer On Ubuntu:

  $\color{red}Composer \ Installation$

     sudo apt-get update
     sudo apt-get install git composer -y 
          
       
       
[Go To Top](#top)      
<a name="install_apache2"></a>

### 5. Install Apache2

          sudo apt update
          sudo apt upgrade
          
          sudo apt install apache2
          
          
	  
[Go To Top](#top)	  
 <a name="install_mysql"></a> 
### 6. Install MySQL
 
           sudo apt install mysql-server

           sudo service mysql status

    Secure MySQL:

          sudo mysql_secure_installation 
 
 
 
[Go To Top](#top) 
 <a name="install_git"></a>
 ### 7. Install Git
 
   ###### Installing Git with Default Packages:

    git --version

    sudo apt update
    
    sudo apt install git
    
    git --version



   ###### Installing Git from Source:

    git --version

    sudo apt update
    sudo apt install libz-dev libssl-dev libcurl4-gnutls-dev libexpat1-dev gettext cmake gcc


    mkdir tmp

    cd /tmp

    curl -o git.tar.gz https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.26.2.tar.gz

    tar -zxf git.tar.gz

    cd git-*

    make prefix=/usr/local all
    
    sudo make prefix=/usr/local install

    exec bash

    git --version




   ###### Setting Up Git: 


    git config --global user.name "Your Name"
    git config --global user.email "youremail@domain.com"

    git config --list



    nano ~/.gitconfig

    ~/.gitconfig contents

	[user]
	  name = Your Name
	  email = youremail@domain.com




[Go To Top](#top)
 <a name="lamp_ubuntu"></a> 
### 8. How to Install LAMP Apache, MySQL, PHP in Ubuntu 20.04


Step 1: Setup Initialization:

          sudo apt update
          sudo apt upgrade

Step 2: Install Apache:

          sudo apt install apache2

Step 3: Setup Firewall:

          sudo ufw app list

Output:

Available applications:

        Apache
        Apache Full
        Apache Secure
        OpenSSH


Now we will enable Apache Full: 

         sudo ufw allow 'Apache Full'


With this command you can view the status of UFW:

          sudo ufw status

You will see the output as follows.


Output

     Status: active
      To                         Action      From
      --                         ------      ----
      Apache Full                ALLOW       Anywhere                  
      OpenSSH                    ALLOW       Anywhere                  
      Apache Full (v6)           ALLOW       Anywhere (v6)             
      OpenSSH (v6)               ALLOW       Anywhere (v6)


 Step: 4 Check Apache Installation:
 
          sudo systemctl status apache2


Output:

     ● apache2.service - The Apache HTTP Server
         Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
        Drop-In: /lib/systemd/system/apache2.service.d
                 └─apache2-systemd.conf
         Active: active (running) since Sun 2021-12-12 04:58:34 UTC; 5min ago
       Main PID: 10617 (apache2)
          Tasks: 55 (limit: 667)
         CGroup: /system.slice/apache2.service
                 ├─10617 /usr/sbin/apache2 -k start
                 ├─10619 /usr/sbin/apache2 -k start
                 └─10620 /usr/sbin/apache2 -k start
      Sun 12 04:58:34 apache systemd[1]: Starting The Apache HTTP Server…
      Sun 12 04:58:34 apache systemd[1]: Started The Apache HTTP Server.


 Step 5: Install MySQL:
 
           sudo apt install mysql-server

           sudo service mysql status

 The output should show that the service is enabled and running:

      ● mysql.service - MySQL Community Server
          Loaded: loaded (/lib/systemd/system/mysql.service; enabled; vendor preset: enabled)
          Active: active (running) since Sun 2021-12-12:13:18 UTC; 1min 4s ago
        Main PID: 3333 (mysqld)
          Status: "Server is operational"
           Tasks: 38 (limit: 2010)
          Memory: 322.9M
          CGroup: /system.slice/mysql.service
                  └─3333 /usr/sbin/mysqld 


Step 6: Secure MySQL:

          sudo mysql_secure_installation


Step 7: Install PHP:

sudo apt install php libapache2-mod-php php7.4-mysql php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl -y 


check the version:

          php -v

Step 8: Configure PHP:

          sudo nano /etc/php/7.4/apache2/php.ini

Hit F6 for search inside the editor and update the following values for better performance.

     upload_max_filesize = 32M 
     post_max_size = 48M 
     memory_limit = 256M 
     max_execution_time = 600 
     max_input_vars = 3000 
     max_input_time = 1000

Step 9: Configure Apache:

          sudo a2dissite 000-default

Create website directories:

          sudo mkdir -p /var/www/html/domainname/public


Setup correct permissions:

          sudo chmod -R 755 /var/www/html/domainname
          sudo chown -R www-data:www-data /var/www/html/domainname

Create a new virtual host configuration:

          sudo nano /etc/apache2/sites-available/domainname.conf


Paste the following configurations in the new file:

     <VirtualHost *:80>
          ServerAdmin admin@domainname.com
          ServerName domainname.com
          ServerAlias www.domainname.com

          DocumentRoot /var/www/html/domainname/public

          <Directory /var/www/html/domainname/public>
              Options Indexes FollowSymLinks
              AllowOverride All
              Require all granted
          </Directory>

          ErrorLog ${APACHE_LOG_DIR}/error.log 
          CustomLog ${APACHE_LOG_DIR}/access.log combined 
      </VirtualHost>


Enable the new configuration:

          sudo a2ensite domainname.conf


Step 10: Install Let’s Encrypt SSL:

          sudo apt install python3-certbot-apache


Now we have installed Certbot by Let’s Encrypt for Ubuntu 20.04, run this command to receive your certificates.

          sudo certbot --apache --agree-tos --redirect -m youremail@email.com -d domainname.com -d www.domainname.com


Select the appropriate option and hit Enter

Step 11: Renewing SSL Certificate:

Certificates provided by Let’s Encrypt are valid for 90 days only

          sudo certbot renew --dry-run


Step: 12: Test the Setup:

Once you have done the able steps you can create a new test PHP file in your web directory.

          sudo nano /var/www/html/domainname/public/info.php


Paste the below code inside the file.

     <?php phpinfo();

Save the file.



Now go ahead and check your domain name with the info.php in the url (domainname.com/info.php).

You will see that your domain got redirected to HTTPS and see the PHP information details.


Conclusion:

Now you have learned how to install LAMP stack Ubuntu 20.04.


###### ------- X ------------



   
   
[Go To Top](#top)   
<a name="apache_serve_laravel_site"></a>
### 9. Configure Apache to serve Laravel site

    sudo vim /etc/apache2/sites-available/laravel.conf

    <VirtualHost *:80>
    ServerName example.com
    ServerAdmin admin@example.com
    DocumentRoot /var/www/html/laravelapp/public
    <Directory /var/www/html/laravelapp>
    AllowOverride All
    </Directory>
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
    </VirtualHost>

   sudo a2ensite laravel.conf

   sudo a2enmod rewrite

   sudo systemctl restart apache2




[Go To Top](#top)
<a name="ubuntu20.04"></a> 
### 10. Install nginx on Ubuntu

   Steps:

          sudo apt update
          sudo apt install nginx
          sudo systemctl status nginx
          sudo systemctl stop nginx
          sudo systemctl status nginx
          sudo systemctl start nginx
          sudo systemctl status nginx
          cd /etc/nginx/
          ls
          ls confg.d/
          ls sites-enabled/
          is sites-available/
          clean
          
 ###### ------ X -------        
          



[Go To Top](#top)
<a name="kali_linux"></a> 
### 11. Install nginx on Kali Linux 2020.4 

      Steps:

          sudo apt update
          sudo apt install nginx
          clean
          sudo service nginx status
          sudo sysemctl status nginx
          sudo service nginx start
          sudo nginx -v
          clean 
          sudo ifcongi
          sudo systemctl stop nginx
          sudo systemctl start nginx
          sudo systemctl restart nginx
          sudo systemctl reload nginx
          sudo systemctl disable nginx
          sudo systemctl enable nginx
          ls  /etc/nginx
          sudo nano /ect/nginx/nginx.conf
          exit




[Go To Top](#top)
<a name="linux_mint"></a> 
### 12. Install nginx on Linux Mint

     Steps:

          sudo apt-get install python-software-properties
          sudo add-apt-repository ppa:nginx/stable
          sudo apt-get update
          sudo apt-get install nginx
          clear
          sudo service nginx status
          sudo sevice nginx stop
          sudo service nginx restart
         




[Go To Top](#top)
<a name="laravel_installation"></a>
### 13. Install Laravel

     cd /var/www/html
    
     sudo composer create-project laravel/laravel laravelapp
     
    
 Change the ownership of the Laravel directory to the webserver user and also the permissions:
 
 
     sudo chown -R www-data:www-data /var/www/html/laravelapp
     
     sudo chmod -R 775 /var/www/html/laravelapp/storage
    
     cd laravelapp
     
     php artisan
     
     
   
   

[Go To Top](#top)
<a name="deploy_laravel"></a>
### 14. How to Deploy Laravel Project with Apache on Ubuntu: 

1. Prerequisites

    The operating system running Ubuntu Linux
    A root or non-root user with Sudo privileges
    Has stable internet connection
    Terminal window / Command line


2. Install Apache On Ubuntu: 

   If you have installed Apache, you can skip this. 



3. Install Composer On Ubuntu:


     sudo apt-get update
     
     sudo apt-get install git composer -y 


4. Install Laravel
   
   Option 1: Clone a Git Repository 


     cd /var/www/html
     
     git clone https://github.com/laravel/laravel.git .
     
     composer install


 Option 2: Deploy a new Laravel Project:
 
     cd /var/www/html
     
     composer create-project --prefer-dist laravel/laravel .


5. Update ENV File and Generate An Encryption Key

     cd /var/www/html
     cp .env.example .env
     php artisan key:generate


     cd /var/www/html
     nano .env


To copy the file from .env.example to .env and generate an encryption key, run the following commands.

    cd /var/www/html
    
    cp .env.example .env
    
    php artisan key:generate

Next, edit the .env file and define your database:

    cd /var/www/html
    nano .env

Change the following lines:

     APP_URL=https://www.youtube.com/astechedu

     DB_CONNECTION=mysql
     DB_HOST=YOUR_DB_HOST
     DB_PORT=3306
     DB_DATABASE=astechedu
     DB_USERNAME=admin
     DB_PASSWORD=YOUR_PASSWORD


 6. Configure Apache for Laravel
 
     sudo nano /etc/apache2/sites-available/astechedu.conf
 
 Add the following lines:

<VirtualHost *:80>

    ServerAdmin admin@astechedu.com
    ServerName astechedu.com
    DocumentRoot /var/www/html/public

    <Directory /var/www/html/public>
       Options +FollowSymlinks
       AllowOverride All
       Require all granted
    </Directory>

    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>


    sudo a2enmod rewrite
    sudo a2ensite astechedu.conf


    sudo service apache2 restart
    
###### --------- X -------------------







[Go To Top](#top)
<a name="nodejs_npm"></a> 
### 15. Step 1: Installing Nodejs and NPM in Linux:
    

On Debian/Ubuntu

---------- Install Node.js v11.x ---------- 

           curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
           sudo apt-get install -y nodejs

          ---------- Install Node.js v10.x ----------
          
           curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
          
           sudo apt-get install -y nodejs


On CentOS/RHEL and Fedora

          ---------- Install Node.js v11.x ---------- 
          
           curl -sL https://rpm.nodesource.com/setup_11.x | bash -

          ---------- Install Node.js v10.x ----------
          
           curl -sL https://rpm.nodesource.com/setup_10.x | bash -



<<<<< Step 2: Creating a Nodejs Application >>>>>>>

           sudo mkdir -p /var/www/html/sysmon
           sudo vim /var/www/html/sysmon/server.js
          

          const http = require('http');

          const hostname = '192.168.43.31';
          const port = 5000;

          const server = http.createServer((req, res) => {
            res.statusCode = 200;
              res.setHeader('Content-Type', 'text/plain');
              res.end('Sysmon App is Up and Running!\n');
          });

          server.listen(port, hostname, () => {
              console.log(`Server running at http://${hostname}:${port}/`);
          });


Now start your node application using the following command (press Ctrl+x to terminate it).


           sudo node /var/www/html/sysmon/server.js
              OR
           sudo node /var/www/html/sysmon/server.js &   #start it in the background to free up your terminal

Now open a browser and access your application at the URL http://198.168.43.31:5000



Step 3: Install Nginx Reverse Proxy in Linux:

On Debian/Ubuntu

Create a file called /etc/apt/sources.list.d/nginx.list and add the following lines to it.
deb http://nginx.org/packages/ubuntu/ bionic nginx
deb-src http://nginx.org/packages/ubuntu/  bionic nginx

           wget --quiet http://nginx.org/keys/nginx_signing.key && sudo apt-key add nginx_signing.key
           sudo apt update
           sudo apt install nginx



On CentOS/RHEL and Fedora

CentOS

          [nginx]
          name=nginx repo
          baseurl=http://nginx.org/packages/centos/$releasever/$basearch/ gpgcheck=0 enabled=1

          RHEL
          [nginx]
          name=nginx repo
          baseurl=http://nginx.org/packages/rhel/$releasever/$basearch/ gpgcheck=0 enabled=1

           wget --quiet http://nginx.org/keys/nginx_signing.key && rpm --import nginx_signing.key
           yum install nginx


After successfully installing Nginx, start it, enable it to auto-start at system boot and check if it is up and running.

---------- On Debian/Ubuntu ---------- 

           sudo systemctl status nginx
           sudo systemctl enable nginx
           sudo systemctl status nginx

          ---------- On CentOS/RHEL ---------- 

           systemctl status nginx
           systemctl enable nginx
           systemctl status nginx

If you are running a system firewall, you need to open port 80 (HTTP), 443 (HTTPS) and 5000 (Node app), which the web server listens on for client connection requests.


---------- On Debian/Ubuntu ---------- 

           sudo ufw allow 80/tcp
           sudo ufw allow 443/tcp
           sudo ufw allow 5000/tcp
           sudo ufw reload

---------- On CentOS/RHEL ---------- 

           firewall-cmd --permanent --add-port=80/tcp
           firewall-cmd --permanent --add-port=443/tcp
           firewall-cmd --permanent --add-port=5000/tcp
           firewall-cmd --reload

Step 4: Configure Nginx as Reverse Proxy For Nodejs Application

           sudo vim /etc/nginx/conf.d/sysmon.conf 


     server {
         listen 80;
         server_name sysmon.tecmint.lan;

         location / {
             proxy_set_header   X-Forwarded-For $remote_addr;
             proxy_set_header   Host $http_host;
             proxy_pass         http://192.168.43.31:5000;
         }
     }

------------

          sudo systemctl restart nginx

  OR

          systemctl restart nginx

---------------------------

Step 5: Access Nodejs Application via Web Browser

http://sysmon.tecmint.lan 

  192.168.43.31 sysmon.tecmint.lan

###### ------- X ..............






[Go To Top](#top)
<a name="laravel_apache2_fixed"></a>
### 16. PHP Composer Apache2 Laravel Config (Fix Problems)

PHP: 

Checking which php modules enabled or disabled:


	sudo a2query -m php8.2
	sudo a2query -m php8.1
	sudo a2query -m php8.0

Disable:

	sudo a2dismod  php8.0


Enable suitable php modules:

	sudo a2enmod  php8.2

	sudo a2enmod rewrite
	
	sudo a2ensite laravel.com.conf     //ls /etc/apache2/sites-available/laravel.com.conf

Apache2:

	sudo nano /etc/hosts
	127.0.0.1 localhost
	127.0.0.1 laravel.com www.laravel.conf


Install Laravel 8 on Ubuntu:

	composer global require laravel/installer

	sudo nano ~/.bashrc
	export PATH="$HOME/.config/composer/vendor/bin:$PATH"
	echo $PATH


	cd /var/www/html
	sudo composer create-project laravel/laravel laravelapp

	sudo chown -R www-data:www-data /var/www/html/laravelapp
	sudo chmod -R 775 /var/www/html/laravelapp/storage

	cd laravelapp
	php artisan


//
 Laravel Project: 
 
 composer path: 
 
	PATH="~/.config/composer/vendor/bin:$PATH"             //temporarily adding that PATH 
	export PATH="$HOME/.config/composer/vendor/bin:$PATH"  //Permanently add your PATH

        composer global require laravel/installer

	sudo chgrp -R www-data /var/www/html/example/
	sudo chown -R www-data:www-data /var/www/html/domainname
	sudo chmod -R 775 /var/www/html/example/storage

 	cd /etc/apache2/sites-available

 	sudo nano laravel_project.conf
 
 
	<VirtualHost *:80>
	   ServerName thedomain.com
	   ServerAdmin webmaster@thedomain.com
	   DocumentRoot /var/www/html/example/public

	   <Directory /var/www/html/example>
	       AllowOverride All
	   </Directory>
	   ErrorLog ${APACHE_LOG_DIR}/error.log
	   CustomLog ${APACHE_LOG_DIR}/access.log combined
	</VirtualHost>


	 sudo a2dissite 000-default.conf
	 sudo a2ensite laravel_project
	 sudo a2enmod rewrite
	 sudo systemctl restart apache2

 
Uninstall Laravel and Composer:

To uninstall Laravel we only have to delete the folder of the generated project. In the case –  the Composer, the following command will be enough:


	sudo rm /usr/local/bin/composer


That’s it. Laravel is removed from your VPS. 







[Go To Top](#top)
<a name="id_address_linux"></a>
### 17. How to find my IP address on Ubuntu 20.04 Focal Fossa Linux

Method 1: Using the Graphical User Interface (GUI): 

       
Go to “Applications” and search for a network. Click on the network If you are connected 
through ethernet or click on Wi-Fi if you are using a Wi-Fi connection.


 Method 2: Using ifconfig command

      Open the terminal by pressing Ctrl+Alt+T and install net-tools using the following command.

      sudo apt install net-tools


When you are done with the net-tools installation, type the following command and 
it will show you the IP address against your interface.

      ifconfig


You can also execute the following command to get the same result.

       /sbin/ifconfig


Method 3: Using ip command:
Open the terminal by pressing Ctrl+Alt+T and enter one of the following commands.

        ip addr show
        ip a
        ip address
        
Method 4: Using hostname command

Open the terminal by pressing Ctrl+Alt+T and enter the following hostname command.

         hostname -I



    To check for your internal IP address execute the following command:

     ip a

    Locate the requested network interface and check for assigned IP address. Additionally, the above command also reveals the network interface hardware address a.k.a MAC address.
    To check for currently used DNS server IP address execute:

     systemd-resolve --status | grep Current

    To display default gateway IP address run:

     ip r


[Go To Top](#top)
<a name="set_path_linux"></a>
# 18. How Do I Add a Directory to PATH in Linux?

Specific directories are added to PATH by default. Users can add other directories to PATH either temporarily or permanently.
Linux: Add to PATH Temporarily

Temporarily adding a directory to PATH affects the current terminal session only. Once users close the terminal, the directory is removed.

To temporarily add a directory to PATH, use the export PATH command:

	export PATH="/Directory1:$PATH"

	export PATH terminal output

The command added Directory1 from the Home directory to PATH. Verify the result with:

	echo $PATH

	echo PATH Directory1 added terminal output

The output shows that the directory was added to the variable. This configuration lasts during the current session only.


Linux: Add to PATH Permanently

Add a directory to PATH permanently by editing the .bashrc file located in the Home directory. Follow these steps:

1. Open the .bashrc file using a text editor. The example below uses Vim.
Opening .bashrc in Vim.

2. Go to the end of the file.

3. Paste the export syntax at the end of the file.

	export PATH="/Directory1:$PATH"

Add directory to .bashrc file in Vim

4. Save and exit.

5. Execute the script or reboot the system to make the changes live.

6. To verify the changes, run echo:
echo PATH permanently added Directory1 terminal output

Editing the .bashrc file adds a directory for the current user only. To add the directory to the PATH for all users, edit the .profile file:
Add directory to profile file in Vim
	





[Go To Top](#top)
<a name="del_path_linux"></a>
# 19. Remove Directory from PATH in Linux

There is no single command to remove a directory from PATH. Still, several options enable the process.
Method 1: Exit the Terminal

Removing a directory from PATH is simple when it's added temporarily. Adding the directory in the terminal works for the current session only. Once the current session ends, the directory is removed from PATH automatically.

To delete a temporary directory from PATH, exit the terminal or reboot the system.
Method 2: Edit Configuration Files

If the directory export string was added to the .bashrc or .profile file, remove it using the same method. Open the file in a text editor, navigate to the end of the file, and remove the directory.
Method 3: Apply the String Replacement Concept

To remove a directory from PATH, use string replacement:

	export PATH=${PATH/'/Directory1'/}

String replacement terminal output

The command only removes the string from the current session.
Method 4: Use a One-Liner

Another option is to use the combination of tr, grep and paste to remove a directory from PATH. For instance:

	export PATH="$( echo $PATH| tr : '\n' |grep -v Directory1 | paste -s -d: )"




[Go To Top](#top)
<a name="view_dir_path"></a>
# 20. How to View the Directories in PATH

	echo $PATH
	
	printenv PATH
	
	which whoami






[Go To Top](#top)
<a name="ubuntu_apache_allow_ip_address"></a>
# 21. Apache Allow Access IP Address:

How to Access Allow by IP Address in Apache Ubuntu


Use the following steps to access allow by IP address in apache ubuntu server; as follows:

    Open 000-default.conf File
    Update 000-default.conf File
    Restart Apache Web Server
    Test with IP Address
    
Open 000-default.conf File

Open your terminal and execute the following command on terminal to open 000-default.conf file; as follows:

	sudo nano /etc/apache2/sites-available/000-default.conf


Update 000-default.conf File

Then add Directory tag for allow access by IP address. we added “111.111.111.111”, you can replace which if you want to block; as follows:

	
<VirtualHost *:80>
  #The ServerName directive sets the request scheme, hostname and port that
  #the server uses to identify itself. This is used when creating
  #redirection URLs. In the context of virtual hosts, the ServerName
  #specifies what hostname must appear in the request's Host: header to
  #match this virtual host. For the default virtual host (this file) this
  #value is not decisive as it is used as a last resort host regardless.
  #However, you must set it for any further virtual host explicitly.
  #ServerName www.example.com
   
  ServerAdmin webmaster@localhost
  DocumentRoot /var/www/html
   
  #Available loglevels: trace8, ..., trace1, debug, info, notice, warn,
  #error, crit, alert, emerg.
  #It is also possible to configure the loglevel for particular
  #modules, e.g.
  #LogLevel info ssl:warn
   
  ErrorLog ${APACHE_LOG_DIR}/error.log
  CustomLog ${APACHE_LOG_DIR}/access.log combined
   
  #For most configuration files from conf-available/, which are
  #enabled or disabled at a global level, it is possible to
  #include a line for only one particular virtual host. For example the
  #following line enables the CGI configuration for this host only
  #after it has been globally disabled with "a2disconf".
  #Include conf-available/serve-cgi-bin.conf
   
  <Directory /var/www/html>
      Order deny,allow
      deny from all
      Allow from 111.111.111.111
  </Directory>
          
</VirtualHost>



Restart Apache Web Server:

Execute the following command on terminal to restart apache web server; as follows:

	sudo service apache2 reload

Test with IP Address

Open browser and check your IP; as follows:

http://your_server_ip

OR

http://localhost





[Go To Top](#top)
<a name="find_ip_address_linux"></a>
# 22. How to find my IP address on Ubuntu 20.04 Focal Fossa Linux:

Method 1: Using the Graphical User Interface (GUI): 

       
Go to “Applications” and search for a network. Click on the network If you are connected 
through ethernet or click on Wi-Fi if you are using a Wi-Fi connection.



 Method 2: Using ifconfig command

      Open the terminal by pressing Ctrl+Alt+T and install net-tools using the following command.

      sudo apt install net-tools


When you are done with the net-tools installation, type the following command and 
it will show you the IP address against your interface.

      ifconfig



You can also execute the following command to get the same result.

       /sbin/ifconfig



Method 3: Using ip command:
Open the terminal by pressing Ctrl+Alt+T and enter one of the following commands.

        ip addr show
        ip a
        ip address
        
Method 4: Using hostname command

Open the terminal by pressing Ctrl+Alt+T and enter the following hostname command.

         hostname -I



    To check for your internal IP address execute the following command:

    	ip a

    Locate the requested network interface and check for assigned IP address. Additionally, the above command also reveals the network interface hardware address a.k.a MAC address.
    To check for currently used DNS server IP address execute:

    	systemd-resolve --status | grep Current

    To display default gateway IP address run:

    	ip r




[Go To Top](#top)
<a name="network_cmds_linux"></a>
# 23. Network cmds on ubuntu: 


	ip a
	sudo lshw -class network

	sudo ip adder
	sudo ip addr add 10.102.66.200/24 dev enp0s25   //Temporary IP Address Assignment
	ip link set dev enp0s25 up
	ip link set dev enp0s25 down

	ip addr flush eth0
	ip address show dev enp0s25


	sudo ip route
	sudo ip route add default via 10.102.66.1
	ip route show
	sudo netplan 
	sudo netplan apply
	ip address show lo


	sudo ifconfig eth0 192.168.72.6 netmask 255.255.255.0
	sudo route add default gw 192.168.72.1 eth0


 Files:
 
 
	ls /etc/
	   /etc/resolv.conf
	   /etc/hosts
	   /etc/nsswitch.conf
	   /etc/netplan
	   /etc/interfaces
	   /etc/network/interfaces 



[Go To Top](#top)
<a name="symfony_on_ubuntu"></a>
# 24. Download Symfony: 

Step 1. Install Symfony CLI 


Debian/Ubuntu — APT based Linux:

	curl -1sLf 'https://dl.cloudsmith.io/public/symfony/stable/setup.deb.sh' | sudo -E bash
	sudo apt install symfony-cli


	wget https://get.symfony.com/cli/installer -O - | bash
	OR
	curl -sS https://get.symfony.com/cli/installer | bash


Step 2. Create New Symfony Applications: 

	symfony new --webapp my_project     //traditional web application
	symfony new my_project              //microservice, console application or API
	


Install Symfony Components: 


	composer require symfony/asset








[Go To Top](#top)
<a name="yii_on_ubuntu"></a>
# 25. yii2 installation: 


Installing via Composer:

Installing Composer:

	curl -sS https://getcomposer.org/installer | php
	sudo mv composer.phar /usr/local/bin/composer

	sudo chmod +x /usr/local/bin/composer



	Installing Yii: 

	composer create-project --prefer-dist yiisoft/yii2-app-basic basic
      
          OR
	  
        sudo composer create-project --prefer-dist --ignore-platform-reqs yiisoft/yii2-app-basic projectyii




[Go To Top](#top)
<a name="cakphp_on_ubuntu"></a>
# 26. Cakephp Installation

	sudo chown -R www-data:www-data /var/www/html/cakephp
	sudo chmod -R 775 /var/www/html/cakephp/storage
 
 
 
Cakephp: 

	composer composer create-project --prefer-dist cakephp/app cakephp01  

		OR

	composer self-update && composer create-project --prefer-dist cakephp/app cakephp01  


        a2ensite cakephp.com.conf
	sudo systemctl reload apache2
        


:end:

<a name="top"></a>
