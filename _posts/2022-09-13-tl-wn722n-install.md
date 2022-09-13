---
layout: post
title: "TL-WN722N Installation"
date: 2022-09-13
tags: TL-WN722N
---

## Update system
```bash
sudo apt-get update
sudo apt-get dist-upgrade
sudo apt-get install gcc build-essential linux-headers-generic linux-headers-`uname -r`
```

## Update kernel if needed
Download from <https://www.kernel.org/pub/linux/kernel/projects/backports/stable/v4.4.2/>
```bash
tar xvfz backports-4.4.2-1.tar.gz  
sudo make clean
sudo make
sudo make defconfig-ath9k
sudo make
sudo make install
```

## rc.local
```bash
echo "ath9k" | sudo tee -a /etc/modules
echo "ath9k_htc" | sudo tee -a /etc/modules
sudo gedit /etc/rc.local
```

New contents
```text
# Declare TP-WN727N USB ID to ath9k_htc module
echo "148F 7601" | tee /sys/bus/usb/drivers/ath9k_htc/new_id
```

```bash
sudo update-initramfs -k all -u
sudo update-grub
```

## Wireless list
```bash
iw list
sudo rfkill unblock all
sudo ifconfig wlx8416f911f04b up 10.10.0.1 netmask 255.255.255.0
```

## dhcpd
Edit `/etc/dhcp/dhcpd.conf`
```text
subnet 10.10.0.0 netmask 255.255.255.0 {
    range 10.10.0.2 10.10.0.16;
    option routers 10.10.0.1;
}
```

```bash
sudo service isc-dhcp-server start
```

## hostapd
Edit `/etc/hostapd/hostapd.conf`
```text
interface=wlx8416f911f04b
driver=nl80211
ssid=Rakis
hw_mode=g
channel=6
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=3
wpa_passphrase=1234567890
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
wmm_enabled=1
ieee80211n=1
#ht_capab=[HT40+][SHORT-GI-40]
```
```bash
sudo hostapd /etc/hostapd/hostapd.conf &
```

## References
* [How to install driver for TP-Link TL-WN722N on Ubuntu 14.04?](http://askubuntu.com/questions/512727/how-to-install-driver-for-tp-link-tl-wn722n-on-ubuntu-14-04)
* <https://www.kernel.org/pub/linux/kernel/projects/backports/stable/>
