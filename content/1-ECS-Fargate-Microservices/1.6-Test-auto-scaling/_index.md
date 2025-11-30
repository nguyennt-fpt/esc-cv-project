---
title : "Testing auto scaling"
date: "2024-01-01"
weight : 6
chapter : false
pre : " <b> 1.6. </b> "
---

Testing ECS Service Auto Scaling

Next, we will update the ECS service to verify that auto scaling is working correctly

In this architecture, the ECS Service is already configured with Auto Scaling using Terraform.

However, to make testing more convenient, i will add an additional third policy
This extra policy can be used to trigger scaling actions more aggressively or under different conditions, making it easier to observe and validate Auto Scaling behavior during load tests or demonstrations

Go to ECS → ecs-fargate-microservices-cluster → select Update service

In the Service Auto Scaling section, click Add more scaling policy

Create a new scaling policy using the following settings:

* Metric: ALBRequestCountPerTarget

* Target value: 50

* Scale-out cooldown: 60 seconds

* Scale-in cooldown: 300 seconds

These values make it easier to trigger scaling events for testing purposes

![auto](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/auto.png)

To generate traffic, use a load-testing tool such as Apache Bench (ab)
Run the command: ab -n 10000 -c 20 your-domain-name

* -n 10000: total number of requests

* -c 20: number of concurrent requests

![ab](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/ab.png)


After a short period, CloudWatch will detect increased load and trigger an alarm

![inalarm](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/inalarm.png)

Once the scaling policy activates, the number of running tasks will automatically increase

In this test, the service scaled from 2 tasks to 4 tasks

This confirms that the auto scaling configuration is working as expected

![scale](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/scale.png)