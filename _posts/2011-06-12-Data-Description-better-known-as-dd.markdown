---
layout: post
title: Data Description better known as dd
date: 2011-06-12
tags: ['linux','tools']
---

One thing that you cannot get away from in IT is the need to copy hard drives, mostly referred to as "imaging" or cloning hard drives.  

Imaging hard drives is a must in break/fix situations. Most of the time it is much quicker to image a hard drive than it is to fix the problem that is occurring. You can spend hours trying to remove viruses and spyware and then you just hope you removed everything. There is no way to know for sure. Imaging hard drives takes care of that and dd does a great job.  

dd stands for Data Description and can be used to do all sorts of functions related to cloning. dd has the ability to copy the contents of a physical drive into a image file, or from one physical disk to another physical disk. dd allows for this copy to take place over a network connection and even over a secure ssh connection.  

This tool is as bare bones as it gets. This tool does not come with a gui interface but there a multiple gui interfaces that have been written for dd. A notable one is <a href="http://sourceforge.net/apps/mediawiki/air-imager" target="_blank">AIR</a>(cross-platform).  

Examples of dd commands:  

Create ISO image of CD/DVD (&#8216;sr0 is my CD-Rom device)  
dd if=/dev/sr0 of=/path/to/file.iso  


Clone one drive to another  
dd if=/dev/hd1 of=/dev/hd2  


Create an image file of one drive and send it to another machine via ssh  
dd if=/dev/hd1 | ssh @ "dd of=/path/to/file.image"  n
