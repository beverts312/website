---
title: EC2
type: docs
---

## Instance Types

* Field Programmable Gate Array (F1) - Genomics research, financial analytics, video processing, big data
* High Speed Storage (I3) - NoSql DB's, Data warehousing
* Graphics Intensive (G3) -  Video Encoding, 3D Application Streaming
* High Disk Throughput (H1) - Map Reduce based workloads, distributed file systems
* Low cost, General Purpose (T3) - Web Servers, small DB's
* Dense Storage (D2) - File servers, Data warehousing, hadoop
* Memory Optimized (R5) - Memory Intensive Apps/DB's
* General Purpose (M5) - Application Servers
* Compute Optimized (C5) - CPU Intensive Apps/DB's
* Arm-based (A1) - Scale-out workloads

## Pricing

* On Demand - Fixed rate, no commitment
* Reserved - Capacity reservation and discount with upfront commitment of 1 or 3 years
* Spot - Bid for a price you want to pay. If terminated by Amazon you will not be charged for a partial hour of usage.
* Dedicated - Physical EC2 server dedicated for your use

## Placement Groups

* Clustered - Low latency/High Throughput, single az
* Spread - Individual Critical, can be multi az
* Partitioned - Multiple EC2 Iinstnaces, can be multi az
* Name must be unique for your account
* Not all types can be in placement groups
* Cant move an existing instance into a placement group

## Facts

* Termination protection is off by default
* Instance Store Volumes are ephemeral
* Retrieve metadata for an instance with `curl http://169.254.169.254/latest/meta-data/`
* Retrieve user data for an instance with `curl http://169.254.169.254/latest/user-data/`
* When a dedicated host is stopped you can switch it between "dedicated" (single-tenant hardware) and "host" (isolated server), but not back to "default " (shared hardware)

## Storage

### EBS

Elastic Block Store (for most EC2 workloads).

#### Types

* General Purpose SSD (gp2) - Most work loads
* Provisioned IOPS SSD (io2) - Databases
* Throughput Optimized HDD (s1) - Big Data/Data Warehouses
* Cold HDD (sc1) - File Servers
* EBS Magnetic (Standard) - Infrequently accessed data

#### Facts

* Root EBS volumes can be encrypted (so can other volumes)
* EBS Snapshots exist on S3
* EBS Snapshots are incremental
* Snapshots should not be taken of a root volume when an instance is running
* EBS volume sizes can be changed on the fly
* EBS Volumes will always be in the same AZ as the instance they are attached to
* By default the root EBS volume is destroyed if an instance is terminated

### EFS

Elastic File Store (super scalable NFS).

* Supports the NFSv4 protocol
* Does not require pre-provisioing
* Can scale to petabytes
* Can support thousands of concurrent connections
* Provides read after write consistency

## Useful Links

* [Instance Metadata and User Data](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-metadata.html)
* [EC2 Instnace Lifecycle](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ec2-instance-lifecycle.html)