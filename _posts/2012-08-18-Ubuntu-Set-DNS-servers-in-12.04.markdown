---
layout: post
title: Ubuntu Set DNS servers in 12.04
date: 2012-08-18
---

After doing clean installs of Ubuntu 12.04 server on my development machine I came across an odd problem on each machine.  As I was trying to update the clean installs I kept getting "could not resolve address" error during the &#8216;apt-get update process.  After playing with it for a minute I realized that DNS was not working.  I could ping the Google IP, but when I pinged Google by name it would fail.  

My fix would have been to update the resolv.conf file, but the first line of that file now states that changes will be overwritten.  Well, this is different.  Apparently Ubuntu has switched to a set of scripts named <a href="http://en.wikipedia.org/wiki/Resolvconf" target="_blank">resolvconf</a> to handle the resolv.conf file.  

Okay, so how do I update my name servers now?  Well, it is actually pretty easy.  

First, edit /etc/network/interfaces  

`sudo nano /etc/network/interfaces`  


Now add `dns-nameservers xx.xxx.xxx.xx xx.xxx.xxx.xx` under the interface you want the settings to be applied to.  

Example:  
  
    auto lo  
    iface lo inet loopback  

    auto etho  
    iface etho inet static  
    address 192.168.0.42  
    network 192.168.0.0  
    netmask 255.255.255.0  
    broadcast 192.168.0.255  
    gateway 192.168.0.1  
    dns-nameservers 8.8.8.8 8.8.4.4  
  
  
There are other ways to accomplish this. I found <a href="http://www.stgraber.org/2012/02/24/dns-in-ubuntu-12-04/" rel="nofollow" target="_blank">this article</a>, which describes how to use &#8216;tail files in<a href="http://en.wikipedia.org/wiki/Resolvconf" target="_blank">resolvconf</a>. This seemed overly complicated compared to using the way described in this article, but using tail files could have some benefit that I do not know about.
