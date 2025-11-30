---
title : "ECR Endpoint"
date: "2024-01-01"
weight : 6
chapter : false
pre : " <b> 1.4.6 </b> "
---

Dự án sử dụng VPC Endpoint cho Amazon ECR thay vì NAT gateway để pull container images cho ECS tasks

* VPC Endpoint là một kết nối riêng tư giữa VPC của bạn và các dịch vụ AWS, cho phép các tài nguyên trong private subnets truy cập ECR mà không cần đi qua internet công cộng

* Cách tiếp cận này tăng cường bảo mật vì traffic vẫn nằm trong mạng AWS, giảm thiểu việc phơi bày với các mối đe dọa bên ngoài tiềm ẩn như nghe lén hoặc tấn công

* Nó cũng đơn giản hóa cấu hình mạng vì bạn không cần thiết lập NAT gateway hoặc quản lý public IP addresses cho ECS tasks của mình

* Ngoài ra, sử dụng VPC Endpoint có thể giúp giảm chi phí truyền dữ liệu, vì traffic trong mạng AWS thường rẻ hơn so với gửi qua NAT gateway ra internet

Nhìn chung, thiết lập này đảm bảo rằng containers của bạn có thể pull images từ ECR một cách an toàn và hiệu quả trong khi vẫn giữ chúng cô lập trong private subnets

![endpoint](/images/1-ECS-Fargate-Microservices/1.4-Resources/endpoint.png)