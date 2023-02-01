# System Information Commands


<a name="top"></a>
Topics

  [Windows](#windows)
  [Linux](#linux)
  
  
  
  
  
  
  
#
[Got To Top](#top)
<a name="windows"></a>
# Windows
Find Out the Maximum RAM Your Computer Can Support
Windows

Windows users can determine the maximum RAM capacity in the Command prompt with the command below. It gives the final value in kilobytes which can be converted to gigabytes (divide the value by 1048576 to convert KB to GB).

    wmic memphysical get MaxCapacity, MemoryDevices





  
#
  [Got To Top](#top)
  <a name="linux"></a>
  # Linux
    
# Basic Linux Commands to Check Hardware and System Information


#
1. Printing Machine Hardware Name (uname –m uname –a)
 
    Using the -m switch with the uname command prints the hardware name of our machine. If we want the uname command to print all the information mentioned above, we can use the command with all the switches.


        uname –m
        uname -a

#
2. The lscpu command reports information about the cpu and processing units. It does not have any further options or functionality.

The lscpu command reports information about the cpu and processing units. It does not have any further options or functionality.


          lscpu

  
lshw –List Hardware

  A general purpose utility, that reports detailed and brief information about multiple different hardware units such as cpu, memory, disk, usb controllers, network adapters etc.
  
  
           sudo lshw
           
           sudo lshw –short
  
  
  Generate report in html/xml format

We can also export lshw reports in html, xml and json formats.


            sudo lshw –html > lshw-output.html

            sudo lshw –xml >lshw-output.xml

#
7
             hwinfo

             hwinfo –short

#
4. lspci- List PCI
 

             lspci


#
5. lsscsi-List sci devices

             lsscsi

#
6. lsusb- List usb buses and device details


             lsusb
             
#
7. lsblk- List block devices


             lsblk
             
#
8. df-disk space of file systems


             df -H


#
9. fdisk

             sudo fdisk –l

#
10. mount


             mount | column -t
 
 
 #
11. Dmidecode

The dmidecode command is different from all other commands. It extracts hardware information by reading data from the SMBOIS data structures (also called DMI tables). # display information about the processor/cpu


            sudo dmidecode -t processor # memory/ram information

            sudo dmidecode -t memory # bios details

            sudo dmidecode -t bios


#
12. /proc files

Many of the virtual files in the /proc directory contain information about hardware and configurations. Here are some of them


CPU/Memory information

                cat /proc/cpuinfo

Version

                cat /proc/version

SCSI/Sata devices

                cat /proc/scsi/scsi 

Partitions

                 cat /proc/partitions


#
13. hdparm

The hdparm command gets information about sata devices like hard disks. Each of the command has a slightly different method of extracting information.


                hdparm

#
14. Inxi

                inxi –Fx








#

***Ways to Check Available Memory in Ubuntu 22.04***

    free           command.
    vmstat         command.
    /proc/meminfo  command.
    top            command.
    htop           command.
    cat /proc/meminfo
    lscpu
    
    
    
    top –i

    M – sort task list by memory usage
    P – sort task list by processor usage
    N – sort task list by process ID
    T – sort task list by run time

man top


***Graphical Utility Option:***

To launch Ubuntu’s system monitor, enter the following in a terminal window:

      gnome-system-monitor




ps
ps -eo pcpu,pid,user,args | sort -k 1 -r | head -10 





#
***Linux***

To find the maximum RAM capacity in Linux, you can make use of the command dmidecode, though it is not installed by default in most distros.

1. Install dmidecode:

#ubuntu/debian

    sudo apt install dmidecode
 
#arch

    sudo pacman -S dmidecode
 
#Fedora

    sudo dnf install dmidecode
 
#openSUSE

    sudo zypper in dmidecode

2. Run the command:

    sudo dmidecode -t 16





:end:  
