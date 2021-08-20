---
layout: post
title: Windows 7 Fix Boot Loader
date: 2010-06-05
---

I was playing around with a Linux distro (Backtrack 4) on my netbook and accidently overwrote the Windows boot loader with the GRUB boot loader. My workstation would not boot anymore but I knew everything was still in place. All I had to do was restore the Windows boot loader.  

To do this, you will need the installation media for Windows. In my case, it was upgrade media that I downloaded and created a bootable USB drive with.  

Once you boot to the installation media, choose **Repair your computer** from the second screen.  

Then choose the installation you want to repair from the list and select **Next**. Most users will only have one choice.  

From the next menu select **Command Prompt**  

Then enter the command:  
`bootrec /fixmbr`  
  
Now you can reboot your workstation and Windows should boot up with no problem.  

**Note:** I found that some users needed to also run the command:  
`bootrec /FixBoot`  
*I did not need to run this command to fix my workstation, but depending on the situation, you may need to.*
