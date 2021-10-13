---
layout: post
title: Linux deduplication with LessFS
date: 2011-08-27
tags: ['linux']
---

De-duplication is a type of compression that looks for redundant data and instead of duplicating data it will create a reference that points to the original source. For example, if you have two images that are exactly the same but one is in your Pictures folder and you copy it to your desktop. Instead of having an exact copy of the image, a "link" is created that points back to the original. If the original image in your Pictures folder is deleted, de-duplication will determine that this resource is still in use and the "link" will remain intact.  

Deduplication uses hashes to compare data. Even if filenames and extensions are different, deduplication will see these files as the same. One drawback to this could be that if two completely different files generate the same hash. This is considered a "collision" and even though there is a very small chance this could occur, it is possible.  

In this tutorial I will set up LessFS on a Ubuntu 10.04 LTS server to handle my deduplication. This is pretty straight forward and very easy to set up.  

We will start with a fresh install of Ubuntu 10.04 LTS. We will not need anything to be installed during the OS install, unless you want an SSH server to finish the install remotely.  

Once you boot into the server the first time we will do our updates and install the needed packages.  
`sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y install build-essential libmhash-dev libtokyocabinet-dev pkg-config libfuse-dev`  


Now download LessFS from sourceforge  
`wget http://sourceforge.net/projects/lessfs/files/lessfs/lessfs-1.5.0/lessfs-1.5.0.tar.gz`  


untar the files using  
`tar -xzvf lessfs-1.5.0.tar.gz`  


Change to the new directory  
`cd lessfs-1.5.0`  


Configure the LessFS package  
`./configure`  


Build LessFS  
`make`  


Install LessFS  
`make install`  


Copy the example startup script  
`sudo cp etc/lessfs-init_example /etc/init.d/lessfs.sh`  


Open the new startup script using your favorite text editor  
`sudo nano /etc/init.d/lessfs.sh`  


Now the hardest part of this tutorial, edit the file as follows  

EDIT line 10 **. /etc/rc.d/init.d/functions** to **#. /etc/rc.d/init.d/functions**  
EDIT line 15 **. /etc/sysconfig/network** to **#. /etc/sysconfig/network**  
EDIT line 18 **[ ${NETWORKING} = "no" ] && exit 0** to **#[ ${NETWORKING} = "no" ] && exit 0**  
ADD line 19 **[ -f /var/run/network/ifstate ] && [ $(cat /var/run/network/ifstate | wc -l ) -eq 0 ] && exit 0**  
EDIT line 22 **MKLESSFS=/usr/local/sbin/mklessfs**  
EDIT line 23 **MOUNTPOINT=/fuse to MOUNTPOINT=/path/to/mount**  
EDIT line 25 **LESSFS=/usr/local/bin/lessfs**  
EDIT line 39 **touch /var/lock/subsys/lessfs to touch /var/lock/lessfs**  
EDIT line 49 **rm -f /var/lock/subsys/lessfs to rm -f /var/lock/lessfs**  

Make the startup script executable  
`sudo chmod +x /etc/init.d/lessfs.sh`  


Set this script to run when the system boots  
`sudo update-rc.d lessfs.sh defaults`  


Copy the LessFS configuration file  
`sudo cp etc/lessfs.cfg /etc/`  


Edit /etc/lessfs.cfg, if you would like to change the data directory (default: /data)  
`sudo nano /etc/lessfs.cfg`  


Make the LessFS directories for storing the file information and metadata  
`sudo mkdir /data_directory && sudo mkdir /data_directory/dta && sudo mkdir /data_directory/mta`  


Create the LessFS files  
`sudo mklessfs -c /etc/lessfs.cfg`  


Now you can reboot. This will give us an opportunity to test out startup script. Once the server has rebooted and you are logged in, run the command  
`df -t fuse.lessfs`  


If this command displays a filesystem, then you are ready to go.  

**NOTE:** If you decide not the use a startup script, you can mount the filesystem manually using  
`sudo lessfs /etc/lessfs.cfg /path/to/mount`  


Now after all that we can test it out. One of the best examples I have found for testing LessFS out is to use dd and /dev/zero. For this example, my data directory is /mnt.  

Check your LessFS file system usage using  
`df -t fuse.lessfs`  


Using the command below will create a 1GB file in /mnt.  
`sudo dd if=/dev/zero of=/mnt/test.dump bs=1M count=1000`  


Check you LessFS file system usage again  
`df -t fuse.lessfs`  


Notice that usage is not a 1GB difference. Using dd with /dev/zero created a 1GB file using nothing but zeros. LessFS recognized that the file was made up of a duplication of information and so it was able to highly compress the file.  

Try it again, except this time create a file in the root of the drive.  
`sudo dd if=/dev/zero of=/test.dump bs=1M count=1000`  


Check your space available  
`df -t fuse.lessfs`  


Delete the test.dump file  
`sudo rm test.dump`  


Check your space again  
`df -t fuse.lessfs`  


Now create the same file, but under your data directory  
`sudo dd if=/dev/zero of=/mnt/test.dump bs=1M count=1000`  


Check your usage  
`df -t fuse.lessfs`  


You should see a huge difference in the space used.  

That is all. It seems like a lot when reading this, but the longest part of this whole thing is installing the server OS and updating. Installing and configuring LessFS is a breeze. According to the <a href="http://lessfs.com" target="blank">official site</a> LessFS also works fine with Samba.  

If you have any feedback or ways to make this better, leave them in comments.
