---
layout: post
title: SSH Tunnel from Windows
date: 2014-08-22
---

This is something I have been doing for a while in place of [VPN] (Virtual Private Network).  I didn't want to go through the headache of setting up a [VPN] server and having to worry about a [VPN] client.  In my case I mainly send web traffic through, so this is a much simpler way to achieve that goal.

## Tools
First thing you need is a server/workstation that you can tunnel into.  This requires some SSH server software.  I was already set up and ready to go.  I currently run about four [Ubuntu] servers and a [Debian] workstation that all run [OpenSSH] server.  If you read this article and thought I would be using Windows from both ends, you were wrong.  But just in case, [freeSSHd] is a good [SSH] server for Windows.

Next you will need to set up [Dynamic DNS][4] or have a static IP address for your home.  I did not have an option for a static address so I am using [Dynamic DNS][4] with [no-ip].

You will also need a [SSH] client.  [Putty] is my choice.  Others can be found [here][1].  [Putty] is my choice mainly because it is easy, small and doesn't require an install.  It was the first client I found, the one I see the most and I have not come across another that has convinced me to leave it behind.

Lastly, for this setup you will need a browser.  This example will user [Firefox].

## Setup
Next we need to set some things up.  First, I need to allow [SSH] traffic into my network.  I will do this on my router.  This step can be different depending on your router, but should be similar enough to get done with these instructions.

### Router
I use a [RaspberryPi][2] running [IPFire] as [my router][6].  Unless you have the same setup this will be a bit different for you.  [Portforward.com][3] may be helpful if you are not sure how to forward a port on your router.

The goal here is to foward certain traffic from the outside to your [SSH] server internally.  It is not a good idea to use the default [SSH] port **(22)** externally.   I suggest picking something out of the ordinary **(ex. 9991)**.  With the port forwarded, external users will hit port 9991 and be directed to your internal host on 22.  That way anyone scanning you externally for known ports will not pick up [SSH].

To create a forward in IPFire I will need to go to

> Firewall > Firewall Rules > New Rule

For the source, I will allow **Any**.  I will enable **Destination NAT (Port forwarding)**.  My firewall interface is 'RED' and new source IP Address will be 'GREEN'.  My destination is my [SSH] servers internal IP **(10.1.1.3)**.  The protocol is TCP, destination port is 22 and External port for this example is **9991**.  I will use the additional settings to set a remark, active the rule and log traffic that uses this rule.  I will now save these settings.


<iframe src="https://onedrive.live.com/embed?cid=F2573DC0233B5BCF&resid=F2573DC0233B5BCF%2119664&authkey=AOQuZ3GQG_sqprs" width="165" height="128" frameborder="0" scrolling="no"></iframe>

### Dynamic DNS
[Dynamic DNS][4] allows you to use a domain name instead of an IP address, and is also kept up to date when your IP address changes.  There are multiple services that you can use to achieve this, some free, some not.  It is best to see if your router supports [Dynamic DNS][4] and choose a provider from that supported list.

Luckily for me [IPFire] supports numerous services.  You cann access these settings in [IPFire] by going to

> Services > Dynamic DNS

Choose a service from the provided list, enter the hostname you registered with that service, and enter the username/password that you use for the service.

<iframe src="https://onedrive.live.com/embed?cid=F2573DC0233B5BCF&resid=F2573DC0233B5BCF%2119665&authkey=AFrQpiU5rv3EEW8" width="165" height="128" frameborder="0" scrolling="no"></iframe>

*
**If you are new to [Dynamic DNS][4] I would suggest [Namecheap] as a provider.  They have lots of useful [documentation][5] in their knowledgebase.**
*


### Putty
Now we configure [Putty].  In the **Host Name (or IP Address)** field you will enter your dynamic DNS address or static IP.  Enter **9991** in the **Port** field.  At this point you can make a [SSH] connection to your server.  But we want to forward some web traffic.  To do that we need to add the tunnel.

![putty1](https://3mqtfa-sn3302.files.1drv.com/y2pIjLZjyQIVyr2jV94SszPEoQwB_rFRz-aU-ADPqlB0lIS5tN9VATArhdBsX6Czm_vMXa101HnNeg1nbyRG6U8460B3S25ECmR7COtBT0dBkA/ssh_tunnel_from_windows_putty1.png)

Select the plus next to **SSH** from the **Category** pane.  Then select **Tunnels**.  For **Source port** enter **8080**, this actually be whatever you want.  Select the **Dynamic** radio button below the **Destination** field.  Click the **Add** button.

![putty2](https://3mqtfa-sn3302.files.1drv.com/y2p0We8K4-bj-klNYxqs-OZ4EtyR02Zwpr50fIB8Cue5Tyk-zQzJ7m5TRCmtKOaNY_cbuyBL6Xd0zwNonlX-0fp6zjnWLBqiq573BMv3NPfWGM/ssh_tunnel_from_windows_putty2.png)

Now select **Open** and you will probably receive a  warning about the security certificate.  Select **Yes or No** and continue past.  Now you should see a command prompt for your [SSH] server.  Log in using your credentials and now you can minize this window.  Keep in mind that it must stay running at all times to keep the tunnel open.


### Browser
Now the magical part.  Once you have connected to your [SSH] server using [Putty] you need to configure your browser to use this tunnel for traffic.  In this example I am using [Firefox], the location of the proxy settings will be different for each browser.

To set the proxy settings in Firefox you will go to

> Options > Network > Settings

![][i3]

Select the **Manual proxy configuration** radio button.  For **SOCKS Host:** enter localhost, for **Port** enter **8080** and then select the box for **Remote DNS**.  

![][i4]

## Conclusion
That is then end.  This can be extended into all types of things, and can tunnel all kinds of different traffic.  I have used tunneling for HTTP, VNC and even tunneled my VMWare Esxi client.  This is a great alternative to VPN as it is fast, reliable and secure.



[OpenSSH]:http://www.openssh.com/
[freeSSHd]:http://www.freesshd.com/?ctt=download
[VPN]:https://en.wikipedia.org/wiki/Virtual_Private_Network
[SSH]:https://en.wikipedia.org/wiki/Secure_Shell
[Ubuntu]:http://ubuntu.com
[Debian]:http://debian.org
[Putty]:http://www.putty.org
[IPFire]:http://ipfire.org
[no-ip]:http://noip.com
[namecheap]:http://namecheap.com
[Firefox]:http://mozilla.org/firefox

[1]:https://en.wikipedia.org/wiki/Comparison_of_SSH_clients#Platform
[2]:http://www.raspberrypi.org/
[3]:http://portforward.com/english/routers/port_forwarding/routerindex.htm
[4]:https://en.wikipedia.org/wiki/Dynamic_DNS
[5]:https://www.namecheap.com/support/knowledgebase/category.aspx/11/dynamic-dns
[6]:http://tech.brookins.info/Raspi_Router_

[i1]:https://3mqtfa-sn3302.files.1drv.com/y2pm2ZeztrG-grB0nta5SviG04pF_ZaEi7XQj3xaUpr2yB3OInUA6Dp4SuaWZNHLQQygZXEIyqBcHgTejdE2UJGabixTsQIx-TAqqgc-4h5caQ/ssh_tunnel_from_windows_router1.png
[i2]:https://3mqtfa-sn3302.files.1drv.com/y2pdn_SXaIKT_fEkSEtuROZhc0ti1QvYW0kba7g-VgTf0wAH1ng6ogENgbua7lvUGLhfRjjPoGdqYadI66s8Z38OH_czLZlMFXKFe19H9Pvpss/ssh_tunnel_from_windows_router2.png
[i3]:https://3mqtfa-sn3302.files.1drv.com/y2pIeHA5ZRPNPWTDgNy6nlZKGmxWGoP57ohNjitMeAMwVJ1_KK17cDzDas52hOaD1nBqoLpddlY3HaQ4qJ2vLIaRWkJbZZbfZJMNYUy4HRxldg/ssh_tunnel_from_windows_browser1.png
[i4]:https://3mqtfa-sn3302.files.1drv.com/y2p7V_5hKa_RYpZr-fEcSCbBgVjmcrRsDRbRvxytR6nXhWEJOmygjSPYpPCCz6wHGqhZ37fbbrld8kRptGpWDFC4w9MU1wxpYIRABVs211pLVQ/ssh_tunnel_from_windows_browser2.png
