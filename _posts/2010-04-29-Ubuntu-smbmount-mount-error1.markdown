---
layout: post
title: Ubuntu smbmount mount error1
date: 2010-04-29
---

I recently ran into a problem mounting a remote share to my newly installed Ubuntu 10.04 installation. I had never had a problem before so I knew my mount script was correct. I found an easy fix to allow a regular user to mount a remote share.  
  
I had already prepared a folder to mount to, made myself the owner of that folder and I had smbfs installed. When I try to mount I received the error "mount error(1): operation not permitted". I could go to the network browser and mount it that way, but my script would only work as root. To fix this, you just need to enable the "sticky" bit on smbmount/mount.cifs. To do this, run the following command  
`sudo chmod +s which smbmount`  
  
If you would also like to be able to unmount, use this command also  
`sudo chmod +s which smbumount`  
  
After that, you should be able to mount using  
`smbmount //servername/sharefolder /mnt/point -o username=username,password=password`  
  
**Update:** When I tried this on Ubuntu 10.04.1, it no longer worked. Running the command below fixed the problem.  
`sudo chmod +s which mount.cifs`  
  
**Update:** These do not work under Ubuntu 10.10. I am really tired of fighting with this.  I have switched over to using fstab to mount the share.  Check out how I do it <a href="http://cbrookins.blogspot.com/2010/10/ubuntu-mount-smb-share-via-fstab.html" target="_blank">here</a>.
