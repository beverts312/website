---
title: Cloudfront
type: docs
---

## Concepts

* Edge Location - Location where the content will be cached
* Origin - Where the files to distribute come from (S3, EC2, ELB, Route53)
* Distribution - Consists of a set of edge locations
* RTMP - Used for Media Streaming

## Facts

* Edge locations are read/write
* Objects are cached for their TTL
* Clearing cached objects incurs a cost

## Useful Links

* [CloudFront Key Features](https://aws.amazon.com/cloudfront/features/)
