---
layout: post
title: SecuritySurveillance using ZoneMinder
date: 2011-06-02
---

I wanted a way to provide some security to my home and give me the ability to remotely view what was happening around my house when I was away. I found plenty of ways to do this using a single camera, but I needed more. I was thinking more like five cameras. Then I remembered ZoneMinder. I found this a few years ago and never though too much about it. Didnt have a use for it at the time, mostly because I didnt own a home. Now that I do, I want to keep an eye on it from time to time. ZoneMinder will allow me to do everything I want at the low cost of Free. I do suggest that you give a donation to this project. It is well worth anything you can afford.   

First things first, we need a workstation. A Linux workstation. Since it is me, a Ubuntu Linux workstation.   

Start out by installing Ubuntu Linux Desktop 10.04 LTS. Why desktop? Because I couldnt get the server version to work. I will look into it and see why, but for now, the desktop version works. Why 10.04 LTS? Because it is LTS, or Long Term Support. I do not plan on upgrading this too often since it will be a work horse. I need as many patches and fixes as I can get out of one version. 10.04 is it for now.   

<a href="http://3.bp.blogspot.com/-CHztb04EF3Q/T1gjWicVD4I/AAAAAAAABQ4/Rl6RIGFT0_Y/s1600/zoneminder_2.png" target="_blank"><img alt="image" height="141" src="http://3.bp.blogspot.com/-CHztb04EF3Q/T1gjWicVD4I/AAAAAAAABQ4/Rl6RIGFT0_Y/s200/zoneminder_2.png" width="200"/></a><a href="http://1.bp.blogspot.com/-Nr9xN6Ps2J8/T1gjXAFZXFI/AAAAAAAABRA/J3JYTzkREJM/s1600/zoneminder_3.png" target="_blank"><img alt="image" height="141" src="http://1.bp.blogspot.com/-Nr9xN6Ps2J8/T1gjXAFZXFI/AAAAAAAABRA/J3JYTzkREJM/s200/zoneminder_3.png" width="200"/></a><a href="http://2.bp.blogspot.com/-kmxeOKx4M28/T1gjXYR2tCI/AAAAAAAABRI/uo6G-pGgelU/s1600/zoneminder_4.png" target="_blank"><img alt="image" height="141" src="http://2.bp.blogspot.com/-kmxeOKx4M28/T1gjXYR2tCI/AAAAAAAABRI/uo6G-pGgelU/s200/zoneminder_4.png" width="200"/></a>

Next we will update Ubuntu and install ZoneMinder using the command  
`sudo apt-get update && sudo apt-get -y upgrade && sudo apt-get -y install zoneminder`  

<a href="http://1.bp.blogspot.com/-bfZk4RQgEqw/T1gjYBmXbdI/AAAAAAAABRY/GWS-RzZXpe4/s1600/zoneminder_6.png" target="_blank"><img alt="image" height="141" src="http://1.bp.blogspot.com/-bfZk4RQgEqw/T1gjYBmXbdI/AAAAAAAABRY/GWS-RzZXpe4/s200/zoneminder_6.png" width="200"/></a><  
Enter a root password for MySQL when it prompts you.   

<a href="http://2.bp.blogspot.com/-iweg-mgJ1LI/T1gjYgx8dbI/AAAAAAAABRg/h8XaHtVhF9g/s1600/zoneminder_7.png" target="_blank"><img alt="image" height="142" src="http://2.bp.blogspot.com/-iweg-mgJ1LI/T1gjYgx8dbI/AAAAAAAABRg/h8XaHtVhF9g/s200/zoneminder_7.png" width="200"/></a>  
Then enter the hostname of your server when it prompts.  

<a href="http://1.bp.blogspot.com/-uiB0EFvSApU/T1gjY8RHfRI/AAAAAAAABRo/CZAiT_zpG-s/s1600/zoneminder_8.png" target="_blank"><img alt="image" height="141" src="http://1.bp.blogspot.com/-uiB0EFvSApU/T1gjY8RHfRI/AAAAAAAABRo/CZAiT_zpG-s/s200/zoneminder_8.png" width="200"/></a>  

Now you need to copy the ZoneMinder Apache configuration into the Apache conf.d directory and name it **zoneminder.conf**.  
`sudo cp /etc/zm/apache.conf /etc/apache2/conf.d/zoneminder.conf`  


Reload Apache  
`sudo /etc/init.d/apache2 force-reload`  


Add the www-data user to the video group  
`sudo adduser www-data video`  


Restart ZoneMinder  
`sudo /etc/init.d/zoneminder restart`  


You can now access the ZoneMinder web interface by pointing your browser of choice at  
`http://localhost/zm`  

The interface is simple, but very functional. All you have to do to get up and running is add a new monitor by selecting Add New Monitor and filling out the information on the source tab.  
<a href="http://2.bp.blogspot.com/-8Ua8Sgk1ifk/T1gjVyiA8sI/AAAAAAAABQo/zHRKi5S_Oqk/s1600/zoneminder_014.png" target="_blank"><img alt="image" height="127" src="http://2.bp.blogspot.com/-8Ua8Sgk1ifk/T1gjVyiA8sI/AAAAAAAABQo/zHRKi5S_Oqk/s200/zoneminder_014.png" width="200"/></a><a href="http://4.bp.blogspot.com/-9oYN3_U2Uek/T1gjWDcwumI/AAAAAAAABQw/VhwPjxaQaZ4/s1600/zoneminder_015.png" target="_blank"><img alt="image" height="200" src="http://4.bp.blogspot.com/-9oYN3_U2Uek/T1gjWDcwumI/AAAAAAAABQw/VhwPjxaQaZ4/s200/zoneminder_015.png" width="182"/></a>  

Check out the <a href="http://www.zoneminder.com/screenshots" target="_blank">screenshots</a> on the <a href="http://www.zoneminder.com/" target="_blank">ZoneMinder</a> website for a better look at what can be accomplished.