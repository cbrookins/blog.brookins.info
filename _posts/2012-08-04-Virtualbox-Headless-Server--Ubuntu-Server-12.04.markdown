---
layout: post
title: Virtualbox Headless Server  Ubuntu Server 12.04
date: 2012-08-04
---

*Same post as before, updated for Ubuntu Server 12.04*

Creating virtual machines is easy on a workstation with a nice gui interface, but what about if you want to do this on a server install that has nothing but a command line. This tutorial goes over installing a headless Ubuntu 12.04 server with phpvirtualbox to manage your virtual machines. From start to finish the set up takes about a hour to complete. The following are the steps I took to complete the install, most came from the documentation for phpvirtualbox.  

Start off by adding the Virtualbox repository to /etc/apt/sources.list  
`echo "deb http://download.virtualbox.org/virtualbox/debian precise contrib non-free" | sudo tee -a /etc/apt/sources.list`  


Add the Virtualbox repository key  
`wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -- | sudo apt-key add oracle_vbox.asc`  


Update Ubuntu  
`sudo apt-get update && sudo apt-get -y upgrade`  


Now we need to install Virtualbox, Apache2, PHP5, Unzip and OpenSSH server.  
`sudo apt-get -y install virtualbox-4.1 apache2 php5 libapache2-mod-php5 unzip openssh-server`  


Apache2 is the web server that will run phpVirtualBox.  
PHP5 is the programming language that phpVirtualBox is written in.  
Unzip is to unzip phpVirtualBox after it has downloaded.  
OpenSSH server will allow you to manage the server from another workstation. Once this is installed the actual server does not need a monitor, or keyboard.  

Create /etc/default/virtualbox  
`sudo nano /etc/default/virtualbox`  


Add this one line to the file  
`VBOXWEB_USER=[USERNAME]`  

Press CTRL+O to write the file to disk  
Press Enter to confirm  

Add local user to vboxusers group  
`sudo adduser [USERNAME] vboxusers`  


Now we are ready to download phpvirtualbox.  
`wget https://phpvirtualbox.googlecode.com/files/phpvirtualbox-4.1-7.zip`  


Unzip phpvirtualbox  
`unzip phpvirtualbox-4.1-7.zip`  


Create the phpvirtualbox directory  
`sudo mkdir /var/www/phpvirtualbox`  


Copy the phpvirtualbox files to the folder /var/www/phpvirtualbox. This directory is the default set in Apache2. You can change this in the Apache2 configuration file if you need to, but that is outside of the scope of this. Use the Apache documentation for help - <a href="http://httpd.apache.org/." target="_blank">http://httpd.apache.org/.</a>  
`sudo cp -R phpvirtualbox-4.1-7/* /var/www/phpvirtualbox`  


Prepare the phpvirtualbox config file  
`sudo cp /var/www/phpvirtualbox/config.php-example /var/www/phpvirtualbox/config.php`  


Edit config.php  
`sudo nano /var/www/phpvirtualbox/config.php`  


Update the $username and $password variable to match your local user  
`var $username = '<username>'`  
`var $password = '<password>'</password></username>`  


You can now start the Virtualbox web service  
`sudo /etc/init.d/vboxweb-service start`  


Download VirtualBox Extension Pack. This package installs what you need to do remote desktop into the virtual machines.  
`wget http://download.virtualbox.org/virtualbox/4.1.18/Oracle_VM_VirtualBox_Extension_Pack-4.1.18-78361.vbox-extpack`  


Install VirtualBox Extension Pack  
`sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-4.1.18-78361.vbox-extpack`  


Restart the server  
`sudo shutdown -r now`  


That will create a functional headless server running Virtualbox and phpVirtualbox. Once the server has finished restarting navigate to  

**http://[HOSTNAME-or-IP_ADDRESS]/phpvirtualbox**  

Here you will need to use the username admin with the password admin to access the web interface.  Once you are logged in you can change the admin password using File &gt; Change Password or  create new users under File >Preferences > Users.  

In the following screenshots everything you see is in the browser window, except the Terminal Server client. My servers IP address is **192.168.1.110**. You will notice that when I RDP to a virtual machine hosted on this server, I use the servers IP address and add a port number. The port number controls which virtual machine I RDP into.",
