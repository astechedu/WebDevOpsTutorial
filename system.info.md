# System Information Commands


<a name="top"></a>
Topics

  [Windows](#windows)
  [Linux](#linux)
  
  
  
  
  
  
# Windows
  
  
  
  [Got To Top](#top)
  <a name=""></a>
  # Linux
    
# Basic Linux Commands to Check Hardware and System Information



1. Printing Machine Hardware Name (uname –m uname –a)
 
    Using the -m switch with the uname command prints the hardware name of our machine. If we want the uname command to print all the information mentioned above, we can use the command with all the switches.


        uname –m
        uname -a


2. The lscpu command reports information about the cpu and processing units. It does not have any further options or functionality.

The lscpu command reports information about the cpu and processing units. It does not have any further options or functionality.


          lscpu

  
lshw –List Hardware

  A general purpose utility, that reports detailed and brief information about multiple different hardware units such as cpu, memory, disk, usb controllers, network adapters etc.
  
  
           sudo lshw $ sudo lshw –short
  
  
  Generate report in html/xml format

We can also export lshw reports in html, xml and json formats.


            sudo lshw –html > lshw-output.html

            sudo lshw –xml >lshw-output.xml


2. hwinfo- Hardware Information

             hwinfo

             hwinfo –short


3. lspci- List PCI
 

             lspci



4. lsscsi-List sci devices

             lsscsi


5. lsusb- List usb buses and device details


             lsusb
             

6. lsblk- List block devices


             lsblk
             

7. df-disk space of file systems


             df -H



8. fdisk

             sudo fdisk –l


9. mount


             mount | column -t
 
 
 
10. Dmidecode

The dmidecode command is different from all other commands. It extracts hardware information by reading data from the SMBOIS data structures (also called DMI tables). # display information about the processor/cpu


            sudo dmidecode -t processor # memory/ram information

            sudo dmidecode -t memory # bios details

            sudo dmidecode -t bios


11. /proc files

Many of the virtual files in the /proc directory contain information about hardware and configurations. Here are some of them


CPU/Memory information

                cat /proc/cpuinfo

Version

                cat /proc/version

SCSI/Sata devices

                cat /proc/scsi/scsi 

Partitions

                 cat /proc/partitions



12. hdparm

The hdparm command gets information about sata devices like hard disks. Each of the command has a slightly different method of extracting information.


                hdparm


13. Inxi

                inxi –Fx


:end:  
