---
title : "ECS Cluster"
date: "2024-01-01"
weight : 3
chapter : false
pre : " <b> 1.4.3 </b> "
---

Trên AWS Console, khi chúng ta xem ECS service, chúng ta có thể thấy một cluster
![cluster](/images/1-ECS-Fargate-Microservices/1.4-Resources/cluster.png)

Cluster có một service, hiện đang chạy

Service này dựa trên một task definition, mà bạn có thể xem trong tab Task Definition

Task definition chỉ định mọi thứ cần thiết để chạy containers, như: tích hợp ALB, số lượng tasks mong muốn, auto scaling, rolling updates, v.v.
![taskdf](/images/1-ECS-Fargate-Microservices/1.4-Resources/taskdf.png)

Trong phần Tasks, bạn thấy hai tasks đang chạy. Đây là hai containers chạy web app cho dự án này

Ở đây, desired task count được đặt là 2, vì vậy ECS đảm bảo rằng hai tasks luôn chạy
![task](/images/1-ECS-Fargate-Microservices/1.4-Resources/task.png)