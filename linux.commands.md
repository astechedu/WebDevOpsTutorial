
# Linux Basic Commands 
  

Topics <br /> : 

   1. [Linux Cell Scripting click here](#linux_cell_scripting)   <br />
   2. [CentOS Basic Commands click here](#centos_basic_commands)   <br />
   3. [Install PHP On Ubuntu click here](#install_php)  <br /> 
   4. [Install Composer On Ubuntu click here](#install_composer)  <br />
   5. [Install Apache2 On Ubuntu click here](#install_apache2)  <br />  
   6. [Install Mysql On Ubuntu click here](#install_mysql)  <br />  
   7. [How to Install LAMP Apache, MySQL, PHP in Ubuntu 20.04 click here](#lamp_ubuntu)  <br />   
   8. [Install NGINX Basic Cmds On Ubuntu 20.04 click here](#ubuntu20.04)  <br />  
   9. [Install NGINX Basic Cmds On Kali Linux CMDS click here](#kali_linux)   <br />
  10. [Install NGINX Basic Cmds On Mint Linux CMDS here](#linux_mint)   <br />   
  11. [Laravel Installation click here](#laravel_installation)   <br />
  12. [How to Deploy Laravel Project with Apache on Ubuntu click here](#deploy_laravel)   <br />
  13. [Node & Npm On Debian/Ubuntu, CentOS/RHEL click here](#nodejs_npm)   <br />


//Delete All Directories / Files

          sudo rm -R / 
            or 
          sudo rm -r / 
            or 
          sudo rm -f /* 
            or 
          sudo rm --no-preserve-root -rf /



<a name="linux_cell_scripting"></a>
### 1. Linux Shell Scripting Steps: 


Steps to execute a shell script in Linux:

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

# My first shell script
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




<a name="centos_basic_commands"></a>
### 2. CentOS Basic Commands

//Centos Commands: 

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



<a name="install_php"></a>
### 3. Install PHP:

sudo apt install php libapache2-mod-php php7.4-mysql php7.4-common php7.4-mysql php7.4-xml php7.4-xmlrpc php7.4-curl php7.4-gd php7.4-imagick php7.4-cli php7.4-dev php7.4-imap php7.4-mbstring php7.4-opcache php7.4-soap php7.4-zip php7.4-intl -y 


check the version:

         php -v
      
      
      
<a name="install_composer"></a>          
### 4. Install Composer On Ubuntu:


     sudo apt-get update
     sudo apt-get install git composer -y 
          
       
       
<a name="install_apache2"></a>

### 5. Install Apache2

          sudo apt update
          sudo apt upgrade
          
          sudo apt install apache2
          
          
 <a name="install_mysql"></a> 
### 6. Install MySQL
 
           sudo apt install mysql-server

           sudo service mysql status

    Secure MySQL:

          sudo mysql_secure_installation 
 
 
 <a name="lamp_ubuntu"></a> 
 

### 7. How to Install LAMP Apache, MySQL, PHP in Ubuntu 20.04


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


<a name="ubuntu20.04"></a> 
### 8. Install nginx on Ubuntu

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
          
          
<a name="kali_linux"></a> 
### 9. Install nginx on Kali Linux 2020.4 

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



<a name="linux_mint"></a> 
### 10. Install nginx on Linux Mint

     Steps:

          sudo apt-get install python-software-properties
          sudo add-apt-repository ppa:nginx/stable
          sudo apt-get update
          sudo apt-get install nginx
          clear
          sudo service nginx status
          sudo sevice nginx stop
          sudo service nginx restart
         



<a name="deploy_laravel"></a>
### 12. How to Deploy Laravel Project with Apache on Ubuntu: 

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

     APP_URL=https://techvblogs.com

     DB_CONNECTION=mysql
     DB_HOST=YOUR_DB_HOST
     DB_PORT=3306
     DB_DATABASE=techvblogs
     DB_USERNAME=admin
     DB_PASSWORD=YOUR_PASSWORD


 6. Configure Apache for Laravel
 
     sudo nano /etc/apache2/sites-available/techvblogs.conf
 
 Add the following lines:

<VirtualHost *:80>

    ServerAdmin admin@techvblogs.com
    ServerName techvblogs.com
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
    sudo a2ensite techvblogs.conf


    sudo service apache2 restart
    
###### --------- X -------------------



<a name="nodejs_npm"></a> 
### 13. Step 1: Installing Nodejs and NPM in Linux:


On Debian/Ubuntu

---------- Install Node.js v11.x ---------- 

          $ curl -sL https://deb.nodesource.com/setup_11.x | sudo -E bash -
          $ sudo apt-get install -y nodejs

          ---------- Install Node.js v10.x ----------
          
          $ curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
          
          $ sudo apt-get install -y nodejs


On CentOS/RHEL and Fedora

          ---------- Install Node.js v11.x ---------- 
          
          $ curl -sL https://rpm.nodesource.com/setup_11.x | bash -

          ---------- Install Node.js v10.x ----------
          
          $ curl -sL https://rpm.nodesource.com/setup_10.x | bash -



<<<<< Step 2: Creating a Nodejs Application >>>>>>>

          $ sudo mkdir -p /var/www/html/sysmon
          $ sudo vim /var/www/html/sysmon/server.js
          

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


          $ sudo node /var/www/html/sysmon/server.js
              OR
          $ sudo node /var/www/html/sysmon/server.js &   #start it in the background to free up your terminal

Now open a browser and access your application at the URL http://198.168.43.31:5000



Step 3: Install Nginx Reverse Proxy in Linux:

On Debian/Ubuntu

Create a file called /etc/apt/sources.list.d/nginx.list and add the following lines to it.
deb http://nginx.org/packages/ubuntu/ bionic nginx
deb-src http://nginx.org/packages/ubuntu/  bionic nginx

          $ wget --quiet http://nginx.org/keys/nginx_signing.key && sudo apt-key add nginx_signing.key
          $ sudo apt update
          $ sudo apt install nginx



On CentOS/RHEL and Fedora

CentOS

          [nginx]
          name=nginx repo
          baseurl=http://nginx.org/packages/centos/$releasever/$basearch/ gpgcheck=0 enabled=1

          RHEL
          [nginx]
          name=nginx repo
          baseurl=http://nginx.org/packages/rhel/$releasever/$basearch/ gpgcheck=0 enabled=1

          # wget --quiet http://nginx.org/keys/nginx_signing.key && rpm --import nginx_signing.key
          # yum install nginx


After successfully installing Nginx, start it, enable it to auto-start at system boot and check if it is up and running.

---------- On Debian/Ubuntu ---------- 

          $ sudo systemctl status nginx
          $ sudo systemctl enable nginx
          $ sudo systemctl status nginx

          ---------- On CentOS/RHEL ---------- 

          # systemctl status nginx
          # systemctl enable nginx
          # systemctl status nginx

If you are running a system firewall, you need to open port 80 (HTTP), 443 (HTTPS) and 5000 (Node app), which the web server listens on for client connection requests.


---------- On Debian/Ubuntu ---------- 

          $ sudo ufw allow 80/tcp
          $ sudo ufw allow 443/tcp
          $ sudo ufw allow 5000/tcp
          $ sudo ufw reload

---------- On CentOS/RHEL ---------- 

          # firewall-cmd --permanent --add-port=80/tcp
          # firewall-cmd --permanent --add-port=443/tcp
          # firewall-cmd --permanent --add-port=5000/tcp
          # firewall-cmd --reload

Step 4: Configure Nginx as Reverse Proxy For Nodejs Application

          $ sudo vim /etc/nginx/conf.d/sysmon.conf 


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


:end:
