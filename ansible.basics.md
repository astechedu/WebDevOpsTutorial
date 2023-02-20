$$\Large{\colorbox{black}{\color{white} Ansible For Beginners}}$$


[Home](all-file-links.md)

#
# Topics: 

   :link:[Ansible Installation on Linux Ubuntu 20.04/22.04](#ansible_installation)
   
   :link:[Ansible Basic Terms](#ansible_basics)









#
<a name="ansible_installation"></a>
# Installing Ansible On Linux:

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

Example:

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
