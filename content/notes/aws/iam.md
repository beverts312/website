---
title: IAM
description: Identity and Access Management
type: docs
---

## Concepts

* Users
* Groups - Can be used to organize users and their permissions
* Roles - Used for AWS resources to authenticate with each other. Access/Secret Keys should never be used by AWS resources.
* Policies - JSON Document describing what resources can be accessed and in what capacity

## Facts

* Global not regional
* Users have no permissions when created
* Root account is the account used when creating the organization, it should be secured and then not used