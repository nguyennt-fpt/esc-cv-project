---
title : "ECS Cluster"
date: "2024-01-01"
weight : 3
chapter : false
pre : " <b> 1.4.3 </b> "
---

On the AWS Console, when we view the ECS service, we can see a cluster
![cluster](/images/1-ECS-Fargate-Microservices/1.4-Resources/cluster.png)

The cluster has one service, which is currently running

This service is based on a task definition, which you can view in the Task Definition tab

The task definition specifies everything needed to run the containers, such as: ALB integration, desired number of tasks, auto scaling, rolling updates, etc
![taskdf](/images/1-ECS-Fargate-Microservices/1.4-Resources/taskdf.png)

In the Tasks section, you see the two running tasks. These are the two containers running the web app for this project

Here, the desired task count is set to 2, so ECS ensures that two tasks are always running
![task](/images/1-ECS-Fargate-Microservices/1.4-Resources/task.png)
