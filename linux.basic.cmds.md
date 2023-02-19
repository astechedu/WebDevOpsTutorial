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

---> Basic Linux Commands <-----


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

1. sudo command
   ------------

Short for superuser do, sudo is one of the most popular basic Linux commands that lets you perform tasks that require administrative or root permissions.

When using sudo, the system will prompt users to authenticate themselves with a password. Then, the Linux system will log a timestamp as a tracker. By default, every root user can run sudo commands for 15 minutes/session.

If you try to run sudo in the command line without authenticating yourself, the system will log the activity as a security event.

Here’s the general syntax:

sudo (command)

You can also add an option, such as:

    -k or –reset-timestamp invalidates the timestamp file.
    -g or –group=group runs commands as a specified group name or ID.
    -h or –host=host runs commands on the host.

2. pwd command
   -----------

Use the pwd command to find the path of your current working directory. Simply entering pwd will return the full current path – a path of all the directories that starts with a forward slash (/). For example, /home/username.

The pwd command uses the following syntax:

pwd [option]

It has two acceptable options:

    -L or –logical prints environment variable content, including symbolic links.
    -P or –physical prints the actual path of the current directory.

3. cd command
   ----------

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

4. ls command
   ----------

The ls command lists files and directories within a system. Running it without a flag or parameter will show the current working directory’s content.

To see other directories’ content, type ls followed by the desired path. For example, to view files in the Documents folder, enter:

ls /home/username/Documents

Here are some options you can use with the ls command:

    ls -R lists all the files in the subdirectories.
    ls -a shows hidden files in addition to the visible ones.
    ls -lh shows the file sizes in easily readable formats, such as MB, GB, and TB.

5. cat command
   -----------

Concatenate, or cat, is one of the most frequently used Linux commands. It lists, combines, and writes file content to the standard output. To run the cat command, type cat followed by the file name and its extension. For instance:

cat filename.txt.

Here are other ways to use the cat command:

    cat > filename.txt creates a new file.
    cat filename1.txt filename2.txt > filename3.txt merges filename1.txt and filename2.txt and stores the output in filename3.txt.
    tac filename.txt displays content in reverse order.

6. cp command
   ----------

Use the cp command to copy files or directories and their content. Take a look at the following use cases.

To copy one file from the current directory to another, enter cp followed by the file name and the destination directory. For example:

cp filename.txt /home/username/Documents

To copy files to a directory, enter the file names followed by the destination directory:

cp filename1.txt filename2.txt filename3.txt /home/username/Documents

To copy the content of a file to a new file in the same directory, enter cp followed by the source file and the destination file:

cp filename1.txt filename2.txt

To copy an entire directory, pass the -R flag before typing the source directory, followed by the destination directory:

cp -R /home/username/Documents /home/username/Documents_backup

7. mv command
   ----------

The primary use of the mv command is to move and rename files and directories. Additionally, it doesn’t produce an output upon execution.

Simply type mv followed by the filename and the destination directory. For example, you want to move filename.txt to the /home/username/Documents directory:

mv filename.txt /home/username/Documents.

You can also use the mv command to rename a file:

mv old_filename.txt new_filename.txt

8. mkdir command
   -------------

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

9. rmdir command
   -------------

To permanently delete an empty directory, use the rmdir command. Remember that the user running this command should have sudo privileges in the parent directory.

For example, you want to remove an empty subdirectory named personal1 and its main folder mydir:

rmdir -p mydir/personal1

10. rm command
    ----------

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

11. touch command
    -------------

The touch command allows you to create an empty file or generate and modify a timestamp in the Linux command line.

For example, enter the following command to create an HTML file named Web in the Documents directory:

touch /home/username/Documents/Web.html

12. locate command
    --------------

The locate command can find a file in the database system.

Moreover, adding the -i argument will turn off case sensitivity, so you can search for a file even if you don’t remember its exact name.

To look for content that contains two or more words, use an asterisk (*). For example:

locate -i school*not

The command will search for files that contain the words school and note, whether they use uppercase or lowercase letters.

13. find command
    ------------

Use the find command to search for files within a specific directory and perform subsequent operations. Here’s the general syntax:

find [option] [path] [expression]

For example, you want to look for a file called notes.txt within the home directory and its subfolders:

find /home -name notes.txt

Here are other variations when using find:

    find -name filename.txt to find files in the current directory.
    find ./ -type d -name directoryname to look for directories.

14. grep command
    ------------

Another basic Linux command on the list is grep or global regular expression print. It lets you find a word by searching through all the texts in a specific file.

Once the grep command finds a match, it prints all lines that contain the specific pattern. This command helps filter through large log files.

For example, you want to search for the word blue in the notepad.txt file:

grep blue notepad.txt

The command’s output will display lines that contain blue.

15. df command
    ----------

Use the df command to report the system’s disk space usage, shown in percentage and kilobyte (KB). Here’s the general syntax:

df [options] [file]

For example, enter the following command if you want to see the current directory’s system disk space usage in a human-readable format:

df -h

These are some acceptable options to use:

    df -m displays information on the file system usage in MBs.
    df -k displays file system usage in KBs.
    df -T shows the file system type in a new column.

16. du command
    ----------

If you want to check how much space a file or a directory takes up, use the du command. You can run this command to identify which part of the system uses the storage excessively.

Remember, you must specify the directory path when using the du command. For example, to check /home/user/Documents enter:

du /home/user/Documents

Adding a flag to the du command will modify the operation, such as:

    -s offers the total size of a specified folder.
    -m provides folder and file information in MB
    k displays information in KB.
    -h informs the last modification date of the displayed folders and files.

17. head command
    ------------

The head command allows you to view the first ten lines of a text. Adding an option lets you change the number of lines shown. The head command is also used to output piped data to the CLI.

Here’s the general syntax:

head [option] [file]

For instance, you want to view the first ten lines of note.txt, located in the current directory:

head note.txt

Below are some options you can add:

    -n or –lines prints the first customized number of lines. For example, enter head -n 5 filename.txt to show the first five lines of filename.txt.
    -c or –bytes prints the first customized number of bytes of each file.
    -q or –quiet will not print headers specifying the file name.

18. tail command
    ------------

The tail command displays the last ten lines of a file. It allows users to check whether a file has new data or to read error messages.

Here’s the general format:

tail [option] [file]

For example, you want to show the last ten lines of the colors.txt file:

tail -n colors.txt


19. diff command
    ------------

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

20. tar command
    -----------

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

21. chmod command
    -------------

chmod is a common command that modifies a file or directory’s read, write, and execute permissions. In Linux, each file is associated with three user classes – owner, group member, and others.

Here’s the basic syntax:

chmod [option] [permission] [file_name]

For example, the owner is currently the only one with full permissions to change note.txt. To allow group members and others to read, write, and execute the file, change it to the -rwxrwxrwx permission type, whose numeric value is 777:

chmod 777 note.txt

This command supports many options, including:

    -c or –changes displays information when a change is made.
    -f or –silent suppresses the error messages.
    -v or –verbose displays a diagnostic for each processed file.

22. chown command
    -------------

The chown command lets you change the ownership of a file, directory, or symbolic link to a specified username.

Here’s the basic format:

chown [option] owner[:group] file(s)

For example, you want to make linuxuser2 the owner of filename.txt:

chown linuxuser2 filename.txt

23. jobs command
    ------------

A job is a process that the shell starts. The jobs command will display all the running processes along with their statuses. Remember that this command is only available in csh, bash, tcsh, and ksh shells.

This is the basic syntax:

jobs [options] jobID

To check the status of jobs in the current shell, simply enter jobs to the CLI.

Here are some options you can use:

    -l lists process IDs along with their information.
    -n lists jobs whose statuses have changed since the last notification.
    -p lists process IDs only.

24. kill command
    ------------

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

25. ping command
    ------------

The ping command is one of the most used basic Linux commands for checking whether a network or a server is reachable. In addition, it is used to troubleshoot various connectivity issues.

Here’s the general format:

ping [option] [hostname_or_IP_address]

For example, you want to know whether you can connect to Google and measure its response time:

ping google.com

26. wget command
    ------------

The Linux command line lets you download files from the internet using the wget command. It works in the background without hindering other running processes.

The wget command retrieves files using HTTP, HTTPS, and FTP protocols. It can perform recursive downloads, which transfer website parts by following directory structures and links, creating local versions of the web pages.

To use it, enter the following command:

wget [option] [url]

For example, enter the following command to download the latest version of WordPress:

wget https://wordpress.org/latest.zip

27. uname command
    -------------

The uname or unix name command will print detailed information about your Linux system and hardware. This includes the machine name, operating system, and kernel. To run this command, simply enter uname into your CLI.

Here’s the basic syntax:

uname [option]

These are the acceptable options to use:

    -a prints all the system information.
    -s prints the kernel name.
    -n prints the system’s node hostname.

28. top command
    -----------

The top command in Linux Terminal will display all the running processes and a dynamic real-time view of the current system. It sums up the resource utilization, from CPU to memory usage.

The top command can also help you identify and terminate a process that may use too many system resources.

To run the command, simply enter top into the CLI.

29. history command

With history, the system will list up to 500 previously executed commands, allowing you to reuse them without re-entering. Keep in mind that only users with sudo privileges can execute this command. How this utility runs also depends on which Linux shell you use.

To run it, enter the command below:

history [option]

This command supports many options, such as:

    -c clears the complete history list.
    -d offset deletes the history entry at the OFFSET position.
    -a appends history lines.

30. man command

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

31. echo command

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

32. zip, unzip commands

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

33. hostname command

Run the hostname command to know the system’s hostname. You can execute it with or without an option. Here’s the general syntax:

hostname [option]

There are many optional flags to use, including:

    -a or –alias displays the hostname’s alias.
    -A or –all-fqdns displays the machine’s Fully Qualified Domain Name (FQDN).
    -i or –ip-address displays the machine’s IP address.

For example, enter the following command to know your computer’s IP address:

hostname -i

34. useradd, userdel commands

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

35. apt-get command

apt-get is a command line tool for handling Advanced Package Tool (APT) libraries in Linux. It lets you retrieve information and bundles from authenticated sources to manage, update, remove, and install software and its dependencies.

Running the apt-get command requires you to use sudo or root privileges.

Here’s the main syntax:

apt-get [options] (command)

These are the most common commands you can add to apt-get:

    update synchronizes the package files from their sources.
    upgrade installs the latest version of all installed packages.
    check updates the package cache and checks broken dependencies.

36. nano, vi, jed commands

Linux allows users to edit and manage files via a text editor, such as nano, vi, or jed. nano and vi come with the operating system, while jed has to be installed.

The nano command denotes keywords and can work with most languages. To use it, enter the following command:

nano [filename]

vi uses two operating modes to work – insert and command. insert is used to edit and create a text file. On the other hand, the command performs operations, such as saving, opening, copying, and pasting a file.

To use vi on a file, enter:

vi [filename]

jed has a drop-down menu interface that allows users to perform actions without entering keyboard combinations or commands. Like vi, it has modes to load modules or plugins to write specific texts.

To open the program, simply enter jed to the command line.

37. alias, unalias commands

alias allows you to create a shortcut with the same functionality as a command, file name, or text. When executed, it instructs the shell to replace one string with another.

To use the alias command, enter this syntax:

alias Name=String

For example, you want to make k the alias for the kill command:

alias k=’kill’

On the other hand, the unalias command deletes an existing alias.

Here’s what the general syntax looks like:

unalias [alias_name]

38. su command

The switch user or su command allows you to run a program as a different user. It changes the administrative account in the current log-in session. This command is especially beneficial for accessing the system through SSH or using the GUI display manager when the root user is unavailable.

Here’s the general syntax of the command:

su [options] [username [argument]]

When executed without any option or argument, the su command runs through root privileges. It will prompt you to authenticate and use the sudo privileges temporarily.

Here are some acceptable options to use:

    -p or –preserve-environment keeps the same shell environment, consisting HOME, SHELL, USER, and LOGNAME.
    -s or –shell lets you specify a different shell environment to run.
    -l or –login runs a login script to switch to a different username. Executing it requires you to enter the user’s password.

39. htop command

The htop command is an interactive program that monitors system resources and server processes in real time. It is available on most Linux distributions, and you can install it using the default package manager.

Compared to the top command, htop has many improvements and additional features, such as mouse operation and visual indicators.

To use it, run the following command:

htop [options]

You can also add options, such as:

    -d or –delay shows the delay between updates in tenths of seconds.
    -C or –no-color enables the monochrome mode.
    -h or –help displays the help message and exit.

40. ps command

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
----------------------------------------------------------------------------------------





















































--------------------------




Ubuntu22.04: 



---------------------------

Kali:



---------------------------

CentOS 8 Stream:


------------------------------------------
Red Hat: 

-----------------------------------------------


















------------------------

CentOS 8 Stream (Nothing is installing)


Working This settings: 


VirtualBox 7 In Windows 10 64-bit (CentOS 8 Stream)

This is used for CentOS Linux, but in the case of centos appstream use the following trick

Go to /etc/yum.repos.d.

Add in CentOS-Stream-AppStream.repo
baseurl=http://mirror.centos.org/centos/8-stream/AppStream/x86_64/os/

Add in CentOS-Stream-BaseOS.repo
baseurl=http://mirror.centos.org/centos/8-stream/BaseOS/x86_64/os/

Add in CentOS-Stream-Extras.repo
baseurl=http://mirror.centos.org/centos/8-stream/extras/x86_64/os/

CentOS-Stream-Extras-common.repo
baseurl=https://vault.centos.org/centos/8-stream/extras/Source/extras-common/

-----------------------------------------------------------------------------------------------






Alpine Linux Image: 


https://www.mowson.org/karl/2016/2016-05-20_alpinelinux_vm_under_virtualbox/

alpine-3.3.3-x86_64.iso


Basic Alpine Linux Install

    Start the VM.
    Login as root (no password required).

Run "setup-alpine", and configure as follows:

    keyboard layout = "us"
    keyboard variant = "us"
    system hostname = whatever suits you
    initialise interface: "eth0"
    "dhcp"
    no manual setup
    enter root password, as desired.
    timezone: "Pacific/Auckland" (or whatever suits you)
    HTTP/FTP proxy URL: [none]
    Detect and add fastest mirror (f)
    SSH server: "openssh"
    NTP client: "chrony"
    install to disk: "sda"
    install type: "sys"
    erase & continue? Y


Update Packeged: 

Use vi to edit the repositories - uncomment all the URL lines to enable them all.

vi /etc/apk/repositories


#/media/cdrom/apks
http://dl-6.alpinelinux.org/alpine/v3.3/main
http://dl-6.alpinelinux.org/alpine/v3.3/community
http://dl-6.alpinelinux.org/alpine/edge/main
http://dl-6.alpinelinux.org/alpine/edge/community
http://dl-6.alpinelinux.org/alpine/edge/testing


Update the package list and upgrade what has already been installed:

apk update
apk upgrade



Setup User and Sudo

Create the sudo group, create a non-root user (use whatever username you like, instead of "otheruser"), and add the new user to the sudo group:

addgroup sudo
adduser otheruser
adduser otheruser sudo

Install sudo

apk add sudo



Run "visudo" and remove the "#" comment character from the 2nd line in this group so it looks like:

## Uncomment to allow members of group sudo to execute any command
	
%sudo ALL=(ALL) ALL


Run "visudo" and remove the "#" comment character from the 2nd line in this group so it looks like:

## Uncomment to allow members of group sudo to execute any command
	
%sudo ALL=(ALL) ALL


:end:
#
	
	
	
	
	
	
	
	
	
<a name="top"></a>
