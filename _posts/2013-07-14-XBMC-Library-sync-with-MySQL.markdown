---
layout: post
title: XBMC Library sync with MySQL
date: 2013-07-14
---

With the release of the RapberryPi I couldn't wait to buy one. So far I have purchased two. I plan to buy at least one for each TV in the house, and maybe a few more for random projects.  My main purpose for the Raspberry Pi that I own today is XBMC. Each Raspi runs [Openelec](http://www.openelec.tv/) . 

The main problem with running multiple XBMC devices are the libraries. You have to update each one individually by default and that becomes a pain. There are also issues with content locations. You have to enter them on each device, or you can copy sources.xml from one device to another.  After a quick run through the XBMC Wiki I came across an "experimental" feature that allows you to [sync your libraries using MySQL](http://wiki.xbmc.org/index.php?title=HOW-TO:Share_libraries_using_MySQL). It also includes how to share playlists, add-on data, keymaps, sources, rss feeds, "favourites" and network share passwords.  I started by installing MySQL on my media server. I would go step-by-step but the official wiki does a good job and provides steps for multiple OS's. You can check out the official guide [here](http://wiki.xbmc.org/index.php?title=HOW-TO:Share_libraries_using_MySQL/Setting_up_MySQL).  

Now configure XBMC to look at this database for the movie and music library. Once again, the wiki provides a great article [here](http://wiki.xbmc.org/index.php?title=HOW-TO:Share_libraries_using_MySQL/Setting_up_XBMC).  

Once this is complete, when you update one device the other is automatically updated since all devices look to this database for their information.

If you want to share some of the other features of XBMC check out [this](http://wiki.xbmc.org/index.php?title=HOW-TO:Share_libraries_using_MySQL/Sync_other_parts_of_XBMC) wiki article.