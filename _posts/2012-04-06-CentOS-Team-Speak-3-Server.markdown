---
layout: post
title: CentOS Team Speak 3 Server
date: 2012-04-06
tags: ['centos','linux']
---

This guide will help to install Team Speak 3 Server on a CentOS 6 server.  This guide assumes that you have already installed CentOS 6 using the **Minimal** setting. Using a different option during installation should not impact the install of the Team Speak 3 server, but I cannot guarantee that. This was only tested using the default **Minimal** setting.  

Once I booted into CentOS, running `ifconfig` shows only the lo (loopback) interface.  

To correct this, we need to edit the network script for eth0.  
`vi /etc/sysconfig/network-scripts/ifcfg-eth0`  


*Update the information highlighted in yellow with your network information.*
Edit **ONBOOT="no"** to **ONBOOT="yes"**  
Add **BOOTPROTO=none**  
Add **NETWORK=<span style="background-color: yellow;">192.168.0.0</span>**  
Add **NETMASK=<span style="background-color: yellow;">255.255.255.0</span>**  
Add **IPADDR=<span style="background-color: yellow;">192.168.0.100</span>**  
Add **USERCTL="no"**  
  
Restart the network service  
`service network restart`  
  
ifconfig should now show eth0.  
  
Install wget  
`yum install wget`  
  
Download Teamspeak 3  
`wget http://teamspeak.gameserver.gamed.de/ts3/releases/3.0.3/teamspeak3-server_linux-x86-3.0.3.tar.gz`  
  
Untar  
`tar -zxvf teamspeak3-server_linux-x86-3.0.3.tar.gz`  
  
Rename folder (optional, if you do not follow this step you will need to adjust the autostart steps below.)  
`mv teamspeak3-server_linux-x86-3.0.3.tar.gz teamspeak3`  
  
Unblock client port in iptables  
`iptables -A INPUT -p udp -m udp --dport 9987 -j ACCEPT`  
`iptables -A INPUT -p tcp -m tcp --dport 30033 -j ACCEPT`  
`iptables -A INPUT -p tcp -m tcp --dport 10011 -j ACCEPT`  
  
Save iptables changes  
`service iptables save`  

Restart iptables  
`service iptables restart`  

Set Team Speak to autostart on boot  
`cp teamspeak3/ts3server_startscript.sh /etc/init.d/`  
`mv /etc/init.d/ts3server_startscript.sh /etc/init.d/teamspeak3`  
`chmod 755 /etc/init.d/teamspeak3`  
`chkconfig teamspeak3 on`  
  
Run Team Speak 3 server, or you can also reboot.  
`/etc/init.d/teamspeak3 start`  
  
On your client, open the teamspeak3 client and select **Connections** then select **Connect**  
  
In server address, put the **ip** or **hostname** of your server  

Choose a nickname  

Select **Connect**  

You should now be connected to your Team Speak 3 server.  There are additional steps that would need to be followed to make this public to the internet.  Mainly forwarding the ports on your home router and setting up a Dynamic DNS address for the server.
