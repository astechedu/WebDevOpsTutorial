# Dockrized Linux Containers
:link:[Home](all-file-links.md)     


<a name="top"></a>
Topics: 

  1. [Fix Failed to download metadata for repo in Centos Dockrized Container](#doc_centos_cont_err) <br>





[Go To TOP](#top)
<a name="doc_centos_cont_err"></a>
# 1. Fix Failed to download metadata for repo

Step 1: Go to the /etc/yum.repos.d/ directory.

    [root@autocontroller ~]# cd /etc/yum.repos.d/

Step 2: Run the below commands

    [root@autocontroller ~]# sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
    [root@autocontroller ~]# sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
    
Step 3: Now run the yum update

    [root@autocontroller ~]# yum update -y

    
