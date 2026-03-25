<p align="center"><img src=logo.jpeg width="300"></p><br>

How to connect to usask-secure (WPA2 Enterprise) on 

 - OpenBSD
 - NetBSD 
 - FreeBSD
 - Solaris
 - Linux

# OpenBSD configuration

## Pre-installation setup

Assuming you already have drivers installed and have previously connected to a known working wifi network. 

Install needed packages
````
    doas pkg_add wpa_supplicant
````
On OpenBSD
````
 doas touch /etc/wpa_supplicant.conf
 doas chmod 600 /etc/wpa_supplicant.conf
 doas rcctl enable wpa_supplicant
 doas rcctl start wpa_supplicant
````

## Configure /etc/wpa_supplicant.conf and hostname.if

### Modify /etc/wpa_supplicant.conf

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

### Modify /etc/hostname.iwm0

Naming depends heavily on your wifi driver and card. Should be hostname.DRIVER

    join homenetwork wpakey homepass
    join uofs-secure wpa wpaakms 802.1x
    inet autoconf

 - save config

### Apply
````
    doas chmod 600 /etc/hostname.if
    doas reboot
````
Should work upon reboot or 
````
    doas sh /etc/netstart iwm0
````
### DONE
Now when you are in range of usask-secure it will auto connect.

Inquire if any issues.

