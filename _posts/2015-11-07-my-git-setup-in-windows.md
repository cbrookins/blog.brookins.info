---
layout: post
title: My git setup in Windows
date: 2015-11-07
---

*This is meant as a reference for me.  I like to nuke and pave my workstation so much that I am constantly setting everything back up the way I like it.  Git is one of those things where I can never remember all the details.*

*This article assumes you have already generated your SSH keys and added your private keys Github or another Git repo service*

## Requirements
[Git](http://www.git-scm.com/)  
[plink](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)  
[pageant](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html)  

## Set up
To start off I install Git.  In my case I like to use [Chocolatey](http://chocolatey.org), but that is just a preference.  You can install Git with the standard install.

``choco install -y git.install``

For the other tools, just download them and drop them wherever you like.  I like to use Chocolatey for this also.  Chocolatey installs plink.exe and pageant.exe to **%PROGRAMFILES%\Putty** for 32-bit OS and **%PROGRAMFILES(X86)%\Putty** for 64-bit OS.

``choco install -y putty.install``

### Environment Variables
Now create a system variable with the name **GIT_SSH** and set the value to the path for plink.exe.  There are many ways to do this, but this is what I like best. It integrates nicely into Windows and I have no need to use the Git Bash shell.

``C:\Program Files(x86)\Putty\plink.exe``

### Pageant
Pageant will need to be running each time you make a SSH connection.  Its job is to hold your private keys.

I set Pageant to run at startup.  I do not auto load my keys for security, but this can be done using the following format for the startup item.

``%PROGRAMFILES(X86)%\Putty\pageant.exe C:\path\to\key1.ppk c:\path\to\key2.ppk``

### Plink
Now plink is set up to be your SSH client when using git.  And will use Pageant to manage your private keys.  You can test using the following command

``plink git@github.com``

If your private SSH key is set up in Pageant and your public key has been imported into Github you should receive the message

``Hi your_username!  You've successfully authenticated, but Github does not provide shell access.``

## Conclusion
From now on plink and pageant should handle all of the SSH goodness with Git.
