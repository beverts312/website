---
title: Staying Anonymous
type: docs
---

Proxy, VPN, tor

Note about location: You want to access the servers you are targetting from the same region as the typical user base to blend in  

Commands below may work on other distributions but they assume you are on Kali Linux.  

## Tor  
Shouldnt run as root (`adduser newusername`)  
Download from https://wwww.torproject.org   

Traffic goes through a variety of nodes, at each node another layer of encryption is added.  
After making it through the inner nodes, the exit node makes the actual request.  
Difficult/Impossible to track unless somebody controlled all inner nodes (exteremly unlikely).  

## Proxychains  
Proxychains allows you to route traffic through a series of proxies.
Use dynamic_chain in most cases
Can be HTTP, SOCKS4, or SOCKS5  
Always use SOCKS5  

Add `SOCKS5 127.0.0.1 9050` to the bottom of your /etc/proxychains.conf  
Start tor - `service tor start`  
Verify - `service tor status`  
Verify anonyminity - `proxychains firefox www.dnsleaktest.com` (your IP should be in another country)  

The more free proxies you use the slower things will be, select just a few free proxies with the highest uptime/reviews  

## VPN  
### Change DNS Provider from your ISP
OpenDNS is a good option.  
Replace your `prepend domain-name-servers ....;` line with:  
`prepend domain-name-servers IP1, IP2;`, where IP1/2 are the OpenDNS IP's.  
Restart your network-manager: `service network-manager restart`  
Verify changes: `cat /etc/resolve.conf`, the output should show `nameserver IP1`, `nameserver IP2` as your first 2 lines.  

### Get & Use VPN
1. Download free vpn from a site like VPN Book, note user/password.  
2. Unzip download.  
3. Make sure all browsers are closed. Navigate to unziped folder, run `openvpn vpnprefix-tcp443.ovpn`, vpnprefix will vary based of the package you chose.  
4. Use credentials to login to vpn.  
5. Wait for `Initialization Sequence Complete` message to come up.  
6. Verfiy: Open a browser and go do [DNS Leak Test](www.dnsleaktest.com), verify your location is not your actual location. Click Standart Test and make sure your ISP is not your actual ISP.  

## Mac Addresses  
Mac address doesnt make it past the router.  
Doesn't really matter if you change it on a VM.  

[macchanger](https://github.com/allobs/macchanger) is a great esay to use tool.  

Change mac address everytime you bootup:  
1. Open crontab config: `crontab -e`  
2. Add this line and save: `@reboot macchanger -r eth0`  

