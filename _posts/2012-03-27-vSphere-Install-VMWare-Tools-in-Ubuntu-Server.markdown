---
layout: post
title: vSphere Install VMWare Tools in Ubuntu Server
date: 2012-03-27
tags: ['vmware', 'ubuntu','linux']
---

<i>"VMware Tools is a suite of utilities that enhances the performance of the virtual machines guest operating system and improves management of the virtual machine. Without VMware Tools installed in your guest operating system, guest performance lacks important functionality."</i>  

This article assumes that you already have vSphere installed with a virtual instance of Ubuntu Server 10.04 installed as a guest.  

In vSphere client select VM &gt; Guest &gt; Install/Upgrade VMWare Tools  

Update your Ubuntu installation  
`sudo apt-get update && sudo apt-get upgrade`  


Install build-essential, binutils and the headers of your current kernel  
`sudo apt-get install build-essential binutils linux-headers-$(uname -r)`  


Mount the CD inside of your Ubuntu instance  
`mount /dev/scd0 /cdrom`  


Untar VMWare Tools  
`tar -vxzf /cdrom/VMWareTools*.tar.gz -C /tmp`  


Install VMWare Tools  
`cd /tmp/vmware-tools-distrib`  
`./vmware-install.pl`  


  
You will have to redo this each time you update your servers kernel.  

Official documentation can be found <a href="http://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&docTypeID=DT_KB_1_1&externalId=1022525" target="_blank">here</a>.
