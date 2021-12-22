---
title: ELB
description: Elastic Load Balancer
type: docs
---

## Concepts

* [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/introduction.html) - Layer 7, can route based off application needs.
* [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/introduction.html) - Layer 4, can route based off network information
* [Classic Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/classic/introduction.html) - 

## Facts

* 504 meants the gateway has timed out. This means there is an issue with your application
* The end user's IPv4 address is available in the `X-Forwarder-For` header
* Only given DNS never IP
* With cross zone load balancing you are able to equally distribute load across instances in multiple AZ's, without it you can distribue load evenly between multiple AZ's but not evenly across instances
* Sticky sessions can be configured so one user is always routed to the same instance
* Path patterns allow you to route to instances based off the path of the request

## Useful Links
* [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
