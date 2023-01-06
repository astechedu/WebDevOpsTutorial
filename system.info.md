# System Information Commands


<a name="top"></a>
Topics

  [Windows](#windows)
  [Linux](#linux)
  
  
  
  
  
  
  # Windows
  
  
  
  [Got To Top](#top)
  <a name=""></a>
  # Linux
  
  
Basic Linux Commands to Check Hardware and System Information

1. Printing Machine Hardware Name (uname –m uname –a)

    uname –m
    uname -a


2. The lscpu command reports information about the cpu and processing units. It does not have any further options or functionality.
 
    lscpu
  
  
  lshw –List Hardware
  
  sudo lshw $ sudo lshw –short
  
  
  Generate report in html/xml format

We can also export lshw reports in html, xml and json formats.

$ sudo lshw –html > lshw-output.html

$ sudo lshw –xml >lshw-output.xml


2. hwinfo- Hardware Information

$ hwinfo

$ hwinfo –short


3. lspci- List PCI

$ lspci



4. lsscsi-List sci devices

$ lsscsi


5. lsusb- List usb buses and device details


$ lsusb

6. lsblk- List block devices

lsblk

7. df-disk space of file systems

df -H



8. fdisk

$ sudo fdisk –l


9. mount


 mount | column -t
 
 
 













  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
  
