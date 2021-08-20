---
layout: post
title: ioCage Notes
date: 
---

## ioCage Notes
iocage fetch  

iocage create -n backupjail ip4_addr="igb1|192.168.2.30/24" -r 11.1-RELEASE  

iocage list  

iocage start {jailNameHere}  

iocage set boot=on {jailNameHere}  

iocage console {yourJailNameHere}  

iocage exec {jailNameHere} {FreeBSDCOmmandHERE}  

iocage restart ALL  
iocage restart {jailNameHere}  

iocage destroy {jailNameHere}  

iocage update {jailNameHere}  
