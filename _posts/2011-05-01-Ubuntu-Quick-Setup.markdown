---
layout: post
title: Ubuntu Quick Setup
date: 2011-05-01
---

One of the most annoying things about reinstalling your operating system is reinstalling all of your applications.  Since I am so against upgrading the OS, I am constantly reinstalling every time a new release of Ubuntu comes out.  I was so tired of having to remember which applications to install that I finally decided to script it.  

I took about an hour out of my day and put together a pretty simple script to automatically set up my repositories, remove default applications that I did not want and install the applications that I have to install every time I reinstall the OS.  

This is the script that I came up with.  
   
 
<pre># Set Colors  
txtbold=$(tput bold) #Bold Text  
txtred=${txtbold}$(tput setaf 1) # Red/Bold Text  
txtrst=$(tput sgr0) #Reset Text  

# Add Mobloquer DEB Repository  
echo "${txtred}Adding Mobloquer Repository${txtrst}"  
sudo add-apt-repository ppa:jre-phoenix/ppa  
gpg --keyserver keyserver.ubuntu.com --recv 9C0042C8  
gpg --export --armor 9C0042C8 | sudo apt-key add -  

# Add Virtualbox Repository  
echo "${txtred}Adding Virtualbox Repository${txtrst}"  
wget -q <a href="http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc" target="_blank">http://download.virtualbox.org/virtualbox/debian/oracle_vbox.asc</a> -O- | sudo apt-key add -  
echo "deb <a href="http://download.virtualbox.org/virtualbox/debian" target="_blank">http://download.virtualbox.org/virtualbox/debian</a> $(lsb_release -sc) contrib" | sudo tee -a /etc/apt/sources.list  

#Add Handbrake Repository  
echo "${txtred}Adding Handbrake Repository${txtrst}"  
sudo add-apt-repository ppa:stebbins/handbrake-releases  
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 816950D8  

# Installation  
echo "${txtred}Updating Ubuntu${txtrst}"  
sudo apt-get -y update && sudo apt-get -y upgrade  
echo "${txtred}Removing Unwanted Applications${txtrst}"  
sudo apt-get -y purge transmission-common gbrainy gnome-games-common gnome-mahjongg aisleriot pitivi  
sudo apt-get -y autoremove  
echo "${txtred}Installing Applications${txtrst}"  
sudo apt-get -y install ubuntu-restricted-extras vlc openshot filezilla gtk-recordmydesktop keepassx ssvnc inkscape gimp gimp-data-extras agave scribus cheese conduit anjuta glade-gnome moblock blockcontrol mobloquer deluge moonlight-plugin-mozilla ffmpeg easytag virtualbox-4.0 handbrake-gtk libdvdread4  

#Install DVD Decryption  
echo "${txtred}Installing DVD Decryption${txtrst}"  
sudo /usr/share/doc/libdvdread4/install-css.sh</pre>  

Copy the above to a new file with the .sh extension.   
Add executable permissions  
`chmod +x filename.sh`  
  
Now run it.  
`filename.sh`
  
This script makes it simple to add and remove applications.  You can install additional applications by editing line twenty nine.  You can remove additional applications by editing line twenty six.  This was thrown together quickly, and could easily be better.  If anyone has any suggestions on how to make this better, leave them in the comments.
