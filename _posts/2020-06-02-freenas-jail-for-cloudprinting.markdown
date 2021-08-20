---
layout: post
title: FreeNAS jail for cloud printing
date: 2020-06-02
---

## Use case  
I wanted to set up my old HP PhotoSmart inkjet printer with Google Cloud Print, 
but I did not want to have the client on one of my machines that I use day to day. I ended up deciding to use a jail on my FreeNAS box.  
  
## The Goods  
Starting off with a fresh FreeNAS-11.3-U3.1 jail.  
  
### Install some packages  
``pkg install cups cloudprint hplip nano``

### Prep cupsd  
``touch /etc/devfs.rules``  

edit **/etc/devfs.rules** and add  
```
[system=10]
add path 'unlpt*' mode 0660 group cups
add path 'ulpt*' mode 0660 group cups
add path 'lpt*' mode 0660 group cups
```  

edit **/etc/rc.conf** and add  
```
cupsd_enable="YES"
devfs_system_ruleset="system"
```  
[comment]: <> (edit **/usr/local/etc/rc.d/cloudprint** and modify)
[comment]: <> (``: ${cloudprint_enable="NO"}`` to read ``: ${cloudprint_enable="YES"}``)

Run the following commands  
``/etc/rc.d/devfs restart``  
``/usr/local/etc/rc.d/cupsd restart``  
``cupsctl --remote-admin --share-printers``  

You should now be able to get to the cups web management using **http://server_name_or_ip:631**  

Login using FreeNAS **root** login. You could also set up a new user and add it to the **cups** group.  

Add your printer under the **Administration** tab  

Now run the following command  
``service cloudprint start``  

Use a browser to go to the provided link and registered the printer with your Google account. Once registration is complete you should be able to send jobs to your printer.    

Reboot and verify that **cloudprint** is running.  



#### Sources  
[FreeBSD Official](https://www.freebsd.org/doc/en/articles/cups/)  
[Cups Official](https://www.cups.org/doc/man-cupsctl.html)  
[Cloudprint GitHub](https://github.com/armooo/cloudprint)
