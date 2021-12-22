---
title: Kinesis
type: docs
---

For Streams

## Types

* Kinesis Streams - Producers send data to shards, where it is available to consumers for between 24hours and 7 days. Typically consumed by an EC2 instance and forwarded to a data store (such as dynamo, s3, emr, or redshift) where it can be processed further
* Kinesis Firehose -  Data must be processed right away, typically sent to elasticsearch, s3, or redshift (via s3)
* Kinesis Analytics - Can be used in cunjunction with streams or firehose, automatically processes data right away