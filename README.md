<p align="center"><img src=logo.jpeg width="300"></p><br>

How to connect to usask-secure on 

 - OpenBSD
 - NetBSD 
 - FreeBSD
 - Solaris
 - Linux

# OpenBSD configuration

## Pre-installation setup

Assuming you already have drivers installed and have previously connected to a known working wifi network. 

Installed needed packages

    pkg_add wpa_supplicant
    
On OpenBSD
````
doas rcctl enable wpa_supplicant
doas rcctl start wpa_supplicant
````

## Configure /etc/wpa_supplicant.conf

### edit wpa_supplicant

Modify file to reflect your authorized user configuration
````
ctrl_interface=/var/run/wpa_supplicant
ctrl_interface_group=wheel
ap_scan=0

network={
    ssid="uofs-secure"
    key_mgmt=WPA-EAP
    pairwise=CCMP
    group=CCMP
    eap=PEAP
    identity="YOURNSID"
    password="YOURPASSWORD"
    phase2="auth=MSCHAPV2"
}

````
 - save config

### Modify your auto connect /etc/hostname.iwm0

Naming depends heavily on your wifi driver and card. Should be hostname.DRIVER

    join homenetwork wpakey homepass
    join uofs-secure wpa wpaakms 802.1x
    inet autoconf

 - save config
````
    doas reboot
````
Should work upon reboot or 

    sh /etc/netstart iwm0
   
Inquire if any issues.

