---
bg: home-assistant.gif
layout: post
title: HAOS with a TrueNAS-VM
date: 2023-01-01
tags: ['truenas','home-assistant','linux','vm','zfs','automation','qemu']
---


As of writing this is the current state of Home Assistant installation methods. Of course, I want all the check marks.

![haos chart](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/HAOS_01.png "haos chart")

### The Problem
I am using TrueNAS, the installation provided for x86_64 is a disk image.  TrueNAS wants to use a zvol so I cant just attach this disk and expand it.  I found
some suggestions about using a live os and using Etcher to write the image.  In the end I think I found a better solution.  

### Solution
I started off by creating a dataset for vms.  I then created a vm with a 40G disk pointed at the new dataset. This created a zvol for my vm on the new dataset. 
Now I need to locate that new zvol.  

```
zfs list
```
In my case the dataset I created was called vm, which was nested under another dataset name One.  

```
One/vm
```

Now I needed to see where this volume was being mapped.  

```
ls -l /dev/zvol/One/vm
```
![zvol map](https://github.com/cbrookins/tech.brookins.info/raw/main/assets/images/HAOS_02.png "zvol map")

We will save the name `zd0` for later.  

I downloaded and unzipped the image on my local computer and then moved it to my TrueNAS server.  You could also do this directly to TrueNAS using **wget** and **tar**. 
You can find images [here](https://github.com/home-assistant/operating-system/releases).  Once you have it downloaded, extracted and located on your TrueNAS server
we need to convert the **haos x86_64** image to **raw**.  You will need to replace the path `/path/to/image/` in the following command with the path where you
placed the image.  

```
qemu-img convert -f qcow2 /path/to/image/haos_ova-9.4.qcow2 -O raw /path/to/image/haos_ova-9.4.raw
```

Now we write this image to the zvol using the following. You will need to replace the path `/path/to/image/` in the following command with the path where you
placed the image. You will also need to replace `zd0` with the output that you saved earlier, from the output of the `ls` command.  

```
sudo dd if=/path/to/image/haos_ova-9.4.raw of=/dev/zd0 bs=1M
```

This could take some time, but once it is complete you can start your vm and it should boot into HAOS.
