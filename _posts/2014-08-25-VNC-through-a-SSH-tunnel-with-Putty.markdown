---
layout: post
title: VNC through a SSH tunnel with Putty
date: 2014-08-25
---

**This posts assumes that you already have a SSH tunnel in place.  If you do not, [read this][1] first.**

Once you have an SSH tunnel in place, adding services to the tunnel is very simple.  I prefer tunneling the traffic instead of opening up numerous ports on my router firewall.

## Tools
We are going to need [Putty], and a [VNC] client.  When it comes to [VNC] clients I do not really prefer one over the other.  [This one][2] works fine for me.

Of course, you will also need a working SSH tunnel.

## Setup
Configuring [Putty] and VNC are pretty straight forward.  If you followed the **[SSH Tunnel from Windows][1]** post, then this will be familiar.

### Putty
You should already have your **Host Name (or IP Address)** and **Port** filled under the **Session** category.

![][i1]

To add a service to tunnel through [Putty] we just need to add the port and destination to

> SSH > Tunnels

You can find this in the left pane in [Putty], labeled **Category**.

Here we will need to add a **Source port**, which can be whatever you want.  Then a **Destination** which will need to be the internal IP address or hostname of the client you are trying to reach and the port your [VNC] server is listening on.  In most cases the default port is **5900**.  If you changed the server to listen on a different port, you will need to adjust that here.

![][i2]

Last thing for [Putty] is to make sure that the **Local** radio button is selected, select **Add** and then select **Open**.  You should now be asked to log in to your SSH server with your credentials.  You will need to do this before connecting over [VNC].

### VNC Client
Next we need to establish our connection to our VNC server.  Open your [VNC] viewer of choice and for the [VNC] server address you will enter **localhost:8081**, substiture **8081** for whatever port you used while configuring [Putty].

![][i3]

Now connect.

That should get you prompted for your [VNC] password, if you have one, and allow you to manage your workstation remotely through a SSH tunnel.  

### Conclusion
All of this traffic is encrypted and no additional ports were required to be opened on your router's firewall.


[Putty]:http://www.chiark.greenend.org.uk/~sgtatham/putty/
[VNC]:http://en.wikipedia.org/wiki/Virtual_Network_Computing

[1]:http://tech.brookins.info/ssh_tunnel_from_windows
[2]:http://www.realvnc.com

[i1]:https://ux5psg-sn3302.files.1drv.com/y2pNkYDxHRG0Z50Z0N0gowvjv8LXp8JfUTa-ARophWSXuzT19ChmCXFWU4LTWNSt72Pjk3D0bCqmtlUpJ6lK6N8vfxC3QzPcfAk4Yzc378MUo4/vnc_through_ssh_tunnel_w_putty_putty1.png
[i2]:https://ux5psg-sn3302.files.1drv.com/y2pozWxZ3M8fbTRfDTOdCdTpmJ39MNXsa75HK_oPhOfV-1TyinqUPpGTTmZyqXBbuD7Ila1Ty6z9XZsxHCA3HbJCvvhQUkTWvjxMYhJ3bUk0KA/vnc_through_SSH_tunnel_w_putty_putty2.PNG
[i3]:https://ux5qsg-sn3302.files.1drv.com/y2pOG9iS-Yko4z55bG2fZ8hKW8Dhk8TZJBG7BdPGeMveWfZOgwZ2Qrx_RYbsQnNisQNYMfVv-H9jPDkx8Y42q1unccVyU33EWqUAsbalh56ExI/vnc_through_SSH_tunnel_w_putty_vnc1.PNG