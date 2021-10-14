---
bg: "windows.gif"
layout: post
title: Windows 7 Reinstall Boot Loader
date: 2012-02-09
tags: ['windows','microsoft']
---

So I installed Ubuntu on my laptop in a dual boot setup. Windows was already present so I let Ubuntu do its thing and ended up with Windows 7 and Ubuntu on my hard drive with the grub boot loader. Easy. No problems there.  

Now I wanted to remove Ubuntu, but how do I do that and get the Windows boot loader back? It was way simpler than I thought it would be. I was expecting to do a full blown Windows repair, but no.  

First you will need a Windows 7 boot cd. I had a Home Premium CD for my laptop, and my laptop is running Home Premium. I am not sure if you can use any old Windows 7 CD but my first guess would be that it would be fine. If anyone knows for sure, leave me a comment.  

Boot to your Windows 7 CD  

<a href="http://2.bp.blogspot.com/-feEIR81_0L4/T1ghJuG6ErI/AAAAAAAABPg/JMnp8Mk9exk/s1600/Screenshot-2012-02-09_18.21.01.png" imageanchor="1" style="clear: left; margin-bottom: 1em; margin-right: 1em;" target="_blank"><img border="0" height="150" src="http://2.bp.blogspot.com/-feEIR81_0L4/T1ghJuG6ErI/AAAAAAAABPg/JMnp8Mk9exk/s200/Screenshot-2012-02-09_18.21.01.png" width="200"/></a><a href="http://2.bp.blogspot.com/-V3qN2eEjWrI/T1ghMNKCYSI/AAAAAAAABPw/YdrwnaGeHaA/s1600/Screenshot-2012-02-09_18.22.13.png" imageanchor="1" style="clear: left; margin-bottom: 1em; margin-right: 1em; text-align: center;" target="_blank"><img border="0" height="150" src="http://2.bp.blogspot.com/-V3qN2eEjWrI/T1ghMNKCYSI/AAAAAAAABPw/YdrwnaGeHaA/s200/Screenshot-2012-02-09_18.22.13.png" width="200"/></a><a href="http://1.bp.blogspot.com/-vz2aoB8OJP0/T1ghK4p1CdI/AAAAAAAABPo/du486Zf7iD4/s1600/Screenshot-2012-02-09_18.21.29.png" imageanchor="1" style="clear: left; margin-bottom: 1em; margin-right: 1em;" target="_blank"><img border="0" height="150" src="http://1.bp.blogspot.com/-vz2aoB8OJP0/T1ghK4p1CdI/AAAAAAAABPo/du486Zf7iD4/s200/Screenshot-2012-02-09_18.21.29.png" width="200"/></a><a href="http://4.bp.blogspot.com/-BbIZleEm5yE/T1ghNOPHXTI/AAAAAAAABP4/Si4DLdNnaZw/s1600/Screenshot-2012-02-09_18.22.28.png" imageanchor="1" style="clear: left; margin-bottom: 1em; margin-right: 1em; text-align: center;" target="_blank"><img border="0" height="150" src="http://4.bp.blogspot.com/-BbIZleEm5yE/T1ghNOPHXTI/AAAAAAAABP4/Si4DLdNnaZw/s200/Screenshot-2012-02-09_18.22.28.png" width="200"/></a><a href="http://3.bp.blogspot.com/-dwkT5ZdnJ04/T1ghN9WdGLI/AAAAAAAABQA/D6x5giZNxEc/s1600/Screenshot-2012-02-09_18.22.45.png" imageanchor="1" style="clear: left; margin-bottom: 1em; margin-right: 1em;" target="_blank"><img border="0" height="150" src="http://3.bp.blogspot.com/-dwkT5ZdnJ04/T1ghN9WdGLI/AAAAAAAABQA/D6x5giZNxEc/s200/Screenshot-2012-02-09_18.22.45.png" width="200"/></a>      

On the first screen select **Next**  
On screen two select **Repair your computer**  
The third screen should display all of the valid Windows 7 installations that are on the HDD/SSD, select the **Use recovery tools...** radio button and then select Next.  
On the fourth screen select **Command Prompt**  
This brings you to the fifth, and final, screen.  On screen five you will enter the commands  

`bootrec /rebuildbcd`  
`bootrec /fixmbr`  
`bootrec /fixboot`  


Now reboot your workstation and the Windows boot manager is back.  To completely remove Ubuntu, you can remove the partitions and extend you windows partition to consume the unused space.
