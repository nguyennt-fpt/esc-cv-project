---
title : "Tài nguyên"
date: "2024-01-01"
weight : 4
chapter : false
pre : " <b> 1.4. </b> "
---

### Tài nguyên được tạo sau khi cung cấp hạ tầng bằng Terraform

Sau khi chạy Terraform để thiết lập hạ tầng, các tài nguyên sau sẽ được tạo:

1. VPC, Subnets, và Security Groups
Các thành phần mạng cơ bản cung cấp mạng cô lập, định tuyến và quy tắc lọc lưu lượng

2. Application Load Balancer (ALB)
Phân phối lưu lượng đến trên các dịch vụ ECS để đảm bảo tính khả dụng cao và khả năng mở rộng

3. ECS Cluster
Môi trường điều phối container nơi các dịch vụ của bạn sẽ chạy trên AWS Fargate

4. AWS WAF
Tường lửa ứng dụng web giúp bảo vệ ứng dụng khỏi các cuộc tấn công web phổ biến

5. VPC Flow Logs và Amazon GuardDuty
Các dịch vụ bảo mật và giám sát phân tích lưu lượng mạng và phát hiện hoạt động đáng ngờ hoặc độc hại

6. ECR VPC Endpoints
Các endpoint riêng tư cho phép ECS tasks kéo container images từ Amazon ECR một cách bảo mật mà không sử dụng internet công cộng

7. RDS và Secrets Manager
Một instance cơ sở dữ liệu được quản lý và thông tin đăng nhập cơ sở dữ liệu được lưu trữ bảo mật được sử dụng bởi ứng dụng của bạn