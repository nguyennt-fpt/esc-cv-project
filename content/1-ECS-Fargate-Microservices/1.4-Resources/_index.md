---
title : "Resources"
date: "2024-01-01"
weight : 4
chapter : false
pre : " <b> 1.4. </b> "
---

### Resources Created After Provisioning the Infrastructure with Terraform

After running Terraform to set up the infrastructure, the following resources will be created:

1. VPC, Subnets, and Security Groups
The foundational networking components that provide isolated networks, routing, and traffic filtering rules

2. Application Load Balancer (ALB)
Distributes incoming traffic across ECS services to ensure high availability and scalability

3. ECS Cluster
A container orchestration environment where your services will run on AWS Fargate

4. AWS WAF
A web application firewall that helps protect applications from common web exploits

5. VPC Flow Logs and Amazon GuardDuty
Security and monitoring services that analyze network traffic and detect suspicious or malicious activity

6. ECR VPC Endpoints
Private endpoints allowing ECS tasks to pull container images from Amazon ECR securely without using the public internet

7. RDS and Secrets Manager
A managed database instance and securely stored database credentials used by your application