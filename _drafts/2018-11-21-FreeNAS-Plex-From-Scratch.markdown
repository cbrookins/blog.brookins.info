---
layout: post
title: Create a custom jail for Plex
date:
---

## FreeNAS Templates  
http://ftp-archive.freebsd.org/pub/FreeBSD/releases/amd64/11.1-RELEASE/base.txz  
http://ftp-archive.freebsd.org/pub/FreeBSD/releases/amd64/11.2-RELEASE/base.txz  

## Prerequisites  
vi /usr/local/etc/pkg/repos/FreeBSD.conf  
update url to https://pkg.freebsd.org/FreeBSD:11:amd64/quarterly  

## Install Plex  
pkg install plexmediaserver  
sysrc -f /etc/rc.conf plexmediaserver_enable="YES"  
service plexmediaserver start 2>/dev/null  
