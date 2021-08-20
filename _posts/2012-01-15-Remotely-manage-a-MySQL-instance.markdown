---
layout: post
title: Remotely manage a MySQL instance
date: 2012-01-15
---

I have always liked to manage systems from my own workstation. I have never liked having to log into a server to manage something that I could just as easily do using management software installed on my own workstation.  

I set up a MySQL server using Ubuntu Server 10.04, and by default it only allows connections from the local machine. I was unable to connect using the MySQL Workbench. The following steps will allow remote connections to a MySQL instance running on Ubuntu Server 10.04<span style="color: red;">*</span>.  

<span style="color: red;">*</span>Different Linux distributions come with different setups. Remote connections may be allowed by default on some distributions. These steps should work on other distributions that do not allow remote connections by default.  

MySQL stores its configuration file in the my.cnf file. This is the only file that needs to be changed to allow connections to a MySQL instance.  

Edit /etc/mysql/my.cnf  
`sudo nano /etc/mysql/my.cnf`  


Edit the line "bind-address = 127.0.0.1" to include your static IP  
`bind-address =`  


Save the changes  
ctrl+x to exit  
Y to confirm the changes  

Restart MySQL  
`sudo /etc/init.d/mysql restart`  


Once the MySQL instance has restarted, remote connections should be allowed to the static address of the server.",
