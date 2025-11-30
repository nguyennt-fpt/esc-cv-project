---
title : "Kiểm tra Auto Scaling"
date: "2024-01-01"
weight : 6
chapter : false
pre : " <b> 1.6. </b> "
---

Kiểm tra Auto Scaling của ECS Service

Tiếp theo, chúng ta sẽ cập nhật ECS service để xác minh rằng auto scaling đang hoạt động chính xác

Trong kiến trúc này, ECS Service đã được cấu hình với Auto Scaling bằng Terraform.

Tuy nhiên, để việc kiểm tra thuận tiện hơn, tôi sẽ thêm một policy thứ ba
Policy bổ sung này có thể được sử dụng để kích hoạt các hành động scaling mạnh mẽ hơn hoặc trong các điều kiện khác nhau, giúp dễ dàng quan sát và xác thực hành vi Auto Scaling trong quá trình load test hoặc demo

Đi đến ECS → ecs-fargate-microservices-cluster → chọn Update service

Trong phần Service Auto Scaling, click Add more scaling policy

Tạo một scaling policy mới với các cài đặt sau:

* Metric: ALBRequestCountPerTarget

* Target value: 50

* Scale-out cooldown: 60 seconds

* Scale-in cooldown: 300 seconds

Những giá trị này giúp dễ dàng kích hoạt các sự kiện scaling cho mục đích kiểm tra

![auto](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/auto.png)

Để tạo traffic, sử dụng công cụ load-testing như Apache Bench (ab)
Chạy lệnh: ab -n 10000 -c 20 your-domain-name

* -n 10000: tổng số requests

* -c 20: số requests đồng thời

![ab](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/ab.png)

Sau một thời gian ngắn, CloudWatch sẽ phát hiện tải tăng và kích hoạt alarm

![inalarm](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/inalarm.png)

Khi scaling policy được kích hoạt, số lượng tasks đang chạy sẽ tự động tăng

Trong bài test này, service đã scale từ 2 tasks lên 4 tasks

Điều này xác nhận rằng cấu hình auto scaling đang hoạt động như mong đợi

![scale](/images/1-ECS-Fargate-Microservices/1.6-Test-auto-scaling/scale.png)