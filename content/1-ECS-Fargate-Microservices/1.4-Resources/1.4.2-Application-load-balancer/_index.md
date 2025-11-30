---
title : "Application Load Balancer"
date: "2024-01-01"
weight : 2
chapter : false
pre : " <b> 1.4.2 </b> "
---

The architecture includes an Application Load Balancer (ALB) with a listener on port 80 and a target group with two IP-based targets

1. Listener (Port 80)

Receives incoming HTTP requests from users

Forwards requests to the target group

![listener](/images/1-ECS-Fargate-Microservices/1.4-Resources/listener.png)

2. Target Group (IP Targets)

Contains two targets identified by IP addresses

Provides flexibility to register any network-accessible endpoint

![target](/images/1-ECS-Fargate-Microservices/1.4-Resources/target.png)

Traffic flow:
User → ALB (port 80) → Target Group → Targets (IP)

