$$\Large{\colorbox{black}{\color{white} Ansible For Beginners}}$$


[Home](all-file-links.md)

#
# Topics: 

   :link:[Ansible Installation on Linux Ubuntu 20.04/22.04](#ansible_installation)
   
   :link:[Ansible Basic Terms](#ansible_basics)









#
<a name="ansible_installation"></a>
#Installing Ansible On Linux:

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

#Ansible Basic Terms


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



						 __________________
						|   Host1         |
						|                 |
						|_________________| 

						 __________________
						|  Host2          |
						|                 |
						|_________________| 
		 __________________
		|Control Node     |
		|                 |
		|_________________| 
						 __________________
						|  Host3          |
						|                 |
						|_________________| 

						 __________________
						|  Host4          |
						|                 |
						|_________________| 




:end: 
