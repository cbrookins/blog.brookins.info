---
layout: post
title: Apache load balancing with pound and rsync
date: 2014-05-19
---

To set this up I used two Ubuntu 12.04 web servers running Apache and a Raspberry Pi, running IPFire, as my load balancer using [pound](http://apsis.ch/pound).

### Configuring Apache
This document assumes that Apache is already configured on both hosts and serving your web site.  

### Configuring SSH login using private key authentication  
On each host run  

`ssh-keygen`  

At the next prompt hit Enter.  When it prompts for a password, leave them blank.  

Check the contents of '~/.ssh' and you should have **id_rsa** and **id_rsa.pub**  

`ls ~/.ssh`  

Now we need to put the contents of the **id_rsa.pub** file into **authorized_keys** on the remote computer.  One each host you should execute the following command, replacing the ip address with your remote host.  

`ssh-copy-id -i ~/.ssh/id_rsa.pub username@ip_address`  

Enter the users password for that remote host when prompted.  This should add the public key to that remote host in that users **authrozed_keys** file located in **~/.ssh/authorized_keys**.  You should now be able to ssh into the remote host without using a password.  

`ssh username@ip_address`  

**NOTE:**  The permissions on the folder **~/.ssh** should be 700, the **authorized_keys** file should be 600, **id_rsa.pub** should be 644, and **id_rsa** should be 600.  

### Configuring Rsync  
To keep everything in sync I decided to use Rsync.  

I create a bash script on each server to rsync the **/var/www** directory from the remote server.  Then I used cron to run them every fifteen minutes.  This is where the public key authentication comes in handy.  This allows me to run remote commands without having to use a password.  

My bash script was a simple rsync command that I saved to the file **~/sync_web.sh**.  

`rsync -au -e ssh username@remote_host:/var/www/* /var/www/`  

I was able to use the same command on each host by just updating **remote_host**.  

### Setting up cron  
The only thing left is to set the rsync command to run every fifteen minutes.  First, edit crontab  

`crontab -e`  

At the end of the file add  

`*/15 * * * * ~/sync_web.sh`  

### Configure pound  
This section will be a bit different depending on what you use to run pound.  In my case I loaded the software on [my router](http://tech.brookins.info/Raspi_Router_), which is a [Raspberry Pi](http://raspberrypi.org) running [IPFire](http://ipfire.org).

#### IPFire
To set up [pound](http://apsis.ch/pound) in IPFire I used [this wiki article](http://wiki.ipfire.org/en/addons/pound/start) from the official IPFire wiki.

Start by installing the **pound** addon using pakfire.

Now **/etc/sysconfig/pound** with the following contents

    run_pound=1  
    pound_options=""  


Then create **/etc/pound.cfg** with the following contents  


    ListenHTTP  
    Address 0.0.0.0  
    Port    80  
    Service  
        HeadRequire "Host: .*www.server0.com.*"  
        Session  
            Type    IP  
            TTL     3600  
        End  
        BackEnd  
          Address 192.168.0.10  
          Port    80  
        End  
        BackEnd  
            Address 192.168.0.11  
            Port    80  
        End  
      End  
    End  


To finish the configuration off,  enable **External Access** to port 80.


#### Ubuntu
Using Ubuntu you can install [pound](http://apsis.ch/pound) using the following command  

`sudo apt-get install pound`  

Edit **/etc/default/pound**  
Change **startup=0** to **startup=1**  

Configure [pound](http://apsis.ch/pound) the same way as mentioned in the IPFire section above.  The [pound](http://apsis.ch/pound) config can be found at **/etc/pound/pound.cfg**. 

Now you can reboot, or start the [pound](http://apsis.ch/pound) daemon using  

`sudo /etc/init.d/pound start`  

All that is left is to forward port 80 to this host from the router.  