---
bg: "script.gif"
layout: post
title: NGINX proxy for Docker
date: 2022-02-11
tags: ['docker','ubuntu','nginx']
---

I run a few docker containers and self hosted software within my home to do various things.  I finally got tired of remembering port numbers and wanted to move to using sub domains.  

I chose to use [NGINX](https://www.nginx.com/) to solve this problem.  I am using the proxy_pass feature of [NGINX](https://www.nginx.com/) to redirect a sub domain to a url:port address.  First things first I set up a [NGINX](https://www.nginx.com/) docker container, which exposes the template directory to the host.  

I then set up a template that would wait for incoming requests for a domain, which redirects the user to that same domain but with the port, which also happens behind the scenes, and the port is not displayed to the user.

## DNS
Make DNS entries for all sub domains you want to use and point them to the NGINX container  
  
In my case I use [pi-hole](https://pi-hole.net/) for DNS so it was pretty straight forward to add an entry.  Most, if not all, routers should also support custom DNS entries.

## Configuration
This is a sample template that is in line with what I used.  
```
server { 
    servername app1.example.com;
    location / {
      proxy_pass https://app1.example.com:8080;
    }
}
server { 
    servername app2.example.com;
    location / {
      proxy_pass https://app2.example.com:8081;
    }
}
```