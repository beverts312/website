---
date: 2017-03-01
title: "How to easily configure a Route53 domain for use with Office 365"
author: Bailey Everts
---

As an avid user of both O365 and Route53, I am frequently configuring new domains on O365. I quickly got frustrated with the experience so I whipped up a [little script](https://github.com/beverts312/node-aws-utils/blob/master/scripts/route53-on-o365.ts) to make my life easier. To make the the lives of others easier, I recently wrapped it up in my [aws-mgmt-utils](https://www.npmjs.com/package/aws-mgmt-utils) package as a bin.

### Prerequisites:

* A domain in a hosted zone on Route53
* An active O365 Subscription (you can start a trial if you dont have one)
* The aws-cli is installed and configured on your machine
* Node.js & npm

### Steps

1. In a terminal, install my utils - npm install -g aws-mgmt-utils (you may need to be admin)
2. In a browser go to the [O365 Admin Page](https://portal.office.com/adminportal/home#/homepage) and click Add a Domain
3. Enter your domain and click next
4. Copy the TXT Value field (it should look something like MS=ms38863110)
5. In a terminal create/update your TXT record - r53-update-record ${your_domain} TXT ${value_from_4}
6. In  the browser click Verify (you may need to wait a few minutes while DNS propagates)
7. In a terminal update all your other records - r53-o365 ${your_domain}
8. Back in the browser you should now be able to click through the rest of the prompts (again, you may need to wait a few minutes for DNS)


Hope this helps! If you want to check out my node aws utilities further or request new features you can do that on [github here](https://github.com/beverts312/node-aws-utils).