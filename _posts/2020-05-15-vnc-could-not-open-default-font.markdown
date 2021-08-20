---
layout: post
title: vncserver Could not open default font error
date: 2020-05-15
---

## Problem
When trying to start vnc using the command **vncserver** on a Kali Linux install, I would receive the error **Could not open default font 'fixed'**  
  
## Solution  
Run command ``dpkg-reconfigure xfonts-base``
