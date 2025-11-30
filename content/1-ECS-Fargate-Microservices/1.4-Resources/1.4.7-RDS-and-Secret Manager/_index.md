---
title : "RDS, Secret Manager"
date: "2024-01-01"
weight : 7
chapter : false
pre : " <b> 1.4.7 </b> "
---

When you search for RDS in the AWS Management Console, you can see that an RDS instance has already been created

![rds](/images/1-ECS-Fargate-Microservices/1.4-Resources/rds.png)

To enhance security, the project uses AWS Secrets Manager to store the RDS credentials

![secret](/images/1-ECS-Fargate-Microservices/1.4-Resources/secret.png)

By using Terraform, the RDS instance and its credentials are defined as code, which means sensitive information like database passwords is not hardcoded anywhere in the application or task definitions

* Terraform provisions the RDS instance, the Secrets Manager secret, and links them automatically to ECS tasks or other applications

* Secrets Manager can automatically rotate credentials, reducing the risk of compromised passwords

* ECS tasks can securely retrieve credentials at runtime without exposing them

This approach ensures that your database credentials are protected, managed, and securely accessed, while keeping the infrastructure fully automated and reproducible