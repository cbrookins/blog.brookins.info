---
layout: post
title: Create a custom jail for OpenVPN in FreeNAS
date:
---

## pre-init script
devfs rule -s 4 add path 'tun*' unhide

## packages
pkg install nano transmission-cli transmission-web transmission-daemon mono sonarr openvpn


## rc.conf
openvpn_enable="YES"
openvpn_configfile="/config/openvpn/openvpn.conf"
openvpn_dir="/config/openvpn"
transmission_enable="YES"
transmission_conf_dir="/config/transmission"
transmission_download_dir="/mnt/downloads"
firewall_enabled="YES"
firewall_script="/config/ipfw/ipfw_rules"
sonarr_enable="YES"
sonarr_data_dir="/config/sonarr"
emby_server_enable="YES"


## Sonarr specific
chown -R /usr/local/share/sonarr   <-- startup folder can be found on System > Status in Sonarr
