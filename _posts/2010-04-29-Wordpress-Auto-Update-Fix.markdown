---
layout: post
title: Wordpress Auto Update Fix
date: 2010-04-29
---

I recently ran into a problem with my Wordpress installations. I could not auto update my plugins. After some research, I found that it was a problem with the hosting server having php4 and php5 enabled at the same time. This is common practice for shared hosting plans.  I found that adding the following lines to the **.htaccess** file will fix the problem.  
  
`AddType x-mapp-php5.php`  
`AddHandler x-mapp-php5.php`  
  
Before doing this, I would recommend you backup your Wordpress installation (incl. database, files and folders).
