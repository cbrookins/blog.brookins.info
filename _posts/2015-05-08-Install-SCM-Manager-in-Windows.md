---
layout: post
title: Install SCM Manager in Windows
date: 2015-05-08
---

**This post assumes you already have a Windows server available**

## Prerequisites
- Windows Server
- Java 1.6 or newer (Java 1.6 = Java 6)
- A copy of SCM Manager ([Download here][2])

## Setup

### Install Java
At the time of writing this, I am using **Java 8u45**.  

### Prep SCM Manager
Unzip your download of SCM Manager to a folder in Program Files. In my case I am working with a 64-bit operating system so I unzipped everything to **C:\Program Files (x86)\scm-server**.  The installation is complete.  

### Set SCM Manager to start at boot
So I know that you can install this as a service using the **install** parameter, but when I did this the service would not start.  So instead of wasting time trying to figure that out, I improvised.  

In Windows Task Scheduler I created a task to run at system startup to run scm-server.bat, located in the bin folder under scm-server.  You can reboot now and test.

Since I was setting this up for my workplace I set this task to run as a service account instead of my own account.  That way the software will continue to function even if I leave the organization.  

### Configure SCM Manager
After reboot the SCM Server should be running and with a web browser you can now open up the administration console.

**http://localhost:8080**  

Username: **scmadmin**  
Password: **scmadmin**  (Change this)

![][i1]

Now under **Config** select each item and configure to your liking.  I made a chage to the **Base Url** and then under **Repository Types** I moved each type to a new location, outside of the user profile.

![][i2]

You can add new users under **Security > Users**, and groups under **Security > Groups**.  But the magic happens under **Main > Repositories**.  Here is where you can create your repos and manage permissions and get the repo url.

![][i3]

## Conclusion
At this point you should have a runnig git server providing a web front end for management.  With the plugins available you can extend the functionality of the product to include things like Active Directory authentication or bug tracking with Bugzilla and Trac.  This software is pretty flexible and very easy to set up. Well worth trying out.

[1]: https://www.scm-manager.org    "SCM Manager"
[2]: https://www.scm-manager.org/download/  "Download"

[i1]: https://vh4ksg-sn3302.files.1drv.com/y2p0AdelSlP7tH5Ttsi7YVpzH0H0iPel1Yn-giv8I-SYf7lnWVOAnvLsuX2trBG01vFW00T2pSLWikxIM18viv5Rcw2_Ku4IMiO2rgxkZKyyo2p5JFixjseBSGR9x0mzmEkEQ9RL1asvx85uUlgO9zuxPj7i-20UOwgBMlNgfXibfo/20150508_SCMManager_01.PNG  "login"
[i2]: https://vh4ksg-sn3302.files.1drv.com/y2pW0guN7N38Nc3rvPNVAmWfQi7zsktwJEyGSjKJuYC-LCaO2qsaGOdYyovdMFghUmfgson1L-DKGI-SQ6CNYrZClzZ7v1-CNm4SQFDANNoXKOpQE3Zr-Jetz7ChgYIFKS4l-Mq8OAoV15603CLCxkYv0ob7WxTdEfKeiqUN0w7dLg/20150508_SCMManager_03.PNG  "navigation"
[i3]: https://vh4ksg-sn3302.files.1drv.com/y2pq1OWC2OiBAiy6u64AdJFA-qiKZ9VM8Nin1mr1qj_dyigRGmylXcpVjN0eEGR1VlVxa_ECnUmVid32FTdgC-tWW-avH8gIBbVPPiPG7zNcOjZu0yrfFBA9iQGP_WI7hu8MTeg1I7Sa4dPj_TjPOse4xjVIgW7bfFzk8c-mKNbz0A/20150508_SCMManager_04.PNG  "repos"
