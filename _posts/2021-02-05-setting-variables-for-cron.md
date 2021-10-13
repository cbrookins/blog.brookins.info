---
layout: post
title: Setting variables for Cron jobs
date: 2021-02-05
tags: ['script','workflow']
---

I recently started moving some personal stuff up to Github, which brought me to the issue of hard coded information that needed to be scrubbed.  I am using Githubs private repositories, but still feel some kind of way about putting certain types of things in the repo.  Mostly webhook urls, usernames, email addresses, etc.  The general solution I came aross was using environment variables that you set on the server running the scripts. This also solves a common issue where when something hardcoded does change, you have to update multiple scripts, where as using a variable you can just update it on the system and all scripts have the new information.  
  
No problem, I update my scripts to use variables.  I set those variables and test the script, no issues, so I set a Cron job.  I am all set.  The following day I check in to verify everything ran smoothly.  Nothing.  I manually kick of the script.  Success.  Wait on the cron.  Nothing.  
  
Come to find out, Cron jobs do not import all environment variables. Luckily they do provide a way to provide variables to Cron.  
  
Using `crontab -e` you can set variables just as you would in `/etc/environment`

Add your variables to the top of the file.

```
var1=/home/user/scripts  
var2=https://webhook.url
```
Save the changes.  
Now when you run a cron job it will have access to those variables that you set.
