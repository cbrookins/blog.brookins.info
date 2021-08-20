---
layout: post
title: Ubuntu Installation using preseed file
date:
---
  
## Scenario  
Hands free installation of Ubuntu over PXE.  Although not truly "hands free" since I still had to PXE boot and set up my keyboard and language.  
  
Notes  
preseed.cfg  
add auto url=tftp://tftpserver/path/to/preseed.cfg to the append line  
Example preseed https://help.ubuntu.com/lts/installation-guide/example-preseed.txt  
