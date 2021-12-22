---
title: Firewall
type: docs
---

## General
On most distributions these runs need to be run as root. Remember that there should be multiple layers of protection between your app and the internet and you may need to adjust the configuration of other layers of defense to allow traffic through.  

## Centos/RHEL 7  

- Install firewalld - `yum install firewalld`  
- Enable firewalld - `systemctl enable firewalld`
- Start firewalld - `systemctl start firewalld`
- Check current rules - `firewall-cmd --list-all`  
- Open port - `firewall-cmd --zone=public --add-port=[number]/[protocol] --permanent && firewall-cmd --reload`

## Ubuntu  

- Enable/Disable Firewall - `ufw [enable/disable]`
- Open/Close port - `ufw [allow/deny] [port]/[protocol]`
- Allow/Deny from a specific IP - `ufw [allow/deny] [ip]`
- Allow/Deny a specific service - `ufw [allow/deny] [service-name]`