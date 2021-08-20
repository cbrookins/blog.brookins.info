---
layout: post
title: Backup using smbclient
date: 2011-02-17
---

I have a large music collection that I share across my home network using DAAP. My wife on the other hand, does not have much of a music collection. She has no problem streaming the music when she is at home, but getting that music to her Ipod is a challenge. Since the music is only available over DAAP, she does not have access to add it to her Ipod.  

Instead of having her download over the stream, I decided it would be best to make her a local copy of my music. I made a one time dump of my music on to her external, but found out quickly that this wouldnt work. As I added to my collection she fell further behind. I had to keep up with making constant copies of my music. I decided to make a script to handle this for me.  

After some searching I decided to use smbclient as my solution. It is pretty basic and functions similar to a command line ftp client. The following command is what I am using:  

/usr/bin/smbclient//<span style="background-color: yellow;">ip_or_hostname</span>/<span style="background-color: yellow;">share_name</span><ipaddress><sharename><ipaddress><sharename>-N -c "recurse; prompt; lcd /<span style="background-color: yellow;">path</span>/<span style="background-color: yellow;">to</span>/<span style="background-color: yellow;">filesyouwantbackedup</span>; mput *; exit;" </sharename></ipaddress></sharename></ipaddress>  

<ipaddress><sharename><ipaddress><sharename>  
</sharename></ipaddress></sharename></ipaddress>  

Breaking down the command, the first bit is the absolute path to smbclient.  
That is followed by the SMB path to the share on my target computer.  
The -N option suppresses the password prompt.  
-c is used to mark the start of smbclient operations or a string of operations. Each operation is separated by a semicolon and all operations are enclosed in quotes.  

You can get a list of all the options and operations at <a href="http://www.samba.org/samba/docs/man/manpages-3/smbclient.1.html" target="_blank">http://www.samba.org/samba/docs/man/manpages-3/smbclient.1.html</a>  

Once I had my script set up, and tested, I set up a cron job to run daily and update the share folder for me. Working perfectly, so far.  

I am sure you could get more involved in this to do a lot more. This fit my situation perfectly since I never remove any music, I only add. I am not sure if this would be best to sync a folder, but it works great to constantly update one. For syncing, I would recommend RSync.",
