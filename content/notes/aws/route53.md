---
title: Route 53
description: DNS Services
type: docs
---

## Routing Policies

* Simple - No health checks
* Weighted - Split requests by %, supports health checks
* Latency - Sends traffic to region with lowest latency
* Failover - Active/Passive Routing

## Common DNS Types

* Start of authority record (SOA) - Specifies authoritative information about a DNS zone, including the primary name server, the email of the domain administrator, the domain serial number, and several timers relating to refreshing the zone.
* Nameserver (NS) - Delegates a DNS zone to use the given authoritative name servers
* Address (A) - IP address to direct traffic to
* Canonical Name (CNAMES) - Alias of one name to another
* Mail Exchange (MX) - Maps a domain name to a list of message transfer agents
* PTR - Pointer to a canonical name

## Facts

* You can register domains on AWS
* Sometimes it can take days to register a new domain name
* You can integrate SNS to be notified of health check failures
* Health checks can be applied to individual record sets
* Given the choice always choose an alias record over a CNAME
