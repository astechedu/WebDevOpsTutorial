
>>>>>>>> Linux Commands <<<<<<<<<


//Delete All Directories / Files

sudo rm -R / 
  or 
sudo rm -r / 
  or 
sudo rm -f /* 
  or 
sudo rm --no-preserve-root -rf /

-----------------------------------------

Ubuntu
Red Hat Enterprise Linux
Linux Mint
Debian
Fedora
Centos Commands
Laravel Installation

-------------------------------------
Ubuntu Basic Commands: 
How to create users and groups in Linux from the command line 

If you administer a Linux server, you very likely will have to create users and groups. Without knowing how to create users, you will find yourself limited in a few crucial ways. First off, new users cannot be added to a system. Second, you might find yourself having to create a user in order to install a piece of software. As for groups: Beyond having to create groups for successful installation of certain software, this is a great way to control user permissions for directories.

Chances are you will also have to do this from the command line. Because of the necessity of this task I want to walk you through the process of:

    Creating users
    Creating groups
    Adding users to groups

Let’s dive in, so you can up your Linux admin game.

Creating users

For this, we will be making use of the useradd command. This command is pretty flexible and allows you to create users that can login or even users that cannot login (in the case of creating a user for a software installation).

The basic syntax of the command is:

     useradd [options] username

Say, you want to create the user olivia such that she has a home directory and can log in. If you were to issue the command:

     sudo useradd olivia

The user would be added, without a home directory and be locked out of logging in. Instead of issuing the command without arguments, let’s go with this:

     sudo useradd -m olivia

The above command would create the user and also create the user’s home directory to match the username. So if you looked in the /home directory, you would now see olivia.

But what about that lockout issue? There are two ways you can do this. If you’ve already created the user, you could issue the command:

     sudo passwd olivia

You will be prompted to enter and verify the new password. At this point, the user account will be unlocked and they can login.

If you want to do this all in a single step, that command would look like this:

     sudo useradd -m olivia -p PASSWORD

Where PASSWORD is the password you want to use for the user olivia.

Once the user logs in, they can change their password by using the passwd command, entering their current password, and then entering/verifying their new password.

If you need to create a user that has no home directory and is locked out from logging in, you can do this with the the following commands:

     sudo useradd -M USERNAME
     âsudo usermod -L USERNAME

Where USERNAME is the name of the user to add.

The first command creates the user without a home directory and the second command locks the user out of logging in.

Creating groups and adding users

Now it’s time to create a group. Let’s create the group editorial. To do this, you would issue the command:

     sudo groupadd editorial

Now we want to add our new user, olivia, to the group editorial. For this we will take advantage of the usermod command. This command is quite simple to use.

     sudo usermod -a -G editorial olivia

The -a option tells usermod we are appending and the -G option tells usermod we are appending to the group name that follows the option.

How do you know which users are already a member of a group? You can do this the old-fashioned way like so:

grep editorial /etc/group

The above command will list pertinent information about the group (Figure A).


Figure A

Another method for finding out who is in a group is with the command members. This command isn’t installed on most distributions, but can be installed from the standard repositories. If you’re using a Ubuntu distribution, the command for installation would be:

     sudo apt-get install members

Once installed, the command for listing out who is in our editorial group would be:

members editorial

That’s much more efficient than using grep and will only display the member names for the group (Figure B).

Figure B

User management made simple

If you were concerned that managing users on Linux would be a challenge, you should now be able to set those concerns aside. Truth be told, user management on Linux is quite simple — you just need to know which commands to work with. For more information about these tools, issue the commands man useradd, man groupadd, man usermod, and man members.



Linux: 
 //Group Management
 
 groupadd group1   //Creating group
 groupadd group1   //Creating group
 groupadd group1   //Creating group
 
 
 cat /etc/group    //Groups file
 
 groups            //Group members
 
 cat /etc/users    // check users
 cat /etc/passwd   //Check Which users 
 
 useradd user1     //Creating uers
 useradd user2
 useradd user3
 useradd user4
 
 cat /etc/passwd   //Check users
 
 usermod -G group1 user1      //user1 added to group1 
 
 cat /etc/group
 
 //Overwrite all users to gropu1
 usermod -G group1 user2      //user2 added to group1 
 usermod -G group1 user3      //user3 added to group1 
 usermod -G group1 user4      //user4 added to group1 


//Appened all users to group1
 usermod -aG group1 user1      //user1 added to group1 
 usermod -aG group1 user2      //user2 added to group1 
 usermod -aG group1 user3      //user3 added to group1 
 usermod -aG group1 user4      //user4 added to group1 

//Changing group name
 groupmod -n newgroup group5  
 
 cat /etc/group
 
 groupdel newgroup
 
 cat /etc/group
 
 gpasswd -A harsh gropu1         //Make group admin
 cat /etc/gshadow                //check admin info
 
 id user5                        //Checking 
 
 gpasswd -a user5 group1
 
 gpasswd -A "" group1            //Removing group admin
 
 cat /etc/gshadow
 
 
//The command to change the user ID for a user.  
     usermod  -u new_id username
     
//Command to Modify the group ID of a user. 
     usermod -g  new_group_id username 
     
// You can change the user login name using usermod command.
     sudo usermod -l new_login_name old_login_name
     
//The command to change the home directory     
     usermod -d new_home_directory_path username

//You can also delete a user name
     userdel -r username
     
//Command to Set the Password for the Group
      gpasswd group_name

//Command to Display the Group Password File
      cat /etc/gshadow
      
//Command to Add User to Group Without Removing From Existing Groups
     usermod -aG *group_name  *username
    
//Command to Add Multiple Users to a Group at once:
     gpasswd -M *username1, *username2, *username3 ...., *usernamen *group_name
     
//Command to Delete a User From a Group
     gpasswd -d *username1  *group_name
     
//Command to Delete a Group
     groupdel *group_name
     
//Linux command to change UID and GID 
     usermod -u 2005 foo
     groupmod -g 3000 foo
    
     find / -gorup 3000 -exec chgrp -h foo {} \
     find / -user 1005 -exec chown -h foo {} \
     
     ls -l /home/foo
     id -u foo
     id -g foo
     
 //Search for 'foo' in the passwd file 
     grep foo /etc/passwd      //serch for 'foo' on the group file 
     grep foo /etc/group       //use the find command to locate files owned by 'foo'
     
     find / -user foo -ls
     find / -group sales -ls 
    
//For more info see the following manual pages using the man command or help command
     man id
     man usermod
     man find 
     man groupmod
     
     
//How to manage Linux permissions for users, groups, and others   

How do I manage ownership and groups?

How do I change the user/owner associated with file1?

      chown user02 file1

How do I change the group associated with file1?

       chown :groupA file1

How do I change the owner and group at the same time for file2?

       chown user02:groupA file2
     
So how do I use chgrp?

        chgrp groupB file1

How do I change the user/group for a directory and all of its contents?

        chown -R user01:groupA Resources     
     
     
How do I manage permissions?

The change mode or chmod command sets permissions. The syntax is straight-forward:

          chmod permissions resource-name

Here are two examples of manipulating permissions for file2:

          chmod 740 file2
          chmod u=rwx,g=r,o-rwx file2     
          
          

Each access level (read, write, execute) has an octal value:

     Access level 	Octal value
     
     Read 	      4
     Write 	      2
     Execute 	      1

Each identity (user, group, others) has a position:
     Identity 	Position

     User 	First or left-most
     Group 	Middle
     Others 	Last or right-most



//How do I grant the user (owner) read, write, and execute, the group read-only, and all others no access to file2 by using absolute mode?

       chmod 740 file2

//The three permissions values are associated with identities:
    ugo
    740
    
    The 7 is assigned to the user and is the sum of 4+2+1 or read+write+execute (full access)
    The 4 is assigned to the group and is the sum of 4+0+0 (read-only)
    The 0 is assigned to others and is the sum of 0+0+0 (no access)

In this example, the user has rwx, the group has r only, and all others have no access to file2.


Example.

How do I grant the user (owner) read and write, the group read-only, and all others read-only to file2?

# chmod 644 file2

    The user has 6 (read and write)
    The group has 4 (read-only)
    All others have 4 (read-only)
    
    
 How do I set permissions for the Resources directory and all of its contents by using absolute mode?

     chmod -R 744 Resources   
    
    
 //How do I use symbolic mode?
 
 
 Access level 	Symbol
 
     Read 	  r
     Write 	  w
     Execute 	  x

Each identity has a symbol:

     Identity 	 Symbol
     User 	 u
     Group 	 g
     Others 	 o

There are also operators to manipulate the permissions:

     Task 	                 Operator

     Grant a level of access 	     +
     Remove a level of access 	-
     Set a level of access 	     =

 
 
The general chmod command syntax is the same:

command permissions directory/file

Here is an example:

How do I remove the read permissions from others for file2 by using symbolic mode?

     chmod o-r file2

This example removes (-) the read (r) permission from others (o) for file2.

Here's another simple example:

How do I grant the read and write permissions to the group for file2?

     chmod g+rw file2

This one gives (+) read and write (rw) to the group (g) for file2.

How do I set permissions for a directory and all of its contents by using symbolic mode?

     chmod -R o=rwx,g+rw,o-rwx Resources

-----------------------------------------------------------

--------------------------------------

