---
layout: post
title: PXE server with multiple Linux distributions
date:
---
  
## Scenario  
I like to try out new OSs from time to time, and I also like to wipe and reload pretty often.  The most annoying thing to me is finding a thumb drive to wipe and then the time it takes to get it loaded, then I can start my install.  This allows me to load those same install to a "server" where I can boot the install from the network and do my install.  
  
I did this on a Raspberry Pi running Raspbian.  It should be useful for almost any Debian based distro.
  
  
## Steps
First, we need a tftp server to serve up our images.  
``sudo apt install tfptd-hpa``  
  
Once that is installed, we need to move our distributions into **/srv/tftp**.  What you want are the netboot installations for your distro.  In my case I was using Ubuntu and CentOS. This use Ubuntu in the example.  The available images can be found [here](http://cdimage.ubuntu.com/netboot/).  
  
``wget http://archive.ubuntu.com/ubuntu/dists/bionic-updates/main/installer-amd64/current/images/netboot/netboot.tar.gz``  
``tar -xvf netboot.tar.gz``  
``sudo mv netboot/ubuntu-installer /srv/tftp/ubuntu``  
``sudo cd /srv/tftp/ubuntu/amd64/boot-screens``  
``sudo cp *.c32 /srv/tftp``  
``sudo cp *.cfg /srv/tftp``
``sudo cd /srv/tftp/ubuntu/amd64``
``sudo cp -R *.cfg``  
``sudo cp pxelinux.0 /srv/tftp/``  
