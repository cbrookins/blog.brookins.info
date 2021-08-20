---
layout: post
title: PXE server using a TrueNAS jail
date: 2021-05-04
---

## Scenario
I wanted to test out Linux as a PXE server for reinstalling OSs on my devices at home.  I was tired of messing with USB drives and wanted to be able to PXE boot, choose an OS and go.  Nothing about this requires this be in a TrueNAS jail, these steps should work for anything based on FreeBSD.  It should work on Linux distros also, even though the TFTP package name may be different.

## Configuration
```pkg install tftp-hpa nano```  
```mkdir -p /mnt/tftpd```  
```chmod -R 775 /mnt/tftpd```  

Add the following to **/etc/rc.conf**
```
tftpd_enable="YES"
tftpd_flags="-p -s /mnt/tftpd -B 1024 --ipv4"
```  

#### BIOS setup  
```wget http://archive.ubuntu.com/ubuntu/dists/bionic-updates/main/installer-amd64/current/images/netboot/netboot.tar.gz```  
```tar -xvf netboot.tar.gz```  
```mkdir -p /mnt/tftpd/ubuntu/18.04```  
```sudo mv netboot/ubuntu-installer /mnt/tftpd/ubuntu/18.04```  
```sudo cd /mnt/tftp/ubuntu/18.04/amd64/boot-screens```  
```sudo cp *.c32 /mnt/tftpd```  
```sudo cp *.cfg /mnt/tftpd```  
```sudo cd /mnt/tftpd/ubuntu/18.04/amd64```  
```sudo cp -R *.cfg```  
```sudo cp pxelinux.0 /mnt/tftpd```  

Edit **txt.cfg** to include menu items for you installations  
```
label ubuntu
	menu label ^Ubuntu 18.04 LTS Install
  menu default
	kernel ubuntu/18.04/amd64/linux
	append vga=788 initrd=ubuntu/18.04/amd64/initrd.gz
```

#### UEFI setup  
I ended up using the Fedora files for UEFI since they didn't seem to care where the grub files were located.  It worked out since I also wanted Fedora available over PXE.  

I could not get the Ubuntu grub files to work.  I read that they may have hard coded paths included in them, which doesn't allow you to modify the folder structure.  

```wget https://download.fedoraproject.org/pub/fedora/linux/releases/32/Server/x86_64/os/EFI/BOOT/grub.cfg```  

```wget https://download.fedoraproject.org/pub/fedora/linux/releases/32/Server/x86_64/os/EFI/BOOT/grubx64.efi```  

Move the grub files into the tftp root directory  
```mv grub.* /mnt/tftpd```

Edit **grub.cfg** to include menu entries for your installations  

```
set default="0"
set timeout=60

menuentry "Install Ubuntu 18.04" {
	linux	/ubuntu/18.04/amd64/linux vga=788 
	initrd	/ubuntu/18.04/amd64/initrd.gz
}
grub_platform
if [ "$grub_platform" = "efi" ]; then
menuentry 'Boot from next volume' {
	exit
}
menuentry 'UEFI Firmware Settings' {
	fwsetup
}
```

#### DHCP Server
**Note:** *There is a way to get BIOS and UEFI working at the same time using the DHCP server, but in my case I was using my routers DHCP server and did not have direct access to the configuration to make that happen.*
  
Now you need to set DHCP option 66 and 67  
Option 66 is the server address  
Option 67 will be the path to the boot file you want to use. The path is formatted from the root of the TFTP server.  For this example our file is in the root of the TFTP server so I would enter **grubx64.efi**  

## Conclusion
Now you should be able to boot a workstation and select PXE to boot to your server and select an available install.
