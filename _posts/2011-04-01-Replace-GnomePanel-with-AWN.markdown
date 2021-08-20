---
layout: post
title: Replace GnomePanel with AWN
date: 2011-04-01
---

If you had asked me a year ago whether or not it was a good idea to use a dock, I probably wouldnt have said yes. I had seen docks used in the past with Ubuntu, and I tried plenty of times to use them exclusively. After so many failed attempts and lack of stable features on the docks that were available I gave up.  

Recently I decided to give docks another chance. I went out to find what the current contenders where and found Docky and AWN (Avant Window Navigator) I did some basic testing to see what kind of features were available and which one ran the lightest on the system.  

It didnt take long to decide on AWN. Using basic features and no hacks or plugins I found that AWN had the smallest footprint on the system resources. It also had the best feature set out of the box, for me. It also ended up being the one that I was able to get everything I needed/wanted with no problems, or searching.  

<a href="http://4.bp.blogspot.com/-qgXxrq2oOew/T1qVsyQNNSI/AAAAAAAABT4/gY7BUzINvKY/s1600/awn_dock.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;" target="_blank"><img border="0" height="20" src="http://4.bp.blogspot.com/-qgXxrq2oOew/T1qVsyQNNSI/AAAAAAAABT4/gY7BUzINvKY/s400/awn_dock.png" width="400"/></a>  

That when I noticed, the problem. I couldnt remove the very last panel from the desktop. I had it autohide so that I couldnt see it but that wasnt enough. It had to go. After some short work in the Ubuntu forums I came out with this.  

Hit **Alt+F2** on your keyboard  

<img border="0" height="177" src="http://1.bp.blogspot.com/-oPbB-doReO8/T1qVsg7u0ZI/AAAAAAAABTw/72lopyk1Km8/s320/alt%252Bf1.png" width="320"/>  
Type gconf-editor and hit Enter, or select Run  

<img border="0" height="180" src="http://4.bp.blogspot.com/-KT2dyAwPBxk/T1qWAg9K7LI/AAAAAAAABUg/CUWx00xTqSM/s320/alt+f1_1.png" width="320"/>  
Expand **Desktop** in the left pane  
Expand **Gnome** in the left pane  
Expand **Session** in the left pane  
Select **Required-Components** in the left pane  

<a href="http://3.bp.blogspot.com/-I05uZHynqN8/T1qVtf141rI/AAAAAAAABUA/10cRiWqfdp4/s1600/gconfeditor.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;" target="_blank"><img border="0" height="250" src="http://3.bp.blogspot.com/-I05uZHynqN8/T1qVtf141rI/AAAAAAAABUA/10cRiWqfdp4/s320/gconfeditor.png" width="320"/></a>  
Edit Panel in the right side pane  

<a href="http://1.bp.blogspot.com/-J6Wr-YRY4pQ/T1qVtv_wP7I/AAAAAAAABUI/iMVltCtRIjI/s1600/gconfeditor_1.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;" target="_blank"><img border="0" height="196" src="http://1.bp.blogspot.com/-J6Wr-YRY4pQ/T1qVtv_wP7I/AAAAAAAABUI/iMVltCtRIjI/s320/gconfeditor_1.png" width="320"/></a>  
Replace **gnome-panel** with **avant-window-navigator**  
<a href="http://tech.brookins.info/wp-content/uploads/2011/04/gconfeditor_3.png" target="_blank"></a>  
<a href="http://1.bp.blogspot.com/-54eZFwYlx0U/T1qVuL8aH3I/AAAAAAAABUQ/cY3mQHgGrnw/s1600/gconfeditor_2.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;" target="_blank"><img border="0" height="196" src="http://1.bp.blogspot.com/-54eZFwYlx0U/T1qVuL8aH3I/AAAAAAAABUQ/cY3mQHgGrnw/s320/gconfeditor_2.png" width="320"/></a>  

<a href="http://4.bp.blogspot.com/-57Ifh-qJMnw/T1qVusVBcCI/AAAAAAAABUY/pA6JDFFF8LM/s1600/gconfeditor_3.png" imageanchor="1" style="margin-left: 1em; margin-right: 1em;" target="_blank"><img border="0" height="250" src="http://4.bp.blogspot.com/-57Ifh-qJMnw/T1qVusVBcCI/AAAAAAAABUY/pA6JDFFF8LM/s320/gconfeditor_3.png" width="320"/></a>  
This will cause gnome-panel not to load the next time you log in and start AWN instead.  You could also use this for docky or any other application that you want to run in place of gnome-panel.  

**Disclaimer:** I only tested this on Ubuntu 10.10.
