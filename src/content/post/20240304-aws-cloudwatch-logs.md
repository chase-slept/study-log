---
title: "3/4 Session 2 - AWS CloudWatch"
publishDate: "04 March 2024"
description: "Second study session of the day--this one covered CloudWatch and related services"
tags: ["CloudWatch, AWS"]
---
*(posted retroactively on 3/5)*

## What I Learned

CloudWatch is a monitoring service for both AWS services and other applications, on-prem or in the cloud. For services in AWS, many metrics are collected and available by default. For others, an agent must be installed locally and permissions/network routes granted to allow for metrics to be delivered to CloudWatch.

Reports can be generated based on the metrics. AWS-Managed versions of Prometheus and Grafana are available for this as well.

Alarms can be assigned to the metrics. These can be used to further automate and process any events. These can be processed in other services, like SNS (to send email alerts) or Lambda (to trigger scripts/workflows).

## Things to Review/Note

This was a straight-forward lecture, so not much to note here. I'd like to review this topic again later, after labs and hands-on. Some things to do:

- Practice setting up the cloudwatch-agent on an EC2 instance (or any of my random servers)--I took notes on the install procedure on EC2
- Work through the Labs in ACG
- Review the lecture again and take note of any special circumstances mentioned (tracking available memory util?)
