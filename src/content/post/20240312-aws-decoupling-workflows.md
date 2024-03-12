---
title: "3/12 Session 1 - AWS: Decoupling Workflows"
publishDate: "12 March 2024"
description: "Study session about decoupling workflows in AWS using ELB, SQS and other services"
tags: ["AWS", "elb", "sqs", "sns", "api gateway"]
---

**Tight Coupling** is when our workflow has one EC2 instance directly communicating with another EC2 instance, such as a frontend instance and a backend instance. With this architecture, if either instance is down it directly affects the other. In contrast, **Loose Coupling** is when a service sits in between, such as an **Elastic Load Balancer (ELB)**, SQS/SNS instance, or an API Gateway. In this architecture, the user-request would hit the ELB first instead of the frontend EC2 instance; the ELB would direct the request to one of many frontend EC2 instances (high availability) and from there it would be sent to a second load balancer. This ELB would direct the request to one of many backend EC2 instances. A key point to remember is that decoupling should happen at every level, such as seen with the frontend and backend instances. We don't want to have a single instance as a failure point for the whole workflow.

In addition to ELB, Simple Queue Service, Simple Notification Service and API Gateways can be used to decouple our workflows. **SQS** is a message queueing service, like the name implies. It uses poll-based messaging, which means a message **producer** writes and sends a message via SQS which a message **consumer** will receive by polling, or requesting, the SQS service. This is an asynchronous process, as the message is sent by the producer, held in a queue by SQS, then requested (via polling) and received by the consumer. Importantly, there are a number of settings that can be configured to change how this process works. Things like a delivery delay, message retention time, polling duration, and visibility timeout will change how the queue service functions. These settings might need to be changed/adjusted from their default values to match your workflow and system requirements. For instance, maybe your EC2 instance takes longer to process the message than the default value and the visibility timeout should be increased.

Other settings to review:

- Delivery Delay
- Message Size
- Encryption
- Message Retention
- Long/Short Polling
- Queue Depth (can be used to trigger auto-scaling)
- Visibility Timeout
- and more to come?

More on SQS and the other decoupling services later.
