---
title : "RDS, Secret Manager"
date: "2024-01-01"
weight : 7
chapter : false
pre : " <b> 1.4.7 </b> "
---

Khi bạn tìm kiếm RDS trong AWS Management Console, bạn có thể thấy rằng một RDS instance đã được tạo

![rds](/images/1-ECS-Fargate-Microservices/1.4-Resources/rds.png)

Để tăng cường bảo mật, dự án sử dụng AWS Secrets Manager để lưu trữ thông tin đăng nhập RDS

![secret](/images/1-ECS-Fargate-Microservices/1.4-Resources/secret.png)

Bằng cách sử dụng Terraform, RDS instance và thông tin đăng nhập của nó được định nghĩa dưới dạng code, có nghĩa là thông tin nhạy cảm như mật khẩu cơ sở dữ liệu không được hardcode ở bất kỳ đâu trong ứng dụng hoặc task definitions

* Terraform cung cấp RDS instance, Secrets Manager secret, và liên kết chúng tự động với ECS tasks hoặc các ứng dụng khác

* Secrets Manager có thể tự động xoay vòng thông tin đăng nhập, giảm rủi ro mật khẩu bị xâm phạm

* ECS tasks có thể truy xuất thông tin đăng nhập một cách an toàn tại runtime mà không phơi bày chúng

Cách tiếp cận này đảm bảo rằng thông tin đăng nhập cơ sở dữ liệu của bạn được bảo vệ, quản lý và truy cập an toàn, đồng thời giữ cho hạ tầng hoàn toàn tự động và có thể tái tạo