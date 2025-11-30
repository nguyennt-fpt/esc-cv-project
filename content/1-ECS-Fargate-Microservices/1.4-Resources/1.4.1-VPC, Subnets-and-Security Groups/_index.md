---
title : "VPC, Subnets, Security Groups"
date: "2024-01-01"
weight : 1
chapter : false
pre : " <b> 1.4.1 </b> "
---

The architecture consists of one VPC named ecs-fargate-microservices-vpc. Inside this VPC, 6 subnets and 4 security groups are configured to ensure that the application is secure and follows best practices

![vpc](/images/1-ECS-Fargate-Microservices/1.4-Resources/vpc.png)

1. Public Subnets (for the Application Load Balancer)

There are two public subnets, and they are used to host the Application Load Balancer (ALB)

Security Group for the ALB

Inbound rules:

* Allow HTTP (port 80)

* Allow HTTPS (port 443)

These ports allow users to access your website

Egress rules:

* Only the required ports are allowed (in this case, port 3000) based on the least privilege principle

This helps minimize risks such as:

* Data exfiltration – containers sending data outside the network

* Malware communication – connecting to malicious C2 servers

* Lateral movement – accessing internal services that should be restricted

* Compliance violations – breaking security standards
![albsg](/images/1-ECS-Fargate-Microservices/1.4-Resources/albsg.png)

2. Private Subnets (for ECS Tasks)

There are two private subnets where ECS Fargate tasks run

Security Group for ECS Tasks

Inbound rules:

* Only allow traffic from the public ALB security group on port 3000 (container's application port)

Egress rules:

* Allow port 53 (DNS)

* Allow port 443 (HTTPS)

* Allow port 3000 (App)

* Allow port 3306 (MySQl)

These are required for tasks to pull images, connect to AWS APIs, or resolve domain names

![ecssg](/images/1-ECS-Fargate-Microservices/1.4-Resources/ecssg.png)

3. Private Subnets (for RDS Database)

There are two additional private subnets dedicated for the RDS instance

Security Group for RDS

Inbound rules:

* Only allow connections from the ECS task security group, using port 3306 (MySQL port)

No outbound rules: the RDS database does not need internet access, so outbound traffic is blocked for security

![rdssg](/images/1-ECS-Fargate-Microservices/1.4-Resources/rdssg.png)

4. Security Group for the VPC Endpoint (ECR Endpoint)

This security group is attached to the Interface VPC Endpoint used by ECS tasks to pull container images from ECR privately (without internet)

Inbound rules

* Allow HTTPS (443) from the ECS Task Security Group

* This enables ECS tasks to access ECR through PrivateLink

Outbound rules

* No outbound (egress) rule is required

* Leaving egress empty is safe and follows strict least privilege best practice

![endpointsg](/images/1-ECS-Fargate-Microservices/1.4-Resources/endpointsg.png)