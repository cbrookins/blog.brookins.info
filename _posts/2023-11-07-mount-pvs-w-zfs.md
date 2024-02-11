---
bg: truenas_scale.gif
layout: post
title: Mount PVC with ZFS
date: 2023-11-07
tags: ['workflow','commands','zfs','truenas']
---

I have always been a fan of having my Kubernetes data easily accessible using a host path, along with a share so that I could access those host paths.  Come to find out, that is not considered best practice.  Mostly due to permission issues that can arise maintaining the container files along with the share itself.  To fix this I am moving to using a PVC (Persistent Volume Claim). This is my process for **TrueNAS**. The **k3s/kubectl/zfs** commands should be usable for other distros and Kubernetes setups.

### Identify the PVC
First lets get a list of all the PVC that we have.  
```
k3s kubectl get pvc -A | sort -u  
```
![output](/assets/images/pvc_01.png)

with this we can now look up where the PVC is stored on disk. Replacing **VOLUME** with the volume from our command above  


```
zfs list | grep VOLUME

EXAMPLE:
zfs list | grep pvc-b976c745-6c53-49d8-9d19-e2f47072a73e
```
![output](/assets/images/pvc_02.png)

### Mount the PVC
Now we are ready to mount the PVC.  Make sure the container is stopped and use the following command

```
zfs set mountpoint=/MOUNTPATH PATH/TO/PVC

EXAMPLE:
zfs set mountpoint=/flatnotes One/ix-applications/releases/flatnotes/volumes/pvc-b976c745-6c53-49d8-9d19-e2f47072a73e
```

You can now access the volume at the mount point.   

### Restore the original mount  
When you are done you need to remount it back to where it was with the following use the PATH/TO/PVC from earlier

```
zfs set mountpoint=legacy PATH/TO/PVC

EXAMPLE:
zfs set mountpoint=legacy One/ix-applications/releases/flatnotes/volumes/pvc-b976c745-6c53-49d8-9d19-e2f47072a73e
```  

### Sources
At the time of writing I found this information in the official [TrueCharts manual](https://truecharts.org/manual/SCALE/guides/pvc-access/).