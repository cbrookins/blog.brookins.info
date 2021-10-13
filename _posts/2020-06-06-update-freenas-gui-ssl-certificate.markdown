---
layout: post
title: Update FreeNAS GUI SSL Certificate
date: 2020-06-06
tags: ['truenas']
---

My FreeNAS cert expired.  Pretty sure I have had it since FreeNAS 9.x and it was the one that came with the distro. I figured it was time to update it. I chose to use a self-signed cert.  

## Create self-signed SSL certificate  
I pretty much stuck to the FreeBSD documentation for this.  That can be found [here](https://www.freebsd.org/doc/handbook/openssl.html). This is also what I used for [my Emby setup]({{site.url}}/2020/03/27/Enable-Emby-over-SSL-with-FreeBSD.html), minus a couple of steps.  

First I generate a key  
`openssl genrsa -rand -genkey -out cert.key 2048`  

Then generate the cert, in this case I am making one that is valid for a year  
`openssl req -new -x509 -days 365 -key cert.key -out cert.crt -sha256` 

## Configuring FreeNAS  
Now we will use the FreeNAS web interface to enter the details of our new certificate. Select **System**, and move to the **Certificates** menu item. Select **ADD**.  
  
Now enter a **Identifier** (name) and select **Import Certificate** from the drop down.  
  
Now run the following command and copy the output into the field for **Certificate**  
``cat cert.crt``  

Then run the following command and copy its output into the field for **Private Key**  
``cat cert.crt`` 

If you followed the steps above, you can leave the password blank and select **Save**  

Now head over to **System** and select the **General** menu option.  

Drop down the **GUI SSL Certificate** option and select your newly created cert. It will ask you to restart the web services. You will want to do that.
  
You should now refresh the browser and make sure you are using **https** (**https://**[server_name_or_ip]) to verify that the server is up and running and using the new SSL cert. If all is good, you can select **Web GUI HTTP->HTTPS Redirect**.  
  
The certificate will still come back as **insecure** since it is not verified by a third party, but the encryption is all the same.
