---
title: SQS
description: Simple Queue Service
type: docs
---

## Facts

* Pull based
* Messages are 256KB
* Messages can be in the queue from 1 minute to 14 days, default retention is 4 days
* Visibility Time Out - the amount of time the message will be invisible after it is picked up. If the job is finished before the visibility timeout expires, it is removed from the queue, otherwise it is made visible again. Default is 12 hours
* Guarantees messages will be processed atleast once

## Useful Links
* [How SQS Works](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-how-it-works.html)