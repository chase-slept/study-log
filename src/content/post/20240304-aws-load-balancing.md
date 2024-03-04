---
title: "3/4 Session 1 - AWS Load Balancing"
publishDate: "04 March 2024"
description: "This study session was about Load Balancing: ALB, NLB, and Classic LB."
tags: ["ALB, NLB, Load Balancing, AWS"]
draft: true
---
## What I learned

**Application Load Balancers** operate on Layer 7 of the OSI model. This means it can perform 'intelligent' routing, which is really just to say we can add rules and priorities (like if/else statements) to our traffic to route it to specific places and depending upon specific conditions. ALBs use a **listener**, which monitors a port/protocol we set and performs routing based on one or more rules we set. The listener sends traffic to a **target group** which contains one or more EC2 Instances.

ALBs can use **path patterns** [which are a lot like Caddy's *handle_path* directive]. Path-Based routing like this allows for requests for example.com to flow to one instance group while requests for example.com/**example_path** flow to a different instance group. This would be useful for serving images/media from a different server than the main example.com web server.

ALBs handle HTTP/HTTPS traffic **ONLY!** For other protocols, a **Network Load Balancer** can be used. NLBs operate at the connection level of the OSI model, Layer 4. This allows for high performance routing--**millions of low-latency requests per second**. Unlike Layer 7, Layer 4 cannot make use of intelligent routing features. All traffic from the listener is sent to the target group, no rules or priority. NLBs can make use of other protocols: TCP, UDP, TCP/UDP, and TLS (for SSL connections). NLBs can use any port within the standard port range.

Lastly, **Classic Load Balancers** are often used for testing and development; they are very easy to deploy and operate at both Layer 4 and Layer 7. They can make use of Sticky Sessions and X-Forwarded headers, to keep track of user sessions and origin IPs. Classic's listeners also uses HTTP/HTTPS. 

## Things to Review/Note

- Sticky Session user errors (such as when an instance is removed while still 'sticky') can be resolved by disabling the feature
- ALB 'sticks' to ALL instances within a target group. To stick to individual instances, use only one instance per group
- 504 errors are not LB-related: troubleshoot the web server or database connections
- if all NLB instances are unhealthy/down, traffic will be routed to ALL instances: this is called 'fail-open'
- Deregistration Delay/Connection Drain are the same, and allow for the connection to stay open when an instance is unhealthy/down. Turn off to immediately close connections when instances fail health-checks

This section was pretty easy to understand because of my time playing with Caddy and other reverse proxies. A lot of similar concepts.