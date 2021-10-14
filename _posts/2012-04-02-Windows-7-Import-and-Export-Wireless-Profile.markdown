---
bg: "windows.gif"
layout: post
title: Windows 7 Import and Export Wireless Profile
date: 2012-04-02
tags: ['windows','microsoft']
---

I decided to script out my Windows customization so that I do not have to spend hours getting my interface the way that I like it.  I got hung up at the point of setting up my wireless network.  I didnt know how to set my wireless settings automatically.  After a little research in the Technet documentation I found a simple command line utility that is included in Windows 7 that I cannot believe I didnt already know about.  

Netsh is the tool I am referring to and even though it is not the easiest to use, it is very powerful.  

It is very simple to import and export wireless profiles.  So first, set up your computer to your wireless network.  

Open a command window by selecting the start orb and typing **cmd** in **Search programs and files**.  

Export the wireless profile  
`netsh wlan export profile profile_name`  


This will export the profile into the directory that your command window is currently in.  The default for a standard command window will be your profile directory (c:usersusername) as an XML file.  

Now you can script out the import of the profile using the following command  
`netsh wlan add profile "pathtoprofilexml"`  


Official documentation can be found <a href="http://technet.microsoft.com/en-us/library/cc754516(v=ws.10).aspx" target="_blank">here</a>.
