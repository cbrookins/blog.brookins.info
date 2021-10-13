---
layout: post
title: Enable Emby over SSL with FreeBSD
date: 2020-03-27
tags: ['emby','freebsd']
---

## Scenario  
I run Emby on FreeNAS, inside a jail. This will go over the process I used to create a **self-signed** SSL certificate to use with Emby.  

## Create self-signed SSL certificate  
I pretty much stuck to the FreeBSD documentation for this. That can be found [here](https://www.freebsd.org/doc/handbook/openssl.html)  

First I generate a key  
`openssl genrsa -rand -genkey -out cert.key 2048`  

Then generate the cert, in this case I am making one that is valid for a year  
`openssl req -new -x509 -days 365 -key cert.key -out cert.crt -sha256` 

Now it has to be converted to a pkcs12 format pfx file  
`openssl pkcs12 -export -in cert.crt -inkey cert.key -out newcert.pfx`  

It will ask for a password. You will need to remember this password to use within Emby.  

## Configuring Emby Server  
Now we will use the Emby Server web interface to enter the details of our new certificate. Select **Manage Emby Server**, and move to the **Network** menu item. Scroll down to **Custom SSL certificate path** and enter the path to the new certificate you created. There is also a button you can use to browse for the certificate.  
  
Now enter the certificate password in the **Certificate password** text field.  
  
I would recommend you set **Secure connection mode** to **Preferred,but not required**, to test your new settings, before changing to **Required for all remote connections**  
  
Restart the server.
  
You should now browse to **https://**[server_name_or_ip]:8920 to verify that the server is up and running on using SSL. If all is good, you can go back to **Secure connection mode** and set it to **Required for all remote connections**.  
  
The certificate will still come back as **insecure** since it is not verified by a third party, but the encryption is all the same.
