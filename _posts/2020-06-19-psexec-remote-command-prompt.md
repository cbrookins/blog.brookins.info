---
layout: post
title: Using PSExec for a remote command prompt
date: 2020-06-19
tags: ['workflow','tools']
---

Sometimes you just need to pull up a remote command prompt.  I use this in most cases to verify a device is what I think it is.  I just need to run a simple ``hostname`` command on a end user device.  
  

## How to

As the title suggests, I use [PSExec][1] to accomplish this.  These days you could also go the Powershell route, but this works more consistently for me at the time of writing. 
This tool requires that you have admin access to the remote device.  In my case I use this as a SysAdmin where we have implemented [LAPS][4], so I will need to pass a username and password to the command. 
If you are already admin on the device using your current credentials, possibly a domain environment without a PAW/LAPS setup, then you can exclude **-u** and **-p**. [This page][1] also includes all available parameters.  
  
Download PSExec, unzip, and execute a single time to accept the EULA. Now in a command prompt ``cd`` to the folder where you unzipped PSExec.exe.  
  
Execute the following to open a remote command prompt on a remote device
```
psexec \\[ip_or_hostname] cmd.exe -u [remote_device_admin] -p [remote_device_password]
```  
  
Once that executes it will drop you to a standard looking command prompt.  You can type ``hostname`` to display the computer name, and it should display the remote computers hostname. Now you can run any command as if you were sitting at the device.  
  
### Additional Items

[Sysinternals Suite][2] - This includes PSExec along with a [large list of additional tools][3]


[1]: https://docs.microsoft.com/en-us/sysinternals/downloads/psexec
[2]: https://download.sysinternals.com/files/SysinternalsSuite.zip
[3]: https://docs.microsoft.com/en-us/sysinternals/downloads/
[4]: https://www.microsoft.com/en-us/download/details.aspx?id=46899
