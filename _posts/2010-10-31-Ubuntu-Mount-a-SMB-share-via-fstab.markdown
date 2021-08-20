---
layout: post
title: Ubuntu Mount a SMB share via fstab
date: 2010-10-31
---

I normally like to mount a share after logging in, only when needed. After fighting with mount.cifs after every update that came down, I finally gave in to fstab. This tutorial goes over how I decided to mount my share at boot. There are many options to choose from when mounting a share, these worked best for me at the time of this tutorial.   

Edit /etc/fstab  
`sudo nano /etc/fstab`  
  
Add a line to the bottom of the file, replacing your shares information  
`//server_hostname/share_name /mnt/mount_folder smbfs rw,noperm,file_mode=0664,dir_mode=0775,username=smbusername,password=smbpassword    0    0` 
Save the file   

CTRL+X to exit   
Y to confirm the save   

Now you can reboot or mount everything from fstab with   

`sudo mount -a`  
  
Additional information can be found at <a href="http://samba.org/" target="_blank">samba.org</a> or the <a href="http://www.ubuntu.com/support/community" target="_blank">Ubuntu Community</a>.   

**Update**   
After updating my kernel to 2.6.35-23-generic, the terminal informed me that smbfs would be dropped from future kernel releases. To fix this, we just need to change the entry in /etc/fstab to use cifs.  

`//server_hostname/share_name /mnt/mount_folder cifs rw,noperm,file_mode=0664,dir_mode=0775,username=smbusername,password=smbpassword   0  0`
