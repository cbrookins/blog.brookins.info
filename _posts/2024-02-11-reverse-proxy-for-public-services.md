---
bg: "script.gif"
layout: post
title: NGINX reverse proxy for public services
date: 2024-02-11
tags: ['docker','ubuntu','nginx','cloudflare','raspberry-pi','ddns-updater']
---

I run a few services inside my homelab, and most of those services have no business on the internet.  I recently set up a couple that I did want to make available externally.  I knew I didn't want to just open up a port directly to the service, and my tailnet would not do the trick for these particular services.  Reverse proxy is where I landed.  This way I can open port 443 and serve all of the services I need.

## Cloudflare
I used a few [**Cloudflare**](https://cloudflare.com) free services to accomplish this project.  

I started by creating and downloading an **Origin Server** certificate.  This will be needed to verify my service with Cloudflare.  

I also randomly generated some urls to use for the services, they will be publicly available, but I still dont want them obvious. I made the DNS entries for them and used Cloudflares DNS proxy option to hide the destination address.

## Nginx
I went with **NGINX** because I was [already familiar with it](https://blog.brookins.info/NGINX-proxy-for-Docker/).  I am currently running it in a docker container on a Raspberry Pi 4.  

I mounted the **Cloudflare** origin server certificate and key from the host to **/cert.pem** and **/cert.key** inside the NGINX container.  This is required if you are using Full end to end encryption with **Cloudflare**.  

### Example Docker compose file
```
services:
    web:
        container_name: nginx
        image: nginx:latest
        volumes:
            - ./nginx/templates:/etc/nginx/templates
            - /etc/ssl/cert.pem:/cert.pem
            - /etc/ssl/key.pem:/key.pem
        ports:
            - "80:80"
            - "443:443"
        restart: unless-stopped
```

### Example NGINX template
```
server {
    server_name npzri.domain.com;
    listen 443 ssl;
    ssl_certificate /cert.pem;
    ssl_certificate_key /key.pem;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_pass http://192.168.1.201:8080;
    }
}

server {
    server_name lnxar.domain.com;
    listen 443 ssl;
    ssl_certificate /cert.pem;
    ssl_certificate_key /key.pem;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_pass https://192.168.1.200:9001;
    }
}
server {
    server_name rziap.domain.com;
    listen 443 ssl;
    ssl_certificate /cert.pem;
    ssl_certificate_key /key.pem;

    location / {
        proxy_set_header Host $host;
        proxy_set_header X-Forwarded-Host $host;
        proxy_set_header X-Forwarded-Server $host;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_pass http://192.168.0.200:30042;
    }
}
```

## ddns-updater
I used the [**ddns-updater**](https://github.com/qdm12/ddns-updater) project in a container to keep the Cloudflare DNS entries up to date if my IP happened to change.  Cloudflare DNS documentation suggests using their **API**, [**ddclient**](https://ddclient.net/) and [**DNS-O-Matic**](https://www.dnsomatic.com/), but I was familiar with this project, and already using it, so I stuck with it and it works pretty nicely.

## Router
On my router I only had to expose port **443** to this Raspberry Pi so that it could serve up the encrypted websites.  I am actually using **Cloudflare** to force everything to **https** so there was no need to expose 80 for any redirects.