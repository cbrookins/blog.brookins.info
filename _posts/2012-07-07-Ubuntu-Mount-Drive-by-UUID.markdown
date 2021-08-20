---
layout: post
title: Ubuntu Mount Drive by UUID
date: 2012-07-07
---

A small issue users can run into is automatically mounting USB drives to the same location every time. This is usually experienced if you work with a lot of USB externals and thumb drives. Most users mount by the dev id (ex. /dev/sda) and partition number (ex. /dev/sda1). This is fine for internal disks, but what about removable. Depending on when they are plugged in and what else is plugged in, they can go from /dev/sdb to /dev/sdc and so on. This is an easy work around.  

Insert your removable device and locate which dev id and partition number that your device<span style="background-color: white;">currently has.</span>  

Now run  

`sudo ls -l /dev/disk/by-uuid`  



the output should look similar to this  

`lrwxrwxrwx 1 root root 10 Jul 5 19:07 155fb40b-8206-4b92-bc52-c8f507085df1 -> ../../sda1`  
`lrwxrwxrwx 1 root root 10 Jul 5 19:07 2ccacd65-4ac7-4ebf-81bb-a90bfcb4abc0 -> ../../sdb1`  
`lrwxrwxrwx 1 root root 10 Jul 5 19:07 49cfef01-93db-4ae6-9925-4c3ea1281448 -> ../../sdb5`  



You want the number starting after the date/time. In this case I have two physical disks, sda and sdb.  

To mount **/dev/sdb1** I would add the following to **/etc/fstab** by entering  


`sudo nano /etc/fstab`  



and entering  

`UUID=2ccacd65-4ac7-4ebf-81bb-a90bfcb4abc0  /mnt/folder  ext4  defaults  0  01`


You will want to update the &#8216;ext4 option above with whatever file system your drive has. It could be vfat, ntfs, ext3 or anything else that is supported.
