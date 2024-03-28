---
title: "3/28 Session 1 - AWS: Caching"
publishDate: "28 March 2024"
description: "Study session about caching on AWS, including Cloudfront, ElastiCache, DAX, etc."
tags: ["AWS", "elasticache", "cloudfront", "memcached", "redis", "dax"]
---

This lecture covered caching in AWS: Global **external** caching using CloudFront (a CDN service) and **internal** caching using ElastiCache.

CloudFront is a Content Delivery Network; it's used to put our HTTP/HTTPS content in a cache that sits closer to the end-user. These edge locations are spread across the globe and are **not** individually selectable--only per-continent allow/deny rules are available in CloudFront; a WAF would be a better way to shape traffic to this content (such as denying access to a particular region/country, etc.). TTL can be adjusted to fetch new content periodically and the cache can be flushed on-demand as well. Importantly, CloudFront serves via HTTPS by default; this makes it a good solution for serving static content via S3 buckets, since S3 does not secure via SSL by default.

Internal caching can be achieved using a database caching service such as ElastiCache, a managed caching service that uses Memcached and/or Redis in front of your database. **Memcached** is a simple solution that can't be used as a database on its own, doesn't support failover/multi-AZ, and doesn't offer backups; Redis can function as a standalone DB and offers failover/multi-AZ and backups. Both of these can be used with relational databases, whereas DynamoDB Accelerator (DAX) can be used for NoSQL databases. DAX reduces response times for these databases from milliseconds to microseconds, offers granular configuration of the node size, cluster count, TTL, maintenance windows, updates, etc., and is highly available within your specified VPC. Basically, ElastiCache in front of our relational databases and DAX in front of our DynamoDB instances. **Use a cache wherever possible!**

AWS Global Accelerator is a networking service meant for TCP/UDP content (like gaming apps or IoT messaging). It uses multiple Anycast IP addresses to increase performance with IP caching. Accelerators are entry points to the AWS global network infrastructure and route traffic to AWS endpoints. Listeners are used to process the inbound connections using port/protocol information. Endpoints are the AWS resources (ALB, EC2 instances, etc.) that are the ultimate destination of our user-requests. Accelerators are assigned two static Anycast IPv4 addresses (dual-stack are assigned four; two IPv4 and two IPv6) that act as entry points for all traffic. Accelerators can be set as Standard or Custom, with Standard routing traffic using location, health checks or weights and Custom using application logic to route traffic to specific EC2 instances or VPC ports. Either way, GA uses the AWS backbone network and edge locations to increase the speed and performance when compared to routing via the public internet.

## To Do

- Implement a cache for my S3 website (this website, actually)
- Read more about Redis/Memcached
- Look at more architectures that use caches
- Check documentation on Global Accelerator, which seems to be the most complex of these caching services
