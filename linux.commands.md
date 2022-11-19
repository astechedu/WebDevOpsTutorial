# Linux Basic Commands 

#Topics 
 
  1. Permissions
  
  
  
  #### 1. Permissions
  
  >>>>> Linux Commands <<<<<<<<<



How do I change directory permissions in Linux? 

To change directory permissions in Linux, use the following:

    chmod +rwx filename to add permissions
    chmod -rwx directoryname to remove permissions. 
    chmod +x filename to allow executable permissions.
    chmod -wx filename to take out write and executable permissions.


How to Change Directory Permissions in Linux for the Group Owners and Others 


The command for changing directory permissions for group owners is similar, but add a “g” for group or “o” for users:

    chmod g+w filename
    chmod g-wx filename
    chmod o+w filename
    chmod o-rwx foldername


To change directory permissions for everyone, use “u” for users, “g” for group, “o” for others, and “ugo” or “a” (for all).

    chmod ugo+rwx foldername to give read, write, and execute to everyone.
    chmod a=r foldername to give only read permission for everyone.


How to Change Groups of Files and Directories in Linux:

By issuing these commands, you can change groups of files and directories in Linux. 

    chgrp groupname filename
    chgrp groupname foldername


How to change ownership in Linux


Another helpful command is changing ownerships of files and directories in Linux:

    chown name filename
    chown name foldername

You can also combine the group and ownership command by using:
    chown -R name:filename /home/name/directoryname


How to change permissions in numeric code in Linux

You may need to know how to change permissions in numeric code in Linux, so to do this you use numbers instead of “r”, “w”, or “x”.

    0 = No Permission
    1 = Execute
    2 = Write
    4 = Read


Permission numbers are:

    0 = ---
    1 = --x
    2 = -w-
    3 = -wx
    4 = r-
    5 = r-x
    6 = rw-
    7 = rwx


  chmod 777 foldername will give read, write, and execute permissions for everyone.

  chmod 700 foldername will give read, write, and execute permissions for the user only.

  chmod 327 foldername will give write and execute (3) permission for the user, w (2) for the group, and read, write, and execute for the users.



Chown Command in Linux (File Ownership):

chown [OPTIONS] USER[:GROUP] FILE(s)

    USER - If only the user is specified, the specified user will become the owner of the given files, the group ownership is not changed.
    USER: - When the username is followed by a colon :, and the group name is not given, the user will become the owner of the files, and the files group ownership is changed to user’s login group.
    USER:GROUP - If both the user and the group are specified (with no space betwen them), the user ownership of the files is changed to the given user and the group ownership is changed to the given group.
    :GROUP - If the User is omitted and the group is prefixed with a colon :, only the group ownership of the files is changed to the given group.
    : If only a colon : is given, without specifying the user and the group, no change is made.
    
    
    
    
    How to Change the Owner of a File: 
    
    chown USER FILE          //User (new owner)
    chown linuxize file1     // linuxxize (new Owner)
    
    chown linuxize file1 dir1 
    
    chown 1000 file2          // 1000 (new owner id)
    
    
    
  How to Change the Owner and Group of a File:
    
  chown USER:GROUP FILE
 
  chown linuxize:users file1

  chown linuxize: file1
  
  
 How to Change the Group of a File:
 
   chown :GROUP FILE

   chown :www-data file1
   
   
 How to Change Symbolic Links Ownership:  
 
   chown www-data: symlink1
   
   chown -h www-data symlink1
   
   
How to Recursively Change the File Ownership: 

    chown -R USER:GROUP DIRECTORY
    chown -R www-data: /var/www
    chown -hR www-data: /var/www
    
    
 Using a Reference File:
 
    chown --reference=file1 file2
    
     (For example, the following command will assign the user and group ownership of the file1 to file2)
   
   
--------------------------------------------------
   
AddGroup & DelGroup: 
--------------------
How to Create Groups in Linux (groupadd Command): 

groupadd Command Syntax:

   groupadd [OPTIONS] GROUPNAME
   
Creating a Group in Linux: 

   groupadd mygroup
   groupadd -f mygroup
   
   
Creating a Group with Specific GID: 

   groupadd -g 1010 mygroup
   
 You can verify the group’s GID, by listing all groups and filtering the result with grep :  
 
   getent group | grep mygroup  
   
   
When used with the -o (--non-unique) option the groupadd command allows you to create a group with non-unique GID:

   groupadd -o -g 1010 mygroup
   

Creating a System Group: 

   groupadd -r mysystemgroup
   
   
Overriding the Default /etc/login.defs Values

   groupadd -K GID_MIN=1200 -K GID_MAX=1500 mygroup   
   
  
Creating a System Group with Password 

   groupadd -p grouppassword mygroup    
     
 
Deleting a group:

  groupdel [groupName]
  
   
--------------------------------------------------------
    

AddUser: 


useradd Command:

useradd [OPTIONS] USERNAME


How to Create a New User in Linux: 

  sudo useradd username
  sudo passwd username
  
  
How to Add a New User and Create Home Directory:

  sudo useradd -m username
  ls -la /home/username/
  
Creating a User with Specific Home Directory:

  sudo useradd -m -d /opt/username username  
  sudo useradd -m -d /opt/username username
  
Creating a User with Specific User ID: 

  sudo useradd -u 1500 username
  id -u username
  
Creating a User with Specific Group ID: 

  sudo useradd -g users username
  id -gn username
  
Creating a User and Assign Multiple Groups:

  sudo useradd -g users -G wheel,developers username    //primary grou:users, secondly groups: whell and developers
  id username  
  
  
Creating a User with Specific Login Shell: 


    sudo useradd -s /usr/bin/zsh username
    grep username /etc/passwd
  
Creating a User with Specific Login Shell     
  
    sudo useradd -s /usr/bin/zsh username
    grep username /etc/passwd                //verify
  
  
Creating a User with Custom Comment: 

    grep username /etc/passwd
  
Creating a User with an Expiry Date: 

    sudo useradd -e 2019-01-22 username
    sudo chage -l username
     
Creating a System User: 

    sudo useradd -r username 
    
Changing the Default useradd Values: 

    useradd -D    
    sudo useradd -D -s /bin/bash: 
    sudo useradd -D | grep -i shell     //verify
    

--------------------------------------------------------
--------------------------------------------------------


What is a Linux Group?

Linux groups help developers manage user accounts in Linux. You can set individual permissions for each user. But, this can be impractical if you’re working with multiple users who should all have the same privileges. 

 Primary group : 
 Secondary group : 
 
How to Add a User to a Group Linux: 

  sudo usermod -a -G group_to_add username
  

The -a flag tells usermod to add a user to a group.
The -G flag specifies the name of the secondary group to which you want to add the user.


 Linux: Add User to Group Example: 
 
  Let’s say you want to add the user “ajay” to the “sudo” group on our computer.
  
    sudo usermod -a -G sudo ajay
    sudo usermod -a -G sudo,test ajay
    
    
 Add User to Group Linux: New User Example:
 
     sudo useradd -g staff -G test cktutorials
     
 How to Check a User’s Group: 
 
      id username        
     
 

-----------------------------------------------------------
