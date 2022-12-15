
# Linux Basic Commands 
  

Topics: <br /> 

   1. [Linux Cell Scripting click here](#linux_cell_scripting)   <br />
   2. [CentOS Basic Commands click here](#centos_basic_commands)   <br />
   3. [Install PHP On Ubuntu click here](#install_php)  <br /> 
   4. [Install Composer On Ubuntu click here](#install_composer)  <br />
   5. [Install Apache2 On Ubuntu click here](#install_apache2)  <br />  
   6. [Install Mysql On Ubuntu click here](#install_mysql)  <br />  
   7. [Install $\color{red}Git$ On Ubuntu click here](#install_git)  <br />  
   8. [How to Install LAMP Apache, MySQL, PHP in Ubuntu 20.04 click here](#lamp_ubuntu)  <br />   
   9. [Install NGINX Basic Cmds On Ubuntu 20.04 click here](#ubuntu20.04)  <br />  
  10. [Install NGINX Basic Cmds On Kali Linux CMDS click here](#kali_linux)   <br />
  11. [Install NGINX Basic Cmds On Mint Linux CMDS here](#linux_mint)   <br />   
  12. [Laravel Installation click here](#laravel_installation)   <br />
  13. [How to Deploy Laravel Project with Apache on Ubuntu click here](#deploy_laravel)   <br />
  14. [Node & Npm On Debian/Ubuntu, CentOS/RHEL click here](#nodejs_npm)   <br />


//Delete All Directories / Files

          sudo rm -R / 
            or 
          sudo rm -r / 
            or 
          sudo rm -f /* 
            or 
          sudo rm --no-preserve-root -rf /



<a name="linux_cell_scripting"></a>
### 1. Linux Shell Scripting Step : 


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



   ###### Setting 
