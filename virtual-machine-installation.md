$$\color{blue}{Virtual \ Machine \ Installations}$$


[Home](all-file-links.md)


Topics:

[VirtualBox Installation On Ubuntu 20.04](#virtualbox-install-on-ubuntu20.04)





[Top](#top)
<a name="virtualbox-install-on-ubuntu20.04"></a>
# VirtualBox Installation On Ubuntu 20.04


***Installing VirtualBox on Ubuntu 20.04 via APT***


The base repositories for Ubuntu 20.04 include VirtualBox, but it doesn’t come installed by default. The easiest way to install VirtualBox on Ubuntu is to use the APT package manager. This method works whether you’re using Ubuntu Desktop or Server.


To install VirtualBox from the Ubuntu repositories using APT:

1. Run the apt update command below to update the list of available packages.

     apt update -y

<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-61.png" width=40%>



2. Next, run the below apt install command to install VirtualBox and the extended pack.

The extended pack is a set of additional features for VirtualBox that lets you use certain features, such as USB 2.0 and 3.0 support, Remote Desktop Protocol (RDP), etc.

      apt install virtualbox virtualbox-ext-pack -y


<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-62.png" width=40%>



3. Select OK, and press Enter after reading the VirtualBox Extension Pack Personal Use and Evaluation License (PUEL) terms.


<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-63-1536x683.png" width=40%>



4. Now, select Yes, and press Enter to accept the Oracle Binary Code License Agreement for the VirtualBox Extension Pack.

<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-64.png" width=40%>



The installer will download and install all the necessary files, as shown below. Wait for the process to complete. That’s it! You’ve successfully installed VirtualBox on your machine using APT.

<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-65-1536x242.png" width=40%>



5. Finally, run the following command to start using VirtualBox or open it from the Applications menu.


      virtualbox
      
      
      
The main VirtualBox Manager window appears, as shown below, where you can manage your VMs.      
      
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-66.png" width=40%>

    
    
#      
***Installing VirtualBox from Oracle’s Official Repository***     
      
You’ve learned to install VirtualBox using the APT package manager, a quick method. But that method has one major downside; you will not get the latest version of VirtualBox.      
      
      
If you prefer to get the latest version of VirtualBox, you need to install it from Oracle’s official repository. Oracle releases new versions of VirtualBox frequently. Note that this method is a bit more complex than the previous one.

To install VirtualBox from Oracle’s official repository, you first need to add the Oracle repository key to your system:


1. Run the wget command below to download and add the Oracle repository key to your keyring. This key ensures that the packages you install using this repository are valid and come from a trusted source.      
      
      wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -
      

      
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-67-1536x157.png" width=40%>

      
2. Next, run the following add-apt-repository command to add the Oracle repository to your system. This repository contains the latest versions of VirtualBox for Ubuntu.


      add-apt-repository "deb [arch=amd64] http://download.virtualbox.org/virtualbox/debian $(lsb_release -cs) contrib"
      
      
       
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-68-1536x508.png" width=40%>
     
      
3. After adding the repository, run the below apt update command to update the APT cache and apply the new changes.      

      apt update -y      
      
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-69.png" width=40%>
     
     
4. Run the apt cache command to check which version of VirtualBox is available in the official repositories.

      apt-cache policy virtualbox          
          
 Pick the latest version of VirtualBox from the list to install.
 
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-70.png" width=40%>
     
 
5. Now, run the apt install command to install the latest VirtualBox version you picked from step four.

      apt install virtualbox-6.1 -y 
 
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-71.png" width=40%>
      
 
 
Alternatively, you can copy and paste the apt install virtualbox- command to your terminal and press Tab to autocomplete the version number.

All the versions currently available will be displayed, as shown below. Choose the newest one to install. This behavior works for any supported Ubuntu release and VirtualBox version combination. 
 
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-72.png" width=40%>
       
 
6. Next, run the following command to download the VirtualBox Extension Pack. Ensure the version number of the extension pack matches the version of VirtualBox you just installed (6.1). 
 
 
      wget https://download.virtualbox.org/virtualbox/6.1.26/Oracle_VM_VirtualBox_Extension_Pack-6.1.26.vbox-extpack 
 
 
  
<img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-73.png" width=40%>
   
 
 7. Lastly, run the VBoxManage command below to install the VirtualBox Extension Pack.

      VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-6.1.26.vbox-extpack
 
 Type y and press Enter when prompted to agree to the terms, as shown below.
 
 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-74.png" width=40%>
   
          
          
#          
***Install VirtualBox using a Deb Package***

If you’re not a fan of adding third-party repositories to your system, you can install VirtualBox using a deb package. You can download the deb package from Oracle and install it manually on your system.

To install VirtualBox from a .deb package:



1. Open your favorite web browser, head to the VirtualBox Linux downloads page, and look for your Linux distribution. This tutorial goes for the VirtualBox 6.1.34 for Ubuntu 20.04.          
          
Right click on the hyperlink, as shown below, and choose Copy link address to copy the download link.

 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-75.png" width=40%>
   

2. Now run the wget command to download the .deb package. Replace the link below with the download link you copied in step one.

The -P option is used to specify the destination directory, which in this case is the Downloads folder.          
          
      wget https://download.virtualbox.org/virtualbox/6.1.34/virtualbox-6.1_6.1.34-150636.1~Ubuntu~eoan_amd64.deb -P Downloads
      
      
 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-76-1536x625.png" width=40%>
         
      
 3. Now, run the following commands to switch to the Downloads directory and install VirtualBox.

cd Downloads

      dpkg -i Downloads/virtualbox-6.1_6.1.34-150636.1~Ubuntu~eoan_amd64.deb     
     
      
  <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-77-1536x212.png" width=40%>
         
           
#      
 ***Creating Your First VM***

You’ve successfully installed VirtualBox on your machine and are ready to create your first VM. This tutorial uses a Windows 10 image to create a VM, but you can choose any you prefer.

To create your first VM:

1. Launch VirtualBox if it’s not already open.

2. Click the New button on the toolbar to create a new VM.    
      
   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-78.png" width=40%>
              
      
3. Configure the name and operating system (OS) for your VM with the following:

    Name – Provide a name for your VM. This tutorial’s choice is W10.

    Machine Folder – Choose the folder where you want your VM to reside. 


    Type – Select the type of OS for your VM. This tutorial’s choice is Windows 10 (32-bit).

    Click Next to continue.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-79.png" width=40%>
       

4. Now, specify how much memory (RAM in MB) you want to allocate for your VM, and click Next.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-80.png" width=40%>
       

5. Select the Create a virtual hard disk now option on the next screen, and click Create.

This option lets you create a virtual hard disk (a file) that stores all the data for your VM, including the operating system, applications, and files.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-81.png" width=40%>
       

6. Next, choose the VDI (VirtualBox Disk Image) option, which is a good choice for most users, and click Next.

But if you’re running VirtualBox on an enterprise environment, choose one of the other two options instead.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-82.png" width=40%>
      

7. On the next screen, choose the storage type for your virtual hard disk. But for this tutorial, select the default option (Dynamically allocated) and click Next.

Why use dynamic allocation? This option is more efficient with storage space because it only allocates the amount of disk space the VM uses.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-83.png" width=40%>
      

8. Choose a name for the virtual hard disk, allocate the storage space for your VM, and click Create. You can choose the storage size you prefer, but this tutorial’s choice is 20 GB.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-84.png" width=40%>
      


Once the VM is created, you’ll see the VM listed in the left pane of the VirtualBox window.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-85.png" width=40%>
      

Attaching a Bootable Media

You’ve just created your first VM on VirtualBox. But right now, even if you start the VM, it won’t do anything since you haven’t attached any bootable media to the VM.


To attach a bootable media to your VM:

1. Click on your VM in the left pane, and click Settings from the toolbar to access your VM’s settings.


   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-86.png" width=40%>
      
      
2. On the Settings window, click Storage in the left pane —> Empty drive under Storage Devices —> the disc icon under Attributes.

A context menu opens where you can choose how to attach a bootable media for the VM (step three).      
        
      
  <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-87.png" width=40%>
      
      
 3. Select Choose disk file from the dropdown menu to look up your bootable media (ISO).     
      
      
   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-88.png" width=40%>
           
4. Now, locate and select your ISO image file.


   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-89.png" width=40%>
          

5. Click OK to close the Settings window.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-90.png" width=40%>
        
6. Lastly, click Start at the toolbar to start your new VM.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-91.png" width=40%>
        

You’ll see a new window open with your VM booting up. At this point, you can install your OS (Windows 10) as you usually would on a local machine.

After installing the OS, you can boot up your VM and use it just like any other computer.

   <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-92.png" width=40%>
      


Increasing VM’s Video Memory (VRAM) to Improve Performance

Did you notice slowness on your VM after setting up its OS? By default, the VRAM allocated to a VM is only 128 MB, which is also the max VRAM you can allocate, as shown below.

 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-93.png" width=40%>
      


This amount of VRAM is fine if you have only one or two windows open. But, if you try to do anything graphics-intensive, like testing your video games on different OS, you’ll need more VRAM.

To increase the video memory for your VM:

1. Click on the Machine menu —> ACPI Shutdown, as shown below, or press Host+H keys to shutdown your VM. The Host key is the right Ctrl key on your keyboard.

 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-94.png" width=40%>
      

2. Next, run the below command to increase (modifyvm) your VM’s VRAM to 256. This command doesn’t provide output but sets your VM’s max VRAM to 256. Be sure to replace W10 with your VM’s name.

      VBoxManage modifyvm "W10" --vram 256

3. Start your VM again, and you’ll notice the difference in performance.

4. Finally, open VM’s settings, click on Display in the left pane and see the Video Memory is set to 256 MB, as shown below. This output indicates that your Windows 10 VM’s video adapter now uses 256 MB of video memory.


 <img src="https://adamtheautomator.com/wp-content/uploads/2022/08/image-95.png" width=40%>
    


:end:










