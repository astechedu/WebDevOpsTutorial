$$\Large{\colorbox{black}{\color{white} Ansible For Beginners}}$$


[Home](all-file-links.md)

#
# Topics: 


   :link:[Ansible Installation on Linux Ubuntu 20.04/22.04, CentOS of Fedora, ](#ansible_installation)   
   
   :link:[Ansible Basic Terms](#ansible_basics)

   :link:[How to Install and Configure Ansible on CentOS](#ansible-on-centos)

   :link:[Examples of Playbook & Inventory](#ansible-playbook-inventory)

   :link:[Ansible Playbook to Exchange keys between hosts](#ssh-share)

  :link:[Some Configuration](#some-config)



#
<a name="some-config"></a>
# Some Configuration 

<!--Changing in file sudoers -->

	sudo nano /etc/sudoers
	ec2-user ALL=(ALL) NOPASSWD: ALL
	ajay ALL=(ALL) NOPASSWD: ALL


        sudo nano /etc/ssh/sshd_config
        PermitRootLogin yes






#
<a name="ansible_installation"></a>
# Installing Ansible On Linux Ubuntu, Fedora or CentOS:


 [Ansible Installation on Ubuntu](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)
 
 To configure the PPA on your system and install Ansible run these commands:

	sudo apt update
	sudo apt install software-properties-common
	sudo add-apt-repository --yes --update ppa:ansible/ansible
	sudo apt install ansible


 
 Fedora Or CentOS:
 
 [Installing Ansible on Fedora or CentOS](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html#installing-ansible-on-ubuntu)
 
 
 On Fedora:

	sudo dnf install ansible

On CentOS:

	sudo yum install epel-release
	sudo yum install ansible


 


:end:

#
OR
#
      sudo apt update
      
      sudo apt-add-repository ppa:ansible/ansible
      
      sudo apt update

      sudo apt install ansible

Setting Up the Inventory File:

      sudo nano /etc/ansible/hosts

Output:

   /etc/ansible/hosts

      [servers]
      server1 ansible_host=203.0.113.111
      server2 ansible_host=203.0.113.112
      server3 ansible_host=203.0.113.113

      [all:vars]
      ansible_python_interpreter=/usr/bin/python3



      ansible-inventory --list -y

Output:


      all:
        children:
          servers:
            hosts:
              server1:
                ansible_host: 203.0.113.111
                ansible_python_interpreter: /usr/bin/python3
              server2:
                ansible_host: 203.0.113.112
                ansible_python_interpreter: /usr/bin/python3
              server3:
                ansible_host: 203.0.113.113
                ansible_python_interpreter: /usr/bin/python3
          ungrouped: {}


Testing Connection:

      ansible all -m ping -u root
   
   
Output:

      server1 | SUCCESS => {
          "changed": false,
          "ping": "pong"
      }
      server2 | SUCCESS => {
          "changed": false,
          "ping": "pong"
      }
      server3 | SUCCESS => {
          "changed": false,
          "ping": "pong"
      } 

   
Running Ad-Hoc Commands (Optional): 

      ansible all -a "df -h" -u root



Output:

      server1 | CHANGED | rc=0 >>
      Filesystem      Size  Used Avail Use% Mounted on
      udev            3.9G     0  3.9G   0% /dev
      tmpfs           798M  624K  798M   1% /run
      /dev/vda1       155G  2.3G  153G   2% /
      tmpfs           3.9G     0  3.9G   0% /dev/shm
      tmpfs           5.0M     0  5.0M   0% /run/lock
      tmpfs           3.9G     0  3.9G   0% /sys/fs/cgroup
      /dev/vda15      105M  3.6M  101M   4% /boot/efi
      tmpfs           798M     0  798M   0% /run/user/0

      server2 | CHANGED | rc=0 >>
      Filesystem      Size  Used Avail Use% Mounted on
      udev            2.0G     0  2.0G   0% /dev
      tmpfs           395M  608K  394M   1% /run
      /dev/vda1        78G  2.2G   76G   3% /
      tmpfs           2.0G     0  2.0G   0% /dev/shm
      tmpfs           5.0M     0  5.0M   0% /run/lock
      tmpfs           2.0G     0  2.0G   0% /sys/fs/cgroup
      /dev/vda15      105M  3.6M  101M   4% /boot/efi
      tmpfs           395M     0  395M   0% /run/user/0

      ...




          ansible all -m apt -a "name=vim state=latest" -u root
          ansible servers -a "uptime" -u root
          ansible server1:server2 -m ping -u root





:notebook: :pen:



#


<a name="ansible_basics"></a>
[Top](#top)

# Ansible Basic Terms

**What is Ansible in DevOps?**

Ansible is defined as an open-source, cross-platform tool for resource provisioning automation that DevOps professionals popularly use for continuous delivery of software code by taking advantage of an “infrastructure as code” approach.

OR

Ansible is a configuration and orchestration management tool where applications are deployed automatically in a variety of environments.

OR

Ansible is the simplest way to automate apps and IT infrastructure. Application Deployment + Configuration Management + Continuous Delivery.



**Plugins**

Plugins are pieces of code that augment Ansible's core functionality. Ansible uses a plugin architecture to enable a rich, flexible and expandable feature set. Ansible ships with a number of handy plugins, and you can easily write your own.

**Control node** 

Any host with Ansible installed. Ansible control nodes are primarily used to run tasks on managed hosts. You can use any machine with Python installed as an Ansible control node. However, you cannot use Windows as an Ansible control node. Managed nodes: Hosts that you manage using Ansible.

**Managed node**

A managed node is any device being managed by the control node. Ansible works by connecting to nodes (clients, servers, or whatever you're configuring) on a network, and then sending a small program called an Ansible module to that node. Ansible executes these modules over SSH and removes them when finished.

**Inventory**

The Ansible inventory file defines the hosts and groups of hosts upon which commands, modules, and tasks in a playbook operate. The file can be in one of many formats depending on your Ansible environment and plugins.


Exmple: 

Here’s what a plain text inventory file looks like:

	---
	[webservers]
	www1.example.com
	www2.example.com

	[dbservers]
	db0.example.com
	db1.example.com




**Module**

A module is a reusable, standalone script that Ansible runs on your behalf, either locally or remotely. Modules interact with your local machine, an API, or a remote system to perform specific tasks like changing a database password or spinning up a cloud instance.

**Playbook**

An Ansible playbook is an organized unit of scripts that defines work for a server configuration managed by the automation tool Ansible. Ansible is a configuration management tool that automates the configuration of multiple servers by the use of Ansible playbooks.

Example 1:

Here’s what a simple playbook looks like:

	---
	- hosts: webservers
	  serial: 5 # update 5 machines at a time
	  roles:
	  - common
	  - webapp

	- hosts: content_servers
	  roles:
	  - common
	  - content



Example 2: 

Inventory: hosts file

	vim /etc/ansible/hosts
	
	[localhost]
	localhost

Playbook: aws.yml file

	- host: localhost
	  tasks: 
	   - ec2: 
	      aws_access_key: keywithoutqoutes
	      aws_secret_key: keywithout qoutes
	      key_name: key-pair-one
	      group: xyz
	      instance_type: t2.micro
	      image: ami-zyajskdxdkjek
	      wait: yes
	      wait_timeout: 500
	      count: 1
	      instance_tags: 
		name: prod-instance
	      monitoring: 
              region: us-east-1
	      vpc_subnet_ip: subnet-any
	      assign_public_id: yes
	      
	      
RUN Playbook CMD: 
	  	
		ansible-playbook aws.yml





Stop Instance: 


	- host: localhost
	  tasks: 
	   - ec2: 
	      aws_access_key: keywithoutqoutes
	      aws_secret_key: keywithout qoutes
	      instance_ids: i-jskxjejkjf
	      region: us-east-1
	      state: stopped OR running OR absent
	      wait: true
	      vpc_subnet_ip: subnet-any
	      assign_public_id: yes
     
	      

RUN Playbook CMD: aswstop.yml

                ansible-playbook awsstop.yml

	 
	 
	 
	 
#

Ansible :

 Opensource, Configuration tools. 

1. Manual 

2. Two types of automation

 a) Scripted Languages
 b) Tool (Ansible:Automation)


Management: 
  
 Server Changes
 
 Device Changes
 
 Cloud
 
 Virtualization Host
 

Working: 

Ansible is is an agent less configuration tool
It works of Push System.
It works an forks and serial mode. Default It comes width forks style (forks5)


Architecture: 

	 1. Control Node
	 2. Manage Node
	 3. Connection plugin
	 4. Inventory System
	 5. Modules
	 6. Ad Hoc
	 7. Playbooks
	 
#



Architecture:


						 _____________________
						|    Managed Node     |
						|       (Host1)       |
						|_____________________| 
						 _____________________
						|    Managed Node     |
						|       (Host1)       |
						|_____________________| 

		 __________________
		| Control Node     |
		|                  |
		|__________________| 
						 _____________________
						|    Managed Node     |
						|       (Host1)       |
						|_____________________| 
						 _____________________
						|    Managed Node     |
						|       (Host1)       |
						|_____________________| 





:end: 




#
<a name="ansible-on-centos"></a>
[Top](#top)

# How to Install and Configure Ansible on CentOS

**Step 1: Update Your Control Node**

Before installing any new software, it is important to ensure that your existing operating version is up-to-date. Enter the command mentioned below to start your task.

	yum update	

**Step 2: Install EPEL Repository**

Moving on, install the EPEL repository on the system.

	yum install epel-release

EPEL provides easy access to install commonly used packages on CentOS.

**Step 3: Install Ansible**

The next step is to install the Ansible package from the EPEL repository.

	yum install ansible

**Step 4: Create a User for Ansible**

Let's create a non-root user on both the nodes that will run our Ansible playbooks. In this demo, we will use "ajaysis"' as the username (but any username can be added). Also, you should ensure that you use the same username on both the nodes (i.e., controller node and your managed node).

Add a user and set a password onto your Controller node.

	useradd  ajaysis

	passwd ajay@123

Add the admin user, and set a password onto your Managed node.

	useradd ajay

	passwd ajay@123




**Step 5: Configure Our Admin User for SSH Access**

Configure the admin user (i.e. Ajaysis user) so that it can access the Managed node without a password. Then, ensure that you set up an SSH key pair to the Ajaysis user.

Now, run the following command (in the control node) to generate an SSH key pair. 

	ssh-keygen

Then, copy the public key and paste it to our Managed node with the command below.

	ssh-copy-id node.ab.example.com
	
**Step 6: Create an Inventory**

An inventory list is created to identify your managed nodes. 

Log in to your control node as the admin user to connect the Managed node to the inventory.

	vim /home/admin/inventory

Now, enter ‘i’ to get to the insert mode, and add the hostname of the Managed Node. node.ab.example.com

Now, save the file by typing ‘[ESC]:wq’.

**Step 7: Create an Ansible Playbook**

Here, we will create a simple Ansible playbook by installing Nginx on the Managed Node.

First, log onto your Controller Node as the “Ajaysis” user and create a file with a descriptive name.

	vim /home/ajaysis/install-nginx.yml

These playbooks are written in YAML language which is human-readable (as shown below).

Now, go to the insert mode and add the following text to your playbook. 

	--

	- hosts: AppServer

	  become: yes

	  tasks: 

	  - name: Installs nginx web server

	    Apt: name: nginx state: started update_cache: true

	    notify:

	    - start nginx

	  handlers:

	  - name: start nginx

	    service:

	      name: nginx

	      state: started

Let’s break the code into segments for a better understanding.

---

YAML provides multiple files to exist in one document file where each is separated by---

The YAML file defines a hierarchical structure with the containing elements such as hosts, tasks, and handlers.

In this playbook, we have a set of tasks, such as:


	- hosts: AppServer

	  become: yes

	  tasks: 

	  - name: Installs nginx web server

	    Apt: name: nginx state: started update_cache: true

	    notify:

	    - start nginx


Task performs all the major operations in the file.

Here, ‘notify’ consists of a list with one item, which is called "start nginx." Notify is not an internal command of Ansible but a reference to a handler that is responsible for performing a function when it is called by a task.

Handlers are the same as hosts and tasks, but they operate only when instructed by a task on the client system.

 handlers:

	  - name: start nginx 

	    service:

	      name: nginx

	      state: started
	      

The code above defines the "start nginx" handler. The handler will execute after the nginx web server is installed. We can save this playbook into a file called something like "nginx.yml".

Then type '[ESC]:wq' to save this and exit.

Note: Prioritize using only spaces and not tabs. Make sure to use consistent spacing for your YAML file to avoid errors.

**Step 8: Run the Playbook**

Our Ansible playbook is built. Now, to run the playbook, type the following command on the controller node:

	ansible-playbook -i /home/admin/inventory /home/admin/install-nginx.yml

In the command above, we have added the inventory file with the "-i" option, followed by the playbook path.



:end:





#

<a name="ansible-playbook-inventory"></a>
[Top](#top)
# Playbook & Inventory More Examples


AD HOC Command:

	ansible webserver -m yum -a "name=httpd state=latest"


OR


Ansible Playbook:


	---
	 - name: playbook name
	   hosts: webserver
	   tasks: 
	     - name: name of task
	       yum: 
		 name: httpd
		 state: latest




#

As an example. Let us consider you want to install an Apache Web server against multiple hosts. The following playbook would get it done for you.

Ansible Playbook Example:


1.


	---
	  - name: Playbook
	    hosts: webservers
	    become: yes
	    become_user: root
	    tasks:
	      - name: ensure apache is at the latest version
		yum:
		  name: httpd
		  state: latest
	      - name: ensure apache is running
		service:
		  name: httpd
		  state: started




Well, I have explained what each line does

name Name of the playbook

hosts A set of hosts usually grouped together as a host group and defined in inventory file

become To tell ansible this play has to be executed with elevated privileges

become_user the user name that we want to switch to like compare it with sudo su - user

tasks set of tasks to execute, All tasks would be defined below this


and then we have two tasks with two modules, the first module is yum and the second module is service

in the first task with yum  the state latest represents that the forementioned package httpd should be installed if it is not installed (or) if it is already installed it should be upgraded to the latest version available. If you do not want it to be upgraded if present, You can change it to state: present

On the Second task with service module, we are making sure that the service named httpd is started and running using the state: started Ansible would not restart the service if it is already started and running.




**Ansible Play vs Ansible Playbook?**


To understand the ansible-playbook you have to understand the Ansible Adhoc commands.

Ad hoc commands can run a single, simple task against a set of targeted hosts as a one-time command. The real power of Ansible, however, is in learning how to use playbooks to run multiple, complex tasks against a set of targeted hosts in an easily repeatable manner.

Here is something to take away

    A play is an ordered set of tasks which should be run against hosts selected from your inventory.

    A playbook is a text file that contains a list of one or more plays to run in order.

In the previously given example, you can see we are running all the tasks against a single host group named webservers  this is called A PLAY.

If I want to run a different set of tasks against different host group. All you need to do is add one more PLAY.

Remember: A Playbook can have many plays destined to run against a different set of host groups

Every Play must contain

    A set of hosts to configure
    A list of tasks to be executed on those hosts

Think of a play as a wire that connects hosts to tasks.



Example Ansible Playbook with multiple hosts and multiple plays.

Here is the ansible playbook with multiple hosts in it.  You can see we are working with web and application servers in the same playbook and executing two different plays (set of tasks) respectively.




2.


	---
	  # Play1 - WebServer related tasks

	  - name: Play Web - Create apache directories and username in web servers
	    hosts: webservers
	    become: yes
	    become_user: root
	    tasks:
	      - name: create username apacheadm
		user:
		  name: apacheadm
		  group: users,admin
		  shell: /bin/bash
		  home: /home/weblogic

	      - name: install httpd
		yum:
		  name: httpd
		  state: installed
        
	
           # Play2 - Application Server related tasks  
  
	  - name: Play app - Create tomcat directories and username in app servers
	    hosts: appservers
	    become: yes
	    become_user: root
	    tasks:
	      - name: Create a username for tomcat
		user:
		  name: tomcatadm
		  group: users
		  shell: /bin/bash
		  home: /home/tomcat

	      - name: create a directory for apache tomcat
		file:
		  path: /opt/oracle
		  owner: tomcatadm
		  group: users
		  state: present
		  mode: 0755


In the preceding playbook, you could notice that two plays are there and both of them targeted to different host groups.



How to Execute an Ansible Playbook

Ansible playbook can be executed with ansible-playbook command. like you have ansible command to execute ad hoc command. This is dedicated for ansible playbooks

Let us see how to execute the preceding playbook and install apache on the webservers host group

Note*: a host group is a group of hosts and servers mentioned in the ansible inventory file.


	➜  Ansible-Examples git:(master) ✗ cat ansible_hosts

	[webservers]
	mwivmweb01
	mwivmweb02
	

Here is the customized Ansible inventory file with two hosts grouped as webservers

Here the host group name is webservers and it is mentioned in the hosts: directive on the playbook

Given below is the command syntax or sample to run an ansible playbook.

	➜ ansible-playbook sampleplaybook.yml -i ansible_hosts


If you have mentioned all the host groups in your default inventory file /etc/ansible/hosts  then you do not have use -i argument.  this is only when you have a customized inventory file like I do.


How to Dry Run the playbook without making Actual Changes

you can actually run the playbook with Dry Run feature to see what changes would be made to the server without having to perform the actual changes.

to do that. you just have to add -C to your ansible-playbook startup command

	➜ ansible-playbook -C sampleplaybook.yml -i ansible_hosts



How to Perform a Syntax Check on the Playbook

If you quickly want to verify if everything is ok with the playbook. You can perform a Syntax check.

Here is the ansible command line example on how to perform Syntax check on ansible playbook. Refer the video for the practical idea.

	➜ ansible-playbook – syntax-check sampleplaybook.yml -i ansible_hosts


How to use Variables in Ansible Playbook

Ansible playbook supports defining the variable in two forms, Either as a separate file with full of variables and values like a properties file. or a Single liner variable declaration like we do in any common programming languages

vars to define inline variables within the playbook

vars_files to import files with variables

Let’s suppose we want to add a few variables for our webserver like the server name and SSL key file and cert file etc.

it can be done with vars like this


	---
	  - name: Playbook
	    hosts: webservers
	    become: yes
	    become_user: root
	    vars:
	       key_file:  /etc/apache2/ssl/mywebsite.key
	       cert_file: /etc/apache2/ssl/mywebsite.cert
	       server_name: www.mywebsite.com
	    tasks:
	      - name: ensure apache is at the latest version
		yum:
		  name: httpd
		  state: latest
	      ### SOME MORE TASKS WOULD COME HERE ###
	      # you can refer the variable you have defined earlier like this #
	      # "{{key_file}}"  (or) "{{cert_file}}" (or) "{{server_name}}" #
	      ##
	      - name: ensure apache is running
		service:
		  name: httpd
		  state: started
		  

and the variables can be referred with the jinja2 template later"{{ variable name }}"

If you want to keep the variables in a separate file and import it with vars_files

You have to first save the variables and values in the same format you have written in the playbook and the file can later be imported using vars_files like this


	---
	  - name: Playbook
	    hosts: webservers
	    become: yes
	    become_user: root
	    vars_files:
		- apacheconf.yml
	    tasks:
	      - name: ensure apache is at the latest version
		yum:
		  name: httpd
		  state: latest
	      ### SOME MORE TASKS WOULD COME HERE ###
	      # you can refer the variable you have defined earlier like this #
	      # "{{key_file}}"  (or) "{{cert_file}}" (or) "{{server_name}}" #
	      ##
	      - name: ensure apache is running
		service:
		  name: httpd
		  state: started


the content of the apacheconf.yml would like like this


	key_file: /etc/apache2/ssl/mywebsite.key  
	cert_file: /etc/apache2/ssl/mywebsite.cert  
	server_name: www.mywebsite.com
	

to keep things cleaner and to keep your playbook simple, It is recommended to use separate variable files and when you are creating ansible roles, you would have to use the variable files more than defining it inline.

 

 
Example Ansible Playbook to Setup LAMP stack

Linux Apache Mysql/MariaDB PHP is shortly called as LAMP stack and it powers most of the internet websites including Facebook.

So let us look at a Sample Ansible Playbook to install LAMP stack with necessary packages and tools.

So what are going to do in this playbook

    Connect to Remote host and execute the following tasks
    
        Install all necessary packages like Apache(httpd), mariadb, php
        Installing a firewall and enabling HTTP services
        Start the Apache HTTPD web server.
        Start the MariaDB server
        Download a Sample PHP page from remote URL
        Access the website we have built by accessng the URL

 

Here is the Ansible Playbook example to setup LAMP Stack


	---
	- name: Setting up LAMP Website
	  user: vagrant
	  hosts: testserver
	  become: yes
	  tasks:
	    - name: latest version of all required packages installed
	      yum:
		name:
		  - firewalld
		  - httpd
		  - mariadb-server
		  - php
		  - php-mysql
		state: latest

	    - name: firewalld enabled and running
	      service:
		name: firewalld
		enabled: true
		state: started

	    - name: firewalld permits http service
	      firewalld:
		service: http
		permanent: true
		state: enabled
		immediate: yes

	    - name: Copy mime.types file
	      copy:
		src: /etc/mime.types
		dest: /etc/httpd/conf/mime.types
		remote_src: yes

	    - name: httpd enabled and running
	      service:
		name: httpd
		enabled: true
		state: started

	    - name: mariadb enabled and running
	      service:
		name: mariadb
		enabled: true
		state: started

	    - name: copy the php page from remote using get_url
	      get_url:
		url: "https://www.example.com/index.php"
		dest: /var/www/html/index.php
		mode: 0644

	    - name: test the webpage/website we have setup
	      uri:
		url: http://{{ansible_hostname}}/index.php
		status_code: 200



#
# Ansible Playbook  to Exchange keys between hosts

Type1: With Ansible Shell module and Typical Commands


	---
	- name: Exchange Keys between servers
	  become: yes
	  become_user: weblogic
	  hosts: app
	  tasks:
	    - name: SSH KeyGen command
	      shell: > 
		ssh-keygen -q -b 2048 -t rsa -N "" -C "creating SSH" -f ~/.ssh/id_rsa
		creates="~/.ssh/id_rsa"

	    - name: Fetch the keyfile from one server to another
	      fetch: 
		src: "~/.ssh/id_rsa.pub"
		dest: "buffer/{{ansible_hostname}}-id_rsa.pub"
		flat: yes

	    - name: Copy the file from master to the destination
	      copy:
		src: "buffer/{{item.dest}}-id_rsa.pub"
		dest: "/tmp/remote-id_rsa.pub"  
	      when: "{{ item.dest != ansible_hostname }}"
	      with_items: 
		- { dest: "{{groups['app'][1]}}"}
		- { dest: "{{groups['app'][0]}}"}

	    - name: add the public key into Authorized_keys file to enable Key Auth
	      shell: "cat /tmp/remote-id_rsa.pub >> ~/.ssh/authorized_keys"
	      register: addtoauth



Type2: With Ansible authorized_key module


	---
	- name: Exchange Keys between servers
	  become: yes
	  become_user: weblogic
	  hosts: app
	  tasks:
	    - name: SSH KeyGen command
	      tags: run
	      shell: > 
		ssh-keygen -q -b 2048 -t rsa -N "" -C "creating SSH" -f ~/.ssh/id_rsa
		creates="~/.ssh/id_rsa"

	    - name: Fetch the keyfile from one server to another
	      tags: run
	      fetch: 
		src: "~/.ssh/id_rsa.pub"
		dest: "buffer/{{ansible_hostname}}-id_rsa.pub"
		flat: yes

	    - name: Copy the key add to authorized_keys using Ansible module
	      tags: run
	      authorized_key:
		user: weblogic
		state: present
		key: "{{ lookup('file','buffer/{{item.dest}}-id_rsa.pub')}}"
	      when: "{{ item.dest != ansible_hostname }}"
	      with_items: 
		- { dest: "{{groups['app'][1]}}"}
		- { dest: "{{groups['app'][0]}}"}



Ansible SSH Key Exchange between multiple hosts


	---
	- name: Exchange Keys between servers
	  hosts: multi
	  tasks:
	    - name: SSH KeyGen command
	      tags: run
	      shell: > 
		ssh-keygen -q -b 2048 -t rsa -N "" -C "creating SSH" -f ~/.ssh/id_rsa
		creates="~/.ssh/id_rsa"

	    - name: Fetch the keyfile from the node to master
	      tags: run
	      fetch: 
		src: "~/.ssh/id_rsa.pub"
		dest: "buffer/{{ansible_hostname}}-id_rsa.pub"
		flat: yes

	    - name: Copy the key add to authorized_keys using Ansible module
	      tags: runcd
	      authorized_key:
		user: vagrant
		state: present
		key: "{{ lookup('file','buffer/{{item}}-id_rsa.pub')}}"
	      when: "{{ item != ansible_hostname }}"
	      with_items: 
		- "{{ groups['multi'] }}"       



CMD:

	sshkey-exchange-t1.yaml 

:end: 
