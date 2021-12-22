---
title: Databases
type: docs
---

## RDS

* Read Replicas are for performance
* Multi-AZ is for DR
* SQL, MySQL, PostgreSQL, Oracle, Aurora, MariaDB
* Runs on VM's but you do not have OS level access to them
* Patched by Amazon
* Not serverless (except for Aurora Serverless)
* Encryption at rest is supported
* SQL Server and Oracle can have a maximum of 2 databases per instance
* Aurora
    * 2 copies of the data is stored in each AZ at a minimum of 3 AZ's
    * Snapshots can be shared across accounts
    * Automated backups turned on by default

## DynamoDB

* No SQL
* Uses SSDs
* Spread accross 3 geographically distinct data centers
* Eventual consistent reads by default but strongly consistent reads can be enabled (for a cost).
* Name and value combined cannot exceed 400kb 

## Elasticache

* Memcached (caching)
* Redis (caching + pub/sub)

## Redshift

* For Business Inelligence or Data Warehousing
* Only available in 1 AZ
* Can restore snapshots to new AZs if there is an outage
* Can retain backups for a maximum of 35 days

## Useful Links

* [Key Value DB's](https://aws.amazon.com/nosql/key-value/)
* [Databases](https://aws.amazon.com/products/databases/)
* [ElastiCache](https://aws.amazon.com/elasticache/)