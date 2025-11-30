---
title : "Application Load Balancer"
date: "2024-01-01"
weight : 2
chapter : false
pre : " <b> 1.4.2 </b> "
---

Kiến trúc bao gồm một Application Load Balancer (ALB) với listener trên port 80 và một target group với hai IP-based targets

1. Listener (Port 80)

Nhận các HTTP requests đến từ người dùng

Chuyển tiếp requests đến target group

![listener](/images/1-ECS-Fargate-Microservices/1.4-Resources/listener.png)

2. Target Group (IP Targets)

Chứa hai targets được xác định bằng địa chỉ IP

Cung cấp tính linh hoạt để đăng ký bất kỳ endpoint nào có thể truy cập qua mạng

![target](/images/1-ECS-Fargate-Microservices/1.4-Resources/target.png)

Luồng traffic:
User → ALB (port 80) → Target Group → Targets (IP)