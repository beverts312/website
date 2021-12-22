---
title: VPC
type: docs
---

## Concepts

* Internet Gateway (IGW) - An internet gateway is a horizontally scaled, redundant, and highly available VPC component that allows communication between instances in your VPC and the internet. It therefore imposes no availability risks or bandwidth constraints on your network traffic. Only one internet gateway can exist per VPC
* Virtual Private Gateways - Allows you to peer your local network with a VPC
* Egress-Only Internet Gateway - Prevents IPv6 based internet resources from connecting into a VPC while allowing IPv6 traffic to the internet
* Route Tables - A route table contains a set of rules, called routes, that are used to determine where network traffic from your subnet or gateway is directed.
* Network ACL
    * Default ACL comes with each VPC and allows all inboud and outbound traffic
    * Custom ACL's deny all inboud and outbound traffic by default
    * Each subnet must be associated with an ACL, if one is not explicitly attatched the default ACL is applied
    * ACL's allow you to block IP Addresses
    * A single ACL can be attatched to multiple subnets
    * Each rule is numbered, rules are evaluated in order
    * Inbound and Outbound rules are separate
* Subnets
    * A single subnet cannot span multiple AZ's
    * A public subnet always has atleast one route in its table that uses an IGW
    * AWS reserves the first 4 and the last IP for each subnet's CIDR block
* Security Groups
    * All inbound traffic is blocked by default
    * All outbound traffic is allowed by default
    * Changes take effect immediatley
    * Unique to each VPC
    * multiple groups can be assigned to a single instance
    * multiple instances can be assigned to a single group
    * Can specify allow rules but not deny rules
* NAT Instances - provide internet access
    * Must be in public subnet
    * Disable source/destination check on the instance
    * Must be route to private subnet for instances there to be able to use it
    * If there is a bottleneck consider making the instance larger
    * Can be HA if it is in an Autoscaling Group and failover is scripted
    * Uses security groups
    * Cannot be used as a bastion
* NAT Gateways - provide internet access
    * Redundant within a single AZ
    * 5Gbps to 45Gbps
    * Does not use security groups
    * No need to patch or disable source/destination checks
    * Automatically gets public IP
    * If using multiple AZ's put a NAT Gateway in each AZ with appropriate routing to ensure availability
* Flow Logs
    * Log traffic within a VPC
    * Cannot enable flow logs for peered VPC's unless those VPC's are in your acconut
    * Flow logs cannot be tagged
    * Internal DNS Traffic is not logged
    * Traffic generated for windows license validation is not logged
    * Traffic to/from 169.254.169.254 is not logged
    * DHCP Traffic is not logged
    * Can be generated at the network interface, subnet, and VPC levels
* VPC Endpoints - allows traffic to AWS services to stay within AWS. Endpoints are virtual, horizontally scaled, and highly available
    * Interface Endpoint - API Gateway, Cloudformation, Cloudwatch, CodeBuild, Config, EC2 API, ELB API, Kenisis, KMS, SageMaker, Secrets Manager, STS, Service Catalog, SNS, SQS, Systems Manager, Endpoints in another AWS account
    * Gateway Endpoints - DynamoDB, S3

## Facts

* No Transitive Peering
* Security Groups are stateful, Network ACL's are stateless
* When creating a custom VPC a Route Table, ACL, and Security Group are all automatically created
* A VPN connection consits of a customer gateway and a virtual private gateway
* By design Amazon DNS ignores requests coming from outside a VPC

## Useful Links

* [VPCs and Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)
* [NAT Instances](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_NAT_Instance.html)
* [Ephemeral Ports](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html#nacl-ephemeral-ports)