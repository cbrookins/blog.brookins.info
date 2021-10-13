---
layout: post
title: Convert a Virtualbox VDI to a VMWare VMDK
date: 2012-01-21
tags: ['virtualbox','vmware']
---

I recently made the switch from a headless <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> server running <a href="http://code.google.com/p/phpvirtualbox/" target="_blank">PHPVirtualbox</a> to the free <a href="http://www.vmware.com/products/vsphere-hypervisor/overview.html" target="_blank">VMWare vSphere Hypervisor (ESXi)</a>.  Switching out the <a href="http://ubuntu.com/" target="_blank">Ubuntu Server 10.04</a> OS for the vSphere hypervisor was simple.  Took less than thirty minutes.  The problem came when I found out that vSphere doesnt like the <a href="http://en.wikipedia.org/wiki/VDI_(file_format)#Virtual_Disk_Image" target="_blank">VDI</a> files that <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> creates by default.  I probably should have checked that first.  

I knew it couldnt be that hard to convert the files, so I started by checking out tools that were available from VMWare. First was the <a href="http://www.vmware.com/products/converter/" target="_blank">VMWare vCenter Converter</a>.  It was described as "Automate and simplify physical to virtual machine conversions as well as conversions between virtual machine formats".  vCenter Converter did not recognize my <a href="http://en.wikipedia.org/wiki/VDI_(file_format)#Virtual_Disk_Image" target="_blank">VDI</a> files.  

Next I came across a lot of people saying to use <a href="http://qemu.org/" target="_blank">Qemu</a> to do the conversion.  Currently I am on a Windows 7 workstation, so this option is no good. I could use a Linux VM or boot to a live distro, but what can I do with what I already have?  

Then I found, in the last place I thought to look, in the <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> documentation&#8230;<a href="http://www.virtualbox.org/manual/ch08.html" target="_blank">http://www.virtualbox.org/manual/ch08.html</a>.  I had used VBoxManage in the past to create <a href="http://en.wikipedia.org/wiki/VDI_(file_format)#Virtual_Disk_Image" target="_blank">VDI</a> files from RAW disks, but it didnt occur to me at first to see what else it could do.  Well, it can convert from <a href="http://en.wikipedia.org/wiki/VDI_(file_format)#Virtual_Disk_Image" target="_blank">VDI</a> to <a href="http://en.wikipedia.org/wiki/VMDK" target="_blank">VMDK</a> and it is VERY easy.  All you need is <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> installed.   

In a Windows command prompt &#8216;cd to the <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> installation directory and run the following command.  You can also add the <a href="http://www.virtualbox.org/" target="_blank">Virtualbox</a> installation directory to your PATH statement if you do not want to &#8216;cd all the time.  Dont forget to change the "pathtoimage.vdi" and "pathtoimage.vmdk".  

In Linux you can run the command as is. Just copy and past, changing the "pathtoimage.vdi" and "pathtoimage.vmdk".  

`VBoxManage clonehd "pathtoimage.vdi" "pathtoimage.vmdk --format VMDK`
