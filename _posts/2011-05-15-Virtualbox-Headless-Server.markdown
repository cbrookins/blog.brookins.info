---
layout: post
title: Virtualbox Headless Server
date: 2011-05-15
---

Creating virtual machines is easy on a workstation with a nice gui interface, but what about if you want to do this on a server install that has nothing but a command line. This tutorial goes over installing a headless Ubuntu 10.04 server with <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a> to manage your virtual machines. From start to finish the set up takes about a hour to complete. The following are the steps I took to complete the install, most came from the documentation for <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a>.  

Start off by adding the <a href="http://virtualbox.org/" target="_blank">Virtualbox</a> repository to **/etc/apt/sources.list**  
`echo "deb http://download.virtualbox.org/virtualbox/debian lucid contrib non-free" | sudo tee -a /etc/apt/sources.list`  


Add the <a href="http://virtualbox.org/" target="_blank">Virtualbox</a> repository key  
`wget -q http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc -- | sudo apt-key add oracle_vbox.asc`  


Update Ubuntu  
`sudo apt-get update && sudo apt-get -y upgrade`  


Now we need to install <a href="http://virtualbox.org/" target="_blank">Virtualbox</a>, <a href="http://httpd.apache.org/" target="_blank">Apache2</a>, <a href="http://php.org/" target="_blank">PHP5</a>, Unzip and <a href="http://openssh.com/" target="_blank">OpenSSH </a>server.  
`sudo apt-get -y install virtualbox-4.0 apache2 php5 libapache2-mod-php5 unzip openssh-server`  


<a href="http://httpd.apache.org/" target="_blank">**Apache2**</a> is the web server that will run phpVirtualBox.  
<a href="http://php.org/" target="_blank">**PHP5**</a> is the programming language that phpVirtualBox is written in.  
**Unzip** is to unzip phpVirtualBox after it has downloaded.  
<a href="http://www.openssh.com/" target="_blank">**OpenSSH**</a> server will allow you to manage the server from another workstation. Once this is installed the actual server does not need a monitor, or keyboard.  

Create /etc/default/virtualbox  
`sudo nano /etc/default/virtualbox`  


Add this one line to the file  
`VBOXWEB_USER=`  

Press **CTRL+O** to write the file to disk  
Press **Enter** to confirm  

Add local user to vboxusers group  
`sudo adduser vboxusers`  


Now we are ready to download <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a>.  
`wget http://phpvirtualbox.googlecode.com/files/phpvirtualbox-4.0-5.zip`  


Unzip <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a>  
`unzip phpvirtualbox-4.0-5.zip`  


Create the <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a> directory  
`sudo mkdir /var/www/phpvirtualbox`  


Copy the <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a> files to the folder /var/www/phpvirtualbox. This directory is the default set in <a href="http://httpd.apache.org/" target="_blank">Apache2</a>. You can change this in the <a href="http://httpd.apache.org/" target="_blank">Apache2</a> configuration file if you need to, but that is outside of the scope of this. Use the <a href="http://httpd.apache.org/" target="_blank">Apache</a> documentation for help - <a href="http://httpd.apache.org/" target="_blank">http://httpd.apache.org/</a>.  
`sudo cp -R phpvirtualbox-4.0-5/* /var/www/phpvirtualbox`  


Prepare the <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">phpvirtualbox</a> config file  
`sudo cp /var/www/phpvirtualbox/config.php-example /var/www/phpvirtualbox/config.php`  


Edit config.php  
`sudo nano /var/www/phpvirtualbox/config.php`  


Update the $username and $password variable to match your local user  
`var $username = ''`  
`var $password = ''`  


You can now start the <a href="http://virtualbox.org/" target="_blank">Virtualbox</a> web service  
`sudo /ect/init.d/vboxweb-service start`  


Download <a href="http://virtualbox.org/" target="_blank">VirtualBox</a> Extension Pack. This package installs what you need to do remote desktop into the virtual machines.  
`wget http://download.virtualbox.org/virtualbox/4.0.6/Oracle_VM_VirtualBox_Extension_Pack-4.0.6-71344.vbox-extpack`  


Install <a href="http://virtualbox.org/" target="_blank">VirtualBox</a> Extension Pack  
`sudo VBoxManage extpack install Oracle_VM_VirtualBox_Extension_Pack-4.0.6-71344.vbox-extpack`  


Restart the server  
`sudo shutdown -r now`  


That will create a functional headless server running Virtualbox and phpVirtualbox. Once the server has finished restarting navigate to  

**http://server_ip_address/phpvirtualbox**  

Here you will need to use the username admin with the password admin to access the web interface. Once you are logged in you can change the admin password using File &gt; Change Password or create new users under File &gt; Preferences &gt; Users.  

In the following screenshots everything you see is in the browser window, except the Terminal Server client. My servers IP address is **192.168.1.110**. You will notice that when I RDP to a virtual machine hosted on this server, I use the servers IP address and add a port number. The port number controls which virtual machine I RDP into.  

<a href="http://3.bp.blogspot.com/-JTWQ0Jz3h4Y/T1k7Fxiyy0I/AAAAAAAABR4/vm6gl4Tboo4/s1600/phpvbox_1.png" target="_blank"><img alt="image" height="118" src="http://3.bp.blogspot.com/-JTWQ0Jz3h4Y/T1k7Fxiyy0I/AAAAAAAABR4/vm6gl4Tboo4/s200/phpvbox_1.png" width="200"/></a> <a href="http://3.bp.blogspot.com/-qqN88-ufIt4/T1k7GO7p-fI/AAAAAAAABSA/vZ7gb10PsWQ/s1600/phpvbox_10.png" target="_blank"><img alt="image" height="111" src="http://3.bp.blogspot.com/-qqN88-ufIt4/T1k7GO7p-fI/AAAAAAAABSA/vZ7gb10PsWQ/s200/phpvbox_10.png" width="200"/></a> <a href="http://3.bp.blogspot.com/-Tgpb5A6zTUI/T1k7G1qKAwI/AAAAAAAABSI/drTzAJdbLGw/s1600/phpvbox_11.png" target="_blank"><img alt="image" height="158" src="http://3.bp.blogspot.com/-Tgpb5A6zTUI/T1k7G1qKAwI/AAAAAAAABSI/drTzAJdbLGw/s200/phpvbox_11.png" width="200"/></a> <a href="http://1.bp.blogspot.com/-JROGEpXEupw/T1k7HCQT64I/AAAAAAAABSQ/RVvYt_JwtAs/s1600/phpvbox_12.png" target="_blank"><img alt="image" height="111" src="http://1.bp.blogspot.com/-JROGEpXEupw/T1k7HCQT64I/AAAAAAAABSQ/RVvYt_JwtAs/s200/phpvbox_12.png" width="200"/></a> <a href="http://4.bp.blogspot.com/-9BPT_wHpbtc/T1k7HgWRa0I/AAAAAAAABSY/b31y8vO39sg/s1600/phpvbox_13.png" target="_blank"><img alt="image" height="111" src="http://4.bp.blogspot.com/-9BPT_wHpbtc/T1k7HgWRa0I/AAAAAAAABSY/b31y8vO39sg/s200/phpvbox_13.png" width="200"/></a> <a href="http://3.bp.blogspot.com/--E02caxAICs/T1k7IVTsjwI/AAAAAAAABSo/isRn3GzC98s/s1600/phpvbox_2.png" target="_blank"><img alt="image" height="129" src="http://3.bp.blogspot.com/--E02caxAICs/T1k7IVTsjwI/AAAAAAAABSo/isRn3GzC98s/s200/phpvbox_2.png" width="200"/></a> <a href="http://3.bp.blogspot.com/-ZE62XX87bXM/T1k7ImSl2WI/AAAAAAAABSs/dkSNcMK6BBU/s1600/phpvbox_3.png" target="_blank"><img alt="image" height="146" src="http://3.bp.blogspot.com/-ZE62XX87bXM/T1k7ImSl2WI/AAAAAAAABSs/dkSNcMK6BBU/s200/phpvbox_3.png" width="200"/></a> <a href="http://3.bp.blogspot.com/-Gadz3i6f_G4/T1k7JPNKxNI/AAAAAAAABS0/1XQlMENClL0/s1600/phpvbox_4.png" target="_blank"><img alt="image" height="108" src="http://3.bp.blogspot.com/-Gadz3i6f_G4/T1k7JPNKxNI/AAAAAAAABS0/1XQlMENClL0/s200/phpvbox_4.png" width="200"/></a> <a href="http://4.bp.blogspot.com/-d_9_H2tCGeE/T1k7JrVtVCI/AAAAAAAABS8/hq8JFwcxN44/s1600/phpvbox_5.png" target="_blank"><img alt="image" height="146" src="http://4.bp.blogspot.com/-d_9_H2tCGeE/T1k7JrVtVCI/AAAAAAAABS8/hq8JFwcxN44/s200/phpvbox_5.png" width="200"/></a> <a href="http://1.bp.blogspot.com/-sOYDnt2gJhA/T1k7KGXYAvI/AAAAAAAABTI/HUdGJ0ZVyn4/s1600/phpvbox_6.png" target="_blank"><img alt="image" height="146" src="http://1.bp.blogspot.com/-sOYDnt2gJhA/T1k7KGXYAvI/AAAAAAAABTI/HUdGJ0ZVyn4/s200/phpvbox_6.png" width="200"/></a> <a href="http://2.bp.blogspot.com/-N2wul8e0KBo/T1k7KkbPBXI/AAAAAAAABTQ/qrPDzUgVTLE/s1600/phpvbox_7.png" target="_blank"><img alt="image" height="146" src="http://2.bp.blogspot.com/-N2wul8e0KBo/T1k7KkbPBXI/AAAAAAAABTQ/qrPDzUgVTLE/s200/phpvbox_7.png" width="200"/></a> <a href="http://4.bp.blogspot.com/-7oKjxIRPjiQ/T1k7LFzZIGI/AAAAAAAABTY/ShFBvZavGW8/s1600/phpvbox_8.png" target="_blank"><img alt="image" height="146" src="http://4.bp.blogspot.com/-7oKjxIRPjiQ/T1k7LFzZIGI/AAAAAAAABTY/ShFBvZavGW8/s200/phpvbox_8.png" width="200"/></a> <a href="http://2.bp.blogspot.com/-e1hwr9H1PYE/T1k7NOIfm7I/AAAAAAAABTg/N-UboG0NfwE/s1600/phpvbox_9.png" target="_blank"><img alt="image" height="146" src="http://2.bp.blogspot.com/-e1hwr9H1PYE/T1k7NOIfm7I/AAAAAAAABTg/N-UboG0NfwE/s200/phpvbox_9.png" width="200"/></a><a href="http://2.bp.blogspot.com/-aCVjbZNNkc0/T1k7H0IQ4HI/AAAAAAAABSg/toPtrXTxbfE/s1600/phpvbox_14.png" target="_blank"><img alt="image" height="200" src="http://2.bp.blogspot.com/-aCVjbZNNkc0/T1k7H0IQ4HI/AAAAAAAABSg/toPtrXTxbfE/s200/phpvbox_14.png" width="149"/></a> 

Just for reference, the Guest Additions iso is, by default, located at **/usr/share/virtualbox/VBoxGuestAdditions.iso**.