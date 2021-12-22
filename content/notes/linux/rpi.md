---
title: PI Setup Tips
type: docs
---

#### Password

Default is `pi/raspberry`
Use `passwd` to change

#### Keyboard

Default is brittish, we gotta fix that shit
 * `sudo dpkg-reconfigure keyboard-configuration` hit enter on the first screen, then `other`, and `English (US)`

#### Wifi

Configure - `/etc/wpa_supplicant/wpa_supplicant.conf`

```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
ssid="NETWORK NAME"
psk="NETWORK PASSWORD"
}
```

Also Configure - `/etc/network/interfaces`

```
source-directory /etc/network/interfaces.d

auto wlan0
allow-hotplug wlan0
iface wlan0 inet manual
wpa-roam /etc/wpa_supplicant/wpa_supplicant.conf
```

#### Raspotify
Allows you to use your raspberry pi as a spotify connect client

* Install `curl -sL https://dtcooper.github.io/raspotify/install.sh | sh`
* Configure `/etc/default/raspotify`