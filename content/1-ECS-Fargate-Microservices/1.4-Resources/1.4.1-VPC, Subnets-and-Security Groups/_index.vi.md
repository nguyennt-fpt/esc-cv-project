---
title : "VPC, Subnets, Security Groups"
date: "2024-01-01"
weight : 1
chapter : false
pre : " <b> 1.4.1 </b> "
---

Kiến trúc bao gồm một VPC có tên ecs-fargate-microservices-vpc. Bên trong VPC này, 6 subnets và 4 security groups được cấu hình để đảm bảo ứng dụng an toàn và tuân theo các best practices

![vpc](/images/1-ECS-Fargate-Microservices/1.4-Resources/vpc.png)

1. Public Subnets (cho Application Load Balancer)

Có hai public subnets, và chúng được sử dụng để host Application Load Balancer (ALB)

Security Group cho ALB

Inbound rules:

* Cho phép HTTP (port 80)

* Cho phép HTTPS (port 443)

Những ports này cho phép người dùng truy cập website của bạn

Egress rules:

* Chỉ những ports cần thiết được cho phép (trong trường hợp này là port 3000) dựa trên nguyên tắc least privilege

Điều này giúp giảm thiểu rủi ro như:

* Data exfiltration – containers gửi dữ liệu ra ngoài mạng

* Malware communication – kết nối đến các C2 servers độc hại

* Lateral movement – truy cập các dịch vụ nội bộ nên bị hạn chế

* Compliance violations – vi phạm các tiêu chuẩn bảo mật

![albsg](/images/1-ECS-Fargate-Microservices/1.4-Resources/albsg.png)

2. Private Subnets (cho ECS Tasks)

Có hai private subnets nơi ECS Fargate tasks chạy

Security Group cho ECS Tasks

Inbound rules:

* Chỉ cho phép traffic từ public ALB security group trên port 3000 (port ứng dụng của container)

Egress rules:

* Cho phép port 53 (DNS)

* Cho phép port 443 (HTTPS)

* Cho phép port 3000 (App)

* Cho phép port 3306 (MySQL)

Những port này cần thiết để tasks có thể pull images, kết nối đến AWS APIs, hoặc resolve domain names

![ecssg](/images/1-ECS-Fargate-Microservices/1.4-Resources/ecssg.png)

3. Private Subnets (cho RDS Database)

Có hai private subnets bổ sung dành riêng cho RDS instance

Security Group cho RDS

Inbound rules:

* Chỉ cho phép kết nối từ ECS task security group, sử dụng port 3306 (MySQL port)

Không có outbound rules: RDS database không cần truy cập internet, vì vậy outbound traffic bị chặn để bảo mật

![rdssg](/images/1-ECS-Fargate-Microservices/1.4-Resources/rdssg.png)

4. Security Group cho VPC Endpoint (ECR Endpoint)

Security group này được gắn vào Interface VPC Endpoint được sử dụng bởi ECS tasks để pull container images từ ECR một cách riêng tư (không qua internet)

Inbound rules

* Cho phép HTTPS (443) từ ECS Task Security Group

* Điều này cho phép ECS tasks truy cập ECR thông qua PrivateLink

Outbound rules

* Không cần outbound (egress) rule

* Để trống egress là an toàn và tuân theo strict least privilege best practice

![endpointsg](/images/1-ECS-Fargate-Microservices/1.4-Resources/endpointsg.png)