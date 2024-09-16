---
bg: "truenas.gif"
layout: post
title: Using timezone/localtime in TrueNAS SCALE containers
date: 2024-09-16
tags: ['linux','truenas','docker','k3s']
---

Most Docker images these days provide a variable to set your timezone, but sometimes the creator expects you to be able to use **/etc/timezone** and **/etc/localtime** from the host machine.  TrueNAS Scale requires an extra step to make them available to your containers.

TrueNAS SCALE only allows you to access the ZFS volume for containers, so you cannot set a host path for **/etc/timezone** or **/etc/localtime**.  The easiest solution for me was to create a symbolic link to these files on the ZFS volume.

This example will use the ZFS volume named **main**

From the CLI create the following symlinks
```
cd /mnt/main

ln -s /etc/timezone
ln -s /etc/localtime
```

This will create the following files in the **/mnt/main** path  

**timezone**  
**localtime**

You should now be able to use them with your containers using the path
```
/mnt/main/timezone
```
```
/mnt/main/localtime
```