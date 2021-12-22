---
date: 2020-08-30
title: "Configure Amazon Inspector using Cloudformation"
author: Bailey Everts
---

### What is Amazon Inspector?
[Amazon Inspector](https://aws.amazon.com/inspector/) is an AWS service which analyzes EC2 instances for known vulnerabilities and other issues.

There are 4 predefined rule packages, my template opts to use all of them:
* [Common Vulnerabilities and Exposures](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cves.html)
* [Center for Internet Security Benchmarks](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_cis.html)
* [Network Reachability](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_network-reachability.html)
* [Security Best Practices](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_security-best-practices.html)

To take full advantage of Amazon Inspector you will also want to be sure to install [Amazon Inspector agents](https://docs.aws.amazon.com/inspector/latest/userguide/inspector_agents.html), this post does not cover that.

### How can I use Cloudformation to deploy and configure Amazon Inspector?

If you dont care about whats going on inside, no need to read any further simply deploy this template out of my s3 bucket: `https://beverts-templates.s3-us-west-2.amazonaws.com/inspector.yml`. It will configure inspector to run once a day against the configured targets using all 4 rule packages. It takes 4 parameters:
* TagKey - tag key to match ec2 instances on
* TagValue - tag value to match ec2 instances on
* ResourceNamePrefix - used in naming of created resources
* SubscriptionEmailAddress - email address to send scan findings to

It is very straightforward to write a template that deploys the all the Inspector and SNS components that will be used to define the scan parameters and sns topic/subscription. The problem is that (at time of writing) [AWS::Inspector::AssessmentTemplate](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-resource-inspector-assessmenttemplate.html) does not have parameters for configuring the run schedule or the notification topic (although these is easily achieved in the UI).

In order to resolve this we will make 2 lambdas:
* [InspectorConfigureFunction](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L134) - This uses the inspector api to configure notifications to an SNS topic created by the template. This lambda will be invoked by [this custom function](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L127) when the template is deployed in order to configure the subscription
* [InspectorRunFunction](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L183) - This uses the inspector api to kick off a scan, it will be invoked once daily by [this event rule](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L237)

![](https://app.lucidchart.com/publicSegments/view/fa322f67-9174-4b84-b570-790336a93e88/image.png)

These are the inspector resources which get deployed:
* [InspectorTarget](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L72) - holds the group
* [InspectorGroup](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L78) - this is what is used to group the ec2 instances. All instances that have the tag key/value specified in the parameters will be added to the group
* [InspectorTemplate](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L85) - this is the main inspector resource that gets created, it ties together the group and the rule packages.

These are the SNS resources which get deployed:
* [InspectorTopic](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L97) - SNS topic for scan findings to be posted to
* [InspectorSubscription](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L103) - Subscribes to the topic, the email address passed in as a parameter will automatically be subscribed to the topic

### My tagging strategy is complex, this template wont satisfy my needs

No problem! This template can be easily extended to support a specific tag combination. First create another parameter like [TagKey](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L5) and another parameter like [TagValue](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L10). You could name them `TagKey2` and `TagValue2`

Then add references to your new parameters in the [ResourceGroupTags](https://github.com/beverts312/dev-env/blob/master/aws/templates/inspector.yml#L81) array just like the entry that is already there.

Upload the new template to your bucket and you should be good to go!

### I want to make this part of my deploy
Nested stacks are a great strategy for keeping your templates modular and this template can be easily be included (one or more times) as a nested stack. Nested stacks can be achieved by using the [AWS::CloudFormation::Stack](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/aws-properties-stack.html) resource type.