$$\colorbox{red}{\color{white} Linux \ Commands}$$


## Delete All Directories / Files

sudo rm -R /  or  sudo rm -r /   or  sudo rm -f /*   or  sudo rm --no-preserve-root -rf /


Steps: 

   - Ubuntu
   - Red Hat Enterprise Linux
   - Linux Mint
   - Debian
   - Fedora
   - Centos Commands
   - Laravel Installation


[Linux Basic Commands](#linux-basic-cmds)

[Linix Networking CMDs](#linux-networking-cmds)

[Alpine Linux Basic Commands](#alpine-basic-cmds)



#

#Ubuntu Basic Commands: 
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
     sudo usermod -L USERNAME

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

 ####Group Management
 
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

#
 ####Overwrite all users to gropu1
 
	 usermod -G group1 user2      //user2 added to group1 
	 usermod -G group1 user3      //user3 added to group1 
	 usermod -G group1 user4      //user4 added to group1 

#
####Appened all users to group1

	 usermod -aG group1 user1      //user1 added to group1 
	 usermod -aG group1 user2      //user2 added to group1 
	 usermod -aG group1 user3      //user3 added to group1 
	 usermod -aG group1 user4      //user4 added to group1 


####Changing group name

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



#


# Linux:


Create User in Short: 

	sudo -i


# Create a standard user account

	useradd -m cli_user1
	

# Create an administrator user account

	useradd -m cli_user1 -G sudo



	ls -la /home/cli_user1



# Create the user with a custom home directory

	useradd -m -d /tmp/tmp_user tmp_user
	
# List the custom home directory

	ls -la /tmp/tmp_user




	useradd -u 1234 uid_user

	id uid_user

        useradd -e 2020-06-30 temp_user
        chage -l temp_user


Setting the New User Password:

	passwd cli_user1



# Exit the root shell

	exit
	
# Switch to the new user account

	su - cli_user1
	
# Show the current user account

	whoami



#

Change USERNAME:

https://www.hepeng.me/changing-username-and-hostname-on-ubuntu/

At the start screen press Ctrl+Alt+F1

Set a password for the "root" account.

	sudo passwd root 

Log out.

	exit


Log in using the "root" account and the password you have previously set.
Change the username and the home folder to the new name that you want.

	usermod -l <newname> -d /home/<newname> -m <oldname>

Change the group name to the new name that you want. I'm not so sure about which group should I change to

	groupmod -n <newgroup> <oldgroup> 

Lock the "root" account.

	passwd -l root

If you were using ecryptfs (encrypted home directory). Mount your encrypted directory using ecryptfs-recover-private and edit <mountpoint>/.ecryptfs/Private.mnt to reflect your new home directory.
Log out.

	exit

	Press Ctrl+Alt+F7.



#

Change HostName:

https://phoenixnap.com/kb/ubuntu-20-04-change-hostname

Change Hostname on Ubuntu 20.04 – Alternative Method (Reboot Required)

    Step 1: Open /etc/hostname and Change the Hostname. ...
    Step 2: Open /etc/hosts and Change the Hostname. ...
    Step 3: Reboot the System.



CMDS:
   
      hostname              
      hostnamectl 



sudo systemctl reboot


#


How To Create a New Sudo-enabled User on Ubuntu 20.04 [Quickstart]:

https://www.digitalocean.com/community/tutorials/how-to-create-a-new-sudo-enabled-user-on-ubuntu-20-04-quickstart


/etc/sudoers


When managing a server, you’ll sometimes want to allow users to execute commands as “root,” the administrator-level user. The sudo command provides system administrators with a way to grant administrator privileges — ordinarily only available to the root user — to normal users.

how to create a new user with sudo access on Ubuntu 20.04 without having to modify your server’s /etc/sudoers file.


Step 1 — Logging Into Your Server

SSH in to your server as the root user:

    ssh root@your_server_ip_address


Step 2 — Adding a New User to the System

Use the adduser command to add a new user to your system:

    adduser sammy


Be sure to replace sammy with the username that you want to create. You will be prompted to create and verify a password for the user:



Step 3 — Adding the User to the sudo Group

Use the usermod command to add the user to the sudo group:

    usermod -aG sudo sammy


Again, be sure to replace sammy with the username you just added. By default on Ubuntu, all members of the sudo group have full sudo privileges.


Step 4 — Testing sudo Access


To test that the new sudo permissions are working, first use the su command to switch to the new user account:

    su - sammy


As the new user, verify that you can use sudo by prepending sudo to the command that you want to run with superuser privileges:

    sudo command_to_run


For example, you can list the contents of the /root directory, which is normally only accessible to the root user:

    sudo ls -la /root


The first time you use sudo in a session, you will be prompted for the password of that user’s account. Enter the password to proceed:


Output:
[sudo] password for sammy:

#
:end:
	
#
	
[Top](#top)
<a name="linux-basic-cmds"></a>
	
#### Linux Basic Commands

	 _________________________
	|                         | 
	| Linux Basic Commands:   |
	|_________________________|


What Is a Linux Command?


	ls, sudo, cd, mv, find, grep, pwd, cat, touch, mkdir, rmdir, 
	df, du, locate, head, tail, diff, tar, chmod, chown, jobs, kill, 
	ping, wget, uname, top , history, man,echo, zip, unzip, hostname, 
	useradd, userdell, apt-get, nano, vi, vim, jed, alias, unalias, su,
	htop, ps


A Linux command is a program or utility that runs on the CLI – a console that interacts with the system via texts and processes. It’s similar to the Command Prompt application in Windows.

Linux commands are executed on Terminal by pressing Enter at the end of the line. You can run commands to perform various tasks, from package installation to user management and file manipulation.

Here’s what a Linux command’s general syntax looks like:

	CommandName [option(s)] [parameter(s)]

A command may contain an option or a parameter. In some cases, it can still run without them. These are the three most common parts of a command:

    CommandName is the rule that you want to perform.
    Option or flag modifies a command’s operation. To invoke it, use hyphens (–) or double hyphens (—).
    Parameter or argument specifies any necessary information for the command.

Keep in mind that all Linux commands are case-sensitive.

The 40 Most Commonly Used Linux Commands

Before proceeding to the list of basic commands, you need to open Terminal first. If you are still unsure, check out our CLI tutorial.

Although the steps may differ depending on your Linux distribution, the Terminal application is usually found in the Utilities section.

Here is the list of basic Linux commands:

####1. sudo command
   

Short for superuser do, sudo is one of the most popular basic Linux commands that lets you perform tasks that require administrative or root permissions.

When using sudo, the system will prompt users to authenticate themselves with a password. Then, the Linux system will log a timestamp as a tracker. By default, every root user can run sudo commands for 15 minutes/session.

If you try to run sudo in the command line without authenticating yourself, the system will log the activity as a security event.

Here’s the general syntax:

sudo (command)

You can also add an option, such as:


    -k or –reset-timestamp invalidates the timestamp file.
    -g or –group=group runs commands as a specified group name or ID.
    -h or –host=host runs commands on the host.


####2. pwd command
   

Use the pwd command to find the path of your current working directory. Simply entering pwd will return the full current path – a path of all the directories that starts with a forward slash (/). For example, /home/username.

The pwd command uses the following syntax:


	pwd [option]


It has two acceptable options:


    -L or –logical prints environment variable content, including symbolic links.
    -P or –physical prints the actual path of the current directory.


####3. cd command
   

To navigate through the Linux files and directories, use the cd command. Depending on your current working directory, it requires either the full path or the directory name.

Running this command without an option will take you to the home folder. Keep in mind that only users with sudo privileges can execute it.

Let’s say you’re in /home/username/Documents and want to go to Photos, a subdirectory of Documents. To do so, enter the following command:

cd Photos.

If you want to switch to a completely new directory, for example, /home/username/Movies, you have to enter cd followed by the directory’s absolute path:

	cd /home/username/Movies

Here are some shortcuts to help you navigate:


    cd ~[username] goes to another user’s home directory.
    cd .. moves one directory up.
    cd- moves to your previous directory.


####4. ls command
   

The ls command lists files and directories within a system. Running it without a flag or parameter will show the current working directory’s content.

To see other directories’ content, type ls followed by the desired path. For example, to view files in the Documents folder, enter:

	ls /home/username/Documents

Here are some options you can use with the ls command:


    ls -R lists all the files in the subdirectories.
    ls -a shows hidden files in addition to the visible ones.
    ls -lh shows the file sizes in easily readable formats, such as MB, GB, and TB.


####5. cat command
   

Concatenate, or cat, is one of the most frequently used Linux commands. It lists, combines, and writes file content to the standard output. To run the cat command, type cat followed by the file name and its extension. For instance:

	cat filename.txt.

Here are other ways to use the cat command:

    cat > filename.txt creates a new file.
    cat filename1.txt filename2.txt > filename3.txt merges filename1.txt and filename2.txt and stores the output in filename3.txt.
    tac filename.txt displays content in reverse order.


####6. cp command
   

Use the cp command to copy files or directories and their content. Take a look at the following use cases.

To copy one file from the current directory to another, enter cp followed by the file name and the destination directory. For example:

	cp filename.txt /home/username/Documents

To copy files to a directory, enter the file names followed by the destination directory:

	cp filename1.txt filename2.txt filename3.txt /home/username/Documents

To copy the content of a file to a new file in the same directory, enter cp followed by the source file and the destination file:

	cp filename1.txt filename2.txt

To copy an entire directory, pass the -R flag before typing the source directory, followed by the destination directory:

	cp -R /home/username/Documents /home/username/Documents_backup

####7. mv command
   

The primary use of the mv command is to move and rename files and directories. Additionally, it doesn’t produce an output upon execution.

Simply type mv followed by the filename and the destination directory. For example, you want to move filename.txt to the /home/username/Documents directory:

	mv filename.txt /home/username/Documents.

You can also use the mv command to rename a file:

	mv old_filename.txt new_filename.txt

####8. mkdir command
   

Use the mkdir command to create one or multiple directories at once and set permissions for each of them. The user executing this command must have the privilege to make a new folder in the parent directory, or they may receive a permission denied error.

Here’s the basic syntax:

	mkdir [option] directory_name

For example, you want to create a directory called Music:

	mkdir Music

To make a new directory called Songs inside Music, use this command:

	mkdir Music/Songs

The mkdir command accepts many options, such as:

    -p or –parents create a directory between two existing folders. For example, mkdir -p Music/2020/Songs will make the new “2020” directory.
    -m sets the file permissions. For instance, to create a directory with full read, write, and execute permissions for all users, enter mkdir -m777 directory_name.
    -v prints a message for each created directory.

####9. rmdir command
   

To permanently delete an empty directory, use the rmdir command. Remember that the user running this command should have sudo privileges in the parent directory.

For example, you want to remove an empty subdirectory named personal1 and its main folder mydir:

	rmdir -p mydir/personal1

####10. rm command
    

The rm command is used to delete files within a directory. Make sure that the user performing this command has write permissions.

Remember the directory’s location as this will remove the file(s) and you can’t undo it.

Here’s the general syntax:

rm filename

To remove multiple files, enter the following command:

	rm filename1 filename2 filename3

Here are some acceptable options you can add:

    -i prompts system confirmation before deleting a file.
    -f allows the system to remove without a confirmation.
    -r deletes files and directories recursively.

	
####11. touch command
    

The touch command allows you to create an empty file or generate and modify a timestamp in the Linux command line.

For example, enter the following command to create an HTML file named Web in the Documents directory:

	touch /home/username/Documents/Web.html

####12. locate command
    

The locate command can find a file in the database system.

Moreover, adding the -i argument will turn off case sensitivity, so you can search for a file even if you don’t remember its exact name.

To look for content that contains two or more words, use an asterisk (*). For example:

	locate -i school*not

The command will search for files that contain the words school and note, whether they use uppercase or lowercase letters.

####13. find command
    

Use the find command to search for files within a specific directory and perform subsequent operations. Here’s the general syntax:

	find [option] [path] [expression]

For example, you want to look for a file called notes.txt within the home directory and its subfolders:

	find /home -name notes.txt

Here are other variations when using find:

    find -name filename.txt to find files in the current directory.
    find ./ -type d -name directoryname to look for directories.

####14. grep command
    

Another basic Linux command on the list is grep or global regular expression print. It lets you find a word by searching through all the texts in a specific file.

Once the grep command finds a match, it prints all lines that contain the specific pattern. This command helps filter through large log files.

For example, you want to search for the word blue in the notepad.txt file:

	grep blue notepad.txt

The command’s output will display lines that contain blue.

####15. df command
    

Use the df command to report the system’s disk space usage, shown in percentage and kilobyte (KB). Here’s the general syntax:

	df [options] [file]

For example, enter the following command if you want to see the current directory’s system disk space usage in a human-readable format:

	df -h

These are some acceptable options to use:

    df -m displays information on the file system usage in MBs.
    df -k displays file system usage in KBs.
    df -T shows the file system type in a new column.

####16. du command
    

If you want to check how much space a file or a directory takes up, use the du command. You can run this command to identify which part of the system uses the storage excessively.

Remember, you must specify the directory path when using the du command. For example, to check /home/user/Documents enter:

	du /home/user/Documents

Adding a flag to the du command will modify the operation, such as:

    -s offers the total size of a specified folder.
    -m provides folder and file information in MB
    k displays information in KB.
    -h informs the last modification date of the displayed folders and files.

####17. head command
    

The head command allows you to view the first ten lines of a text. Adding an option lets you change the number of lines shown. The head command is also used to output piped data to the CLI.

Here’s the general syntax:

head [option] [file]

For instance, you want to view the first ten lines of note.txt, located in the current directory:

	head note.txt

Below are some options you can add:

    -n or –lines prints the first customized number of lines. For example, enter head -n 5 filename.txt to show the first five lines of filename.txt.
    -c or –bytes prints the first customized number of bytes of each file.
    -q or –quiet will not print headers specifying the file name.

####18. tail command
    

The tail command displays the last ten lines of a file. It allows users to check whether a file has new data or to read error messages.

Here’s the general format:

	tail [option] [file]

For example, you want to show the last ten lines of the colors.txt file:

	tail -n colors.txt


####19. diff command
    

Short for difference, the diff command compares two contents of a file line by line. After analyzing them, it will display the parts that do not match.

Programmers often use the diff command to alter a program instead of rewriting the entire source code.

Here’s the general format:

	diff [option] file1 file2

For example, you want to compare two text files – note.txt and note_update.txt:

	diff note.txt note_update.txt

Here are some acceptable options to add:

    -c displays the difference between two files in a context form.
    -u displays the output without redundant information.
    -i makes the diff command case insensitive.

####20. tar command
    

The tar command archives multiple files into a TAR file – a common Linux format similar to ZIP, with optional compression.

Here’s the basic syntax:

	tar [options] [archive_file] [file or directory to be archived]

For instance, you want to create a new TAR archive named newarchive.tar in the /home/user/Documents directory:

	tar -cvf newarchive.tar /home/user/Documents

The tar command accepts many options, such as:

    -x extracts a file.
    -t lists the content of a file.
    -u archives and adds to an existing archive file.

Check out the more practical examples to know more about the other functions.

####21. chmod command
    

chmod is a common command that modifies a file or directory’s read, write, and execute permissions. In Linux, each file is associated with three user classes – owner, group member, and others.

Here’s the basic syntax:

	chmod [option] [permission] [file_name]

For example, the owner is currently the only one with full permissions to change note.txt. To allow group members and others to read, write, and execute the file, change it to the -rwxrwxrwx permission type, whose numeric value is 777:

	chmod 777 note.txt

This command supports many options, including:

    -c or –changes displays information when a change is made.
    -f or –silent suppresses the error messages.
    -v or –verbose displays a diagnostic for each processed file.
####
22. chown command
    

The chown command lets you change the ownership of a file, directory, or symbolic link to a specified username.

Here’s the basic format:

	chown [option] owner[:group] file(s)

For example, you want to make linuxuser2 the owner of filename.txt:

chown linuxuser2 filename.txt

####23. jobs command
    

A job is a process that the shell starts. The jobs command will display all the running processes along with their statuses. Remember that this command is only available in csh, bash, tcsh, and ksh shells.

This is the basic syntax:

	jobs [options] jobID

To check the status of jobs in the current shell, simply enter jobs to the CLI.

Here are some options you can use:

    -l lists process IDs along with their information.
    -n lists jobs whose statuses have changed since the last notification.
    -p lists process IDs only.

####24. kill command
    

Use the kill command to terminate an unresponsive program manually. It will signal misbehaving applications and instruct them to close their processes.

To kill a program, you must know its process identification number (PID). If you don’t know the PID, run the following command:

	ps ux

After knowing what signal to use and the program’s PID, enter the following syntax:

	kill [signal_option] pid

There are 64 signals that you can use, but these two are among the most commonly used:

    SIGTERM requests a program to stop running and gives it some time to save all of its progress. The system will use this by default if you don’t specify the signal when entering the kill command.
    SIGKILL forces programs to stop, and you will lose unsaved progress.

For example, the program’s PID is 63773, and you want to force it to stop:

	kill SIGKILL 63773

####25. ping command
    

The ping command is one of the most used basic Linux commands for checking whether a network or a server is reachable. In addition, it is used to troubleshoot various connectivity issues.

Here’s the general format:

	ping [option] [hostname_or_IP_address]

For example, you want to know whether you can connect to Google and measure its response time:

	ping google.com

####26. wget command
    

The Linux command line lets you download files from the internet using the wget command. It works in the background without hindering other running processes.

The wget command retrieves files using HTTP, HTTPS, and FTP protocols. It can perform recursive downloads, which transfer website parts by following directory structures and links, creating local versions of the web pages.

To use it, enter the following command:

	wget [option] [url]

For example, enter the following command to download the latest version of WordPress:

	wget https://wordpress.org/latest.zip

####27. uname command
    

The uname or unix name command will print detailed information about your Linux system and hardware. This includes the machine name, operating system, and kernel. To run this command, simply enter uname into your CLI.

Here’s the basic syntax:

	uname [option]

These are the acceptable options to use:

    -a prints all the system information.
    -s prints the kernel name.
    -n prints the system’s node hostname.

####28. top command
    

The top command in Linux Terminal will display all the running processes and a dynamic real-time view of the current system. It sums up the resource utilization, from CPU to memory usage.

The top command can also help you identify and terminate a process that may use too many system resources.

To run the command, simply enter top into the CLI.

####29. history command

With history, the system will list up to 500 previously executed commands, allowing you to reuse them without re-entering. Keep in mind that only users with sudo privileges can execute this command. How this utility runs also depends on which Linux shell you use.

To run it, enter the command below:

	history [option]

This command supports many options, such as:

    -c clears the complete history list.
    -d offset deletes the history entry at the OFFSET position.
    -a appends history lines.

####30. man command

The man command provides a user manual of any commands or utilities you can run in Terminal, including the name, description, and options.

It consists of nine sections:

    Executable programs or shell commands
    System calls
    Library calls
    Games
    Special files
    File formats and conventions
    System administration commands
    Kernel routines
    Miscellaneous

To display the complete manual, enter:

	man [command_name]

For example, you want to access the manual for the ls command:

	man ls

Enter this command if you want to specify the displayed section:

	man [option] [section_number] [command_name]

For instance, you want to see section 2 of the ls command manual:

	man 2 ls

####31. echo command

The echo command is a built-in utility that displays a line of text or string using the standard output. Here’s the basic syntax:

	echo [option] [string]

For example, you can display the text Hostinger Tutorials by entering:

	echo “Hostinger Tutorials”

This command supports many options, such as:

    -n displays the output without the trailing newline.
    -e enables the interpretation of the following backslash escapes:

    \a plays sound alert.
    \b removes spaces in between a text.

    \c produces no further output.
    -E displays the default option and disables the interpretation of backslash escapes.

####32. zip, unzip commands

Use the zip command to compress your files into a ZIP file, a universal format commonly used on Linux. It can automatically choose the best compression ratio.

The zip command is also useful for archiving files and directories and reducing disk usage.

To use it, enter the following syntax:

	zip [options] zipfile file1 file2….

For example, you have a file named note.txt that you want to compress into archive.zip in the current directory:

	zip archive.zip note.txt

On the other hand, the unzip command extracts the zipped files from an archive. Here’s the general format:

	unzip [option] file_name.zip

So, to unzip a file called archive.zip in the current directory, enter:

	unzip archive.zip

####33. hostname command

Run the hostname command to know the system’s hostname. You can execute it with or without an option. Here’s the general syntax:

	hostname [option]

There are many optional flags to use, including:

    -a or –alias displays the hostname’s alias.
    -A or –all-fqdns displays the machine’s Fully Qualified Domain Name (FQDN).
    -i or –ip-address displays the machine’s IP address.

For example, enter the following command to know your computer’s IP address:

	hostname -i

####34. useradd, userdel commands

Linux is a multi-user system, meaning more than one person can use it simultaneously. useradd is used to create a new account, while the passwd command allows you to add a password. Only those with root privileges or sudo can run the useradd command.

When you use the useradd command, it performs some major changes:

    Edits the /etc/passwd, /etc/shadow, /etc/group, and /etc/gshadow files for the newly created accounts.
    Creates and populates a home directory for the user.
    Sets file permissions and ownerships to the home directory.

Here’s the basic syntax:

	useradd [option] username

To set the password:

passwd the_password_combination

For example, to add a new person named John, enter the following command simultaneously:

	useradd John

	passwd 123456789

To delete a user account, use the userdel command:

	userdel username

####35. apt-get command

apt-get is a command line tool for handling Advanced Package Tool (APT) libraries in Linux. It lets you retrieve information and bundles from authenticated sources to manage, update, remove, and install software and its dependencies.

Running the apt-get command requires you to use sudo or root privileges.

Here’s the main syntax:

	apt-get [options] (command)

These are the most common commands you can add to apt-get:

    update synchronizes the package files from their sources.
    upgrade installs the latest version of all installed packages.
    check updates the package cache and checks broken dependencies.

####36. nano, vi, jed commands

Linux allows users to edit and manage files via a text editor, such as nano, vi, or jed. nano and vi come with the operating system, while jed has to be installed.

The nano command denotes keywords and can work with most languages. To use it, enter the following command:

	nano [filename]

vi uses two operating modes to work – insert and command. insert is used to edit and create a text file. On the other hand, the command performs operations, such as saving, opening, copying, and pasting a file.

To use vi on a file, enter:

	vi [filename]

jed has a drop-down menu interface that allows users to perform actions without entering keyboard combinations or commands. Like vi, it has modes to load modules or plugins to write specific texts.

To open the program, simply enter jed to the command line.

####37. alias, unalias commands

alias allows you to create a shortcut with the same functionality as a command, file name, or text. When executed, it instructs the shell to replace one string with another.

To use the alias command, enter this syntax:

	alias Name=String

For example, you want to make k the alias for the kill command:

	alias k=’kill’

On the other hand, the unalias command deletes an existing alias.

Here’s what the general syntax looks like:

	unalias [alias_name]

####38. su command

The switch user or su command allows you to run a program as a different user. It changes the administrative account in the current log-in session. This command is especially beneficial for accessing the system through SSH or using the GUI display manager when the root user is unavailable.

Here’s the general syntax of the command:

	su [options] [username [argument]]

When executed without any option or argument, the su command runs through root privileges. It will prompt you to authenticate and use the sudo privileges temporarily.

Here are some acceptable options to use:

    -p or –preserve-environment keeps the same shell environment, consisting HOME, SHELL, USER, and LOGNAME.
    -s or –shell lets you specify a different shell environment to run.
    -l or –login runs a login script to switch to a different username. Executing it requires you to enter the user’s password.

####39. htop command

The htop command is an interactive program that monitors system resources and server processes in real time. It is available on most Linux distributions, and you can install it using the default package manager.

Compared to the top command, htop has many improvements and additional features, such as mouse operation and visual indicators.

To use it, run the following command:

	htop [options]

You can also add options, such as:

    -d or –delay shows the delay between updates in tenths of seconds.
    -C or –no-color enables the monochrome mode.
    -h or –help displays the help message and exit.

####40. ps command

The process status or ps command produces a snapshot of all running processes in your system. The static results are taken from the virtual files in the /proc file system.

Executing the ps command without an option or argument will list the running processes in the shell along with:

    The unique process ID (PID)
    The type of the terminal (TTY)
    The running time (TIME)
    The command that launches the process (CMD)

Here are some acceptable options you can use:

    -T displays all processes associated with the current shell session.
    -u username lists processes associated with a specific user.
    -A or -e shows all the running processes.

	
	
:end: 
	
	
#
# Linux Basic CMDs
	
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



 display:

    All users 

    All groups
    
    

Display users & groups list: 


You can display with the help of compgen builtin command as follows:

    To display all users run following command:

    compgen -u

    To display all groups run following command:

    compgen -g

However you can also display all users by cut -d ":" -f 1 /etc/passwd.


//

Here we are going to use getent for the detailed the info

We can list the user with the following command:

getent passwd

We can list the group as follows:

    getent group

To fetch detail a specific user

    getent passwd lalit



You can also list a specific group’s membership using the following command:

     getent group www-data



Listing All Groups:

     less /etc/group



To get a list of all groups, type the following command:

	getent group

You can also use awk or cut to print only the first field containing the name of the group:

	getent group | awk -F: '{ print $1}'

	getent group | cut -d: -f1
	
	
--------------------------------------------------------------------------------


Get a List of all Users using the getent Command :

	getent passwd

	getent passwd | awk -F: '{ print $1}'
	getent passwd | cut -d: -f1


Check whether a user exists in the Linux system:

	getent passwd | grep jack
	
	getent passwd jack
	
	getent passwd | wc -l
	
	
System and Normal Users: 

	grep -E '^UID_MIN|^UID_MAX' /etc/login.defs
	
	getent passwd {1000..60000}
	
	
Your system UID_MIN and UID_MIN values may be different so the more generic version of the command above would be:

eval getent passwd {$(awk '/^UID_MIN/ {print $2}' /etc/login.defs)..$(awk '/^UID_MAX/ {print $2}' /etc/login.defs)}

If you want to print only the usernames just pipe the output to the cut command:

eval getent passwd {$(awk '/^UID_MIN/ {print $2}' /etc/login.defs)..$(awk '/^UID_MAX/ {print $2}' /etc/login.defs)} | cut -d: -f1
	
	
	
	
#

[Top](#top)
<a name="linux-networking-cmds"></a>

# Linux Networking Commands with Examples:


    ifconfig        //showing the IP address of 3 networks, Ethernet, local network, and WLAN
    ip
    traceroute
    tracepath
    ping
    netstat
    ss
    dig
    nslookup
    route
    host
    arp
    iwconfig
    hostname
    curl or wget
    mtr
    whois
    ifplugstatus
    iftop
    tcpdum



ifconfig

	ifconfig eth0
	ifconfig lo
	ifconfig wlan0


To assign an IP address and Gateway to an interface:

 ifconfig eth0 <address> netmask <address> 


To enable or disable an interface:

ifup eth0                 //To enable an interface
ifdown eth0              //To disable an interface
ifconfig eth0 mtu xxxx   //To set the size of MTU


ip

ip a 
ip addr

ip a show eth0
ip a how lo
ip a show wlan0


	
traceroute
traceroute <destination>

sudo apt-get install inetutils-traceroute

Ex:
traceroute google.com
traceroute -n google.com
sudo traceroute -I google.com

sudo traceroute -T google.com



4.tracepath

tracepath <destination> 

Example:   

tracepath mindmajix.com


5. ping


Syntax:

ping <destination> 

Example:
Command: 

ping google.com
ping -c <number> <destination>


6. netstat

Syntax:

netstat


1) To display the programs 

Syntax:

netstat -p

2) To get the details of the ports

Syntax:

netstat -s

3) To get the information of the routing table 

Syntax:

netstat -r



7. ss

syntax: 
 
 ss
 
 ss -ta
 ss -ua
 ss -xa
 
 ss -lt  
ss -lu  
ss -lx



    To get a list of all the established sockets of TCP for IPV4,

Command: 

$ ss -t4 state established

    To get a list of all closed TCP sockets,

Command:

 $ ss -t4 state closed
 
 
 
    To get a list of all connected ports for a specific IP address:

Command:

 $ ss dst XXX.XXX.XXX.XXX
 
 
 
 
8. dig (Domain Information)

Syntax:

dig <domainName> 

Example:

 $ dig google.com
 
Command:

 $ dig google.com MX

    To get all types of records at once, use the keyword ANY ass below:

Command:

 $ dig google.com ANY
 
 
 
 
9.nslookup


Linux nslookup is also a command used for DNS related queries. It is the older version of dig.

Syntax:

 nslookup <domainName>

Example:

nslookup mindmajix.com




10.route

Linux route command displays and manipulates the routing table existing for your system.


Displaying numerical IP address

route -n


Toa add a gateway

Syntax:

 route add default gw <IP address> 
 
 
 To get routing information
 
 Syntax:

 route -Cn
 
 
11. host

Linux host command displays the domain name for a given IP address and IP address for a given hostname. It is also used to fetch DNS lookup for DNS related query.

Example:

host mindmajix.com  
host 149.77.21.18


Syntax:

host -t <resourceName> 


12.arp

Linux arp command stands for Address Resolution Protocol. It is used to view and add content to the kernel's ARP table.

Syntax:

arp

Command:

 $ arp -n

You can also delete the entries from the arp table, as shown below.
Command:

$ arp -d HWADDR



13.iwconfig

Linux iwconfig is used to configure the wireless network interface. It is used to set and view the basic WI-FI details like SSID and encryption. To know more about this command, refer to the man page.

Syntax:

iwconfig

Output:
14.hostname

Linux hostname is the simple command used to view and set the hostname of a system.

Syntax:

hostname

Output:

    To set the hostname

Use the syntax below to set the hostname.

Syntax:

 sudo hostname <newName>

The hostname set through this command is not permanent. It will be reset to the name in the hostname file back when the system reboots.

In order to permanently set a hostname, you have to re-write the hostname in the hostname file, present on the server. Once set, you have to reboot the box.

In Ubuntu, /etc/hostname file is used.

In RHEL, /etc/sysconfig/network is used.
15.curl & wget

Linux curl and wget commands are used in downloading files from the internet through CLI. The curl command has to be used with the option "O" to fetch the file, while the wget command is used directly.

Below are the syntax and the example for the two commands.

a) Curl

Syntax:

curl -O <fileLink>

Example:

 curl -O google.com/doodles/childrens-day-2014-multiple-countries 

b) wget

Syntax:

 wget <fileLink> 

Example:

wget google.com/doodles/new-years-day-2012

Output:
16.mtr

Linux mtr command is a combination of ping and the traceroute command. It continuously displays information regarding the packets sent with the ping time of each hop. It is also used to view the network issues.

Syntax:

mtr <path>

Example:

$ mtr google.com

Output:

You can use mtr with –report option. It sends 10 packets to each hop that is found on the way.

Syntax:

$ mtr --report <path>

17.whois

Linux whois command is used to fetch all the information related to a website. You can get all the information about a website including the registration and the owner information.

Syntax:

whois <websiteName>

Example:

whois mindmajix.com

Output:
18.ifplugstatus

Linux ifplugstatus command is used to check if a cable is plugged into the network interface. This command is not directly available on Ubuntu. You can install this using the command below:
Command:

sudo apt-get install ifplugd

Syntax:

 ifplugstatus

Output:

In the output above, "link beat detected" means that the cable is plugged in.
19.iftop

Linux iftop command is used in traffic monitoring. 

Use the following command to download iftop on your system.
Command:

 $ wget http://www.ex-parrot.com/pdw/iftop/download/iftop-0.17.tar.gz

This will give a zip file. To extract it, use the following command,
Command:

$  tar zxvf iftop-0.17.tar.gz

You can compile this using,
Commands:

$ cd iftop-0.17
$  ./configure
$ make
$ make install

Now, run the tool as a root user,

 $ sudo iftop -I <interface>

Output:

You can view the ports using the -P option in command like this,
Command:

 $ sudo iftop -P

You can use the -B command to get the data in bytes, instead of bits (which is shown by default).
Command:

 $ iftop -B

20.tcpdump

Linux tcpdump command is the most used command in network analysis among other Linux network commands. It captures the traffic that is passing through the network interface and displays it. 

This kind of access to the packet will be crucial when troubleshooting the network.

Syntax:

 $ tcpdump -i <network_device>

Output:

You can also specify the protocol (TCP, UDP, ICMP, and others) in the command like this,
Command:

 $ tcpdump -i <network_device> tcp

To specify the port, use the command,
Command:

 $ tcpdump -i <network_device> port 80

tcpdump command keeps executing and sending packets unless canceled. Hence you can specify the number of events to be captured to control the continuous execution.
Related  Article: Linux Tutorial for Beginners
Command:

 $ tcpdump -c 20 -i <network_device>

You can

also specify the IP you are capturing from, using the tag src or dst.
Command:

 $ tcpdump -c 20 -i <network_device> src XXX.XXX.XXX.XXX

You can save the network traffic captured at an instant, into a file and use it later. This can be done using the command below,

a) Save into a file
Command:

$ tcpdump -w /path/ -i <network_device>

b) Read from the file
Command:

 $ tcpdump -r /path

These were the most essential network commands in Linux that are used frequently for network analysis and troubleshooting.

	
	
:end:	
	
	
	
[Top](#top)
	
<a name="alpine-basic-cmds"</a>	
	
# Alpine Basicd Commands:




10 Alpine Linux apk Command Examples:
	

apk-command

I am new Alpine Linux system admin user. How do I use apk command line utility for the package management on Apline Linux server running in cloud or a Linux container? How can I use the Alpine package manager?

apk command details
	
	Description	Alpine Linux package manager
	
	Category	        Package Manager
	Difficulty level	Easy
	Root privileges	Yes
	OS compatibility	Alpine • Linux
	Est. reading time	10 minutes
	Table of contents ↓

	    1 Syntax
	    2 Examples
	    3 Update the package list
	    4 Search for package
	    5 Install a package
	    6 Remove/delete a package
	    7 Upgrade running system
	    8 List installed packages
	    9 Show statistics
	    10 See also

Alpine Linux is a free and open-source Linux kernel-based distro. It uses musl and busybox as init system. This distro is designed with security in mind and targeted at power users who want a secure machine. Alpine comes with PaX and grsecurity for Linux kernel protection, including all binaries with stack smashing protection. APK stands for Alpine Linux package keeper (manager). One can use the apk command to delete, install, upgrade, or list software on a running Alpine Linux based system. Like most modern Linux distros, all software packages for Alpine Linux are digitally signed to avoid security problems. You can install packages from a local disk (such as CDROM or a USB stick) or the internet archive location using apk command, the Alpine package manager for binary packages, instead of compiling them from the source.



The list of repositories is stored in /etc/apk/repositories configuration file. Use the cat command to view /etc/apk/repositories file. Alpine Linux package often has the .apk extension called “a-packs”. The apk command is equivalent to apt/apt-get command on Debian/Ubuntu, yum command on CentOS/RHEL Linux, or zypper command on SuSE/OpenSUSE Linux..
Purpose

    Use apk for installing, upgrading, configuring, and removing apps/programs for an Alpine Linux operating system in a consistent manner.

Syntax

The basic syntax is as follows:

	apk [options] command
	apk [options] command pkgName
	apk [options] command pkgName1 pkgName2

Alpine Linux apk command examples

Let us see how to use the apk command to install security updates or new set of packages on an Alpine Linux server.
How to update the package list

To update your package list, enter:

	apk update


The syntax is:
	
	apk search pkgName

For example, search a package named htop, run:

	apk search htop


To search and display description:

	apk search -v -d 'htop'


To list all packages available, along with their descriptions

	apk search -v

How do I search package by wildcards?

The syntax is as follows to search all php7 packages or php5 packages:
	
	apk search -v 'php5*'
	
### OR ###

	apk search -v 'php7*'

How to install a package(s) by name

The syntax is:
	
	apk add pkgName
	apk add pkgName1 pkgName2

To install a htop package, run:

	apk add htop


To install Apache2 along with PHP7 and modules, run:

	apk add apache2 php7-apache2 php7-gd php7-mysqli

Interactive install or upgrade

We can force confirmation before performing certain operations by passing the -i option:
	
	apk -i add nginx

	apk -i upgrade

The following packages will be upgraded:
  libcrypto1.1 libssl1.1 alpine-base linux-lts xtables-addons-lts openssh-keygen openssh-client openssh-sftp-server openssh-server-common openssh-server openssh openssl zfs-lts
After this operation, 16 KiB of additional disk space will be used.
Do you want to continue [Y/n]?

Simulation with apk command

We can simulate the requested operation without making any changes. Helpful to see what packages will be upgrades or what will be done on the Alpine Linux system:
	
	apk -s command
	apk -s add nginx

	apk -s upgrade

In other words, nothing was installed or upgraded on the system, but you will know precisely what apk was about to do.
How to hold a specific package back and not upgrade it

If you want to upgrade Alpine Linux system, but keep or hold a specific package add version number. For instance, to hold the bash package to the version 	
	5.0.0-r0 level or lower, run:
	
	apk add bash=5.0.0-r0

One can do regex based version matching to hold the version to a major/minor release. For example:
	
	apk add bash=~5.0

Now, upgrade the system. However, apk will upgrade the entire system, keeping the bash package at the 5.0.0-r0 or lower level:
	
	apk upgrade

It is possible to remove holding. For example, make sure upgrade bash to the current lastest version, run:

	apk add bash>5.0.0-r0

Alpine Linux apk Command Examples:
	
How do install a local .apk file package?

The syntax is as follows to add a local package named foo.apk:
	
	apk add --allow-untrusted /path/to/foo.apk

	apk add --allow-untrusted pkg1.apk pkg2.apk
	
How to remove or delete a package(s) by name

The syntax is:
	
	apk del pkgName
	apk del pkgName1 pkgName2

To delete a htop package run:

	apk del htop

How do I delete old packages caches on Alpine Linux?

To remove out older versions of packages, run the clean command as follows:
	
	apk cache clean
	
## or ##
	apk -v cache clean

One can also clean cache and download missing packages in one step:

	apk cache -v sync
	
How to upgrade running Alpine Linux

The syntax is:
	
	apk update && apk upgrade

You can create a bash shell alias as follows in ~/.bashrc
echo "alias update='apk update && apk upgrade'" >> /.bashrc

Run it as follows:

	update
	
How do I upgrade selected packages only?

The syntax is
	
	apk add -u pkgName

To upgrade a htop only package:
	
	apk update

	apk add -u htop
	
How do I list installed packages?

The syntax is:
	apk info
	
# filter out info using the grep command #
	
	apk info -vv | grep 'foo'
	
# Get verbose outputs and sort it using the sort command #

	apk info -vv | sort

Fig.02: How do I show/list installed packages in Alpine Linux

Fig.02: How do I show/list installed packages in Alpine Linux
	
Find out which package a file belongs to..

to determine which package a file named /etc/passwd or /sbin/apk belongs to:
	
	apk info --who-owns /etc/passwd
	
/etc/passwd is owned by alpine-baselayout-3.0.4-r0

	apk info --who-owns /sbin/apk
	
/sbin/apk is owned by apk-tools-2.6.8-r2
	
List contents of the PACKAGE

	apk -L info pkgName

	apk -L info htop


Check if PACKAGE is installed

	apk -e info pkgName

	apk -e info atop

No output displayed if PACKAGE is NOT installed.
	
List packages that the PACKAGE depends on

	apk -R info atop

	apk -R info atop


List all packages depending on PACKAGE

Pass the -r to the apk command:
	
	apk info -r pkgNameHere
	
# For example, list all pkgs depending upon GNU/bash #

	apk info -r bash

Sample outputs:

bash-5.1.16-r0 is required by:
bash-completion-2.11-r4
wireguard-tools-wg-quick-1.0.20210914-r0

Show installed size of PACKAGE

You need to pass the -s to the apk command as follows:
	
	apk info -s pkgName

# Let us list size of a package named 'atop' #

	apk info -s atop


Print description for PACKAGE

Want to get a short description about APK package? Try passing the -d as follows:

	apk info -d pkgName

	apk info -d bash

Here is what I see:

bash-5.1.16-r0 description:
	
The GNU Bourne Again shell

Print all information about PACKAGE

Pass the -a option to the apk command as follows:
	
	apk info -a pkgName
	
# Get info about GNU/bash, run: #

	apk info -a bash


apk command options and examples:

Table 1: 	
	
	apk update 	Update the package list 	apk update
	apk upgrade 	Upgrade the system 	        apk update
	apt ugrade
	apk add pkg 	Add a package 	                apk add apache
	apk del pkg 	Delete a package 	        apk del nginx
	apk search -v 	Search for packages 	        apk search -v
	apk search -v -d 'nginx*‘
	apk search -v 'apache*'
	apk info 	List all installed pacakges 	                                        apk info
	apk fix 	Repair package or upgrade it without modifying main dependencies 	apk fix
	apk policy pkg 	Show repository policy for packages 	                                apk policy bash
	apk stats 	Show statistics about repositories and installations 	                apk stats
	See also

You learned about apk command and everyday examples to add, remove and manage packages on Alpine Linux. See also:

    	/etc/apk/repositories file.
	
    The apk command has many more options. Hence, read apk command manual page using the man command or help command

man apk
	apk --help
	
# Want to get help about add/del commands? #
	
	apk add --help

#
	apk add docker
	apk del docker
	docker context use
	docker context ls
	docker context show
	service docker start
	service docker status
	service docker stop or restart
	unset DOCKER_HOST
	export DOCKER_HOST=unix:///var/run/docker.sock

:end:
	
#
Ubuntu22.04: 

#
Kali:


#
CentOS 8 Stream:

#
Red Hat: 
#

:end:
#
		
	
<a name="top"></a>
