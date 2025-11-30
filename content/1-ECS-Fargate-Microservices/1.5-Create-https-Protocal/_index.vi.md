---
title : "Tạo giao thức HTTPS"
date: "2024-01-01"
weight : 5
chapter : false
pre : " <b> 1.5. </b> "
---

Kích hoạt HTTPS cho Ứng dụng Web

Để kích hoạt HTTPS, trước tiên bạn cần một hosted zone trong Route 53, điều này yêu cầu một tên miền đã đăng ký. Bạn có thể mua domain từ bất kỳ nhà cung cấp domain nào và trỏ nameservers của nó đến Route 53

Bước 1: Tạo Record trong Route 53

* Mở Route 53 và đi đến hosted zone của bạn

* Click Create record

![record1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record1.png)

* Đối với Record type, chọn A – Routes traffic to an IPv4 address and some AWS resources

* Trong Route traffic to, chọn Alias to Application and Classic Load Balancer

* Chọn ALB hiện có của bạn và click Create record

![record2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record2.png)

* Bây giờ bạn có thể thấy một record mới đã được tạo

![record3](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record3.png)

Bước 2: Thêm HTTPS Listener vào ALB

* Đi đến EC2 console → Load Balancing → chọn ALB của bạn

![listener1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/listener1.png)

* Click Add listener và chọn Protocol: HTTPS

* Chọn target group (ecs-fargate-microservices-tg)

![listener2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/listener2.png)

* Trong Default SSL/TLS certificate, click Request a new ACM certificate

![acm1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm1.png)

* Copy tên domain từ record bạn đã tạo trong Route 53 vào trường domain name của ACM

* Để các cài đặt khác mặc định và click Create

![acm2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm2.png)

* Click Create record in Route 53 để xác thực certificate

![acm3](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm3.png)

* Một record mới đã được tạo trong Route 53

![acm4](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm4.png)

* Chờ khoảng 2 phút để certificate được cấp

![acm5](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm5.png)

* Quay lại trang Add listener, chọn certificate vừa tạo và click Create

![acm6](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm6.png)

Bước 3: Chuyển hướng HTTP sang HTTPS

* Chọn listener trên port 80 → Manage listener → Edit listener

![redirect](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/redirect.png)

* Chọn Redirect to URL và đặt Port: 443, sau đó lưu rule

![redirectconfig](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/redirectconfig.png)

Bước 4: Kiểm tra cấu hình

* Truy cập ứng dụng web của bạn bằng HTTPS → nó sẽ tải thành công

![https](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/https.png)

* Truy cập bằng HTTP → nó sẽ tự động chuyển hướng sang HTTPS
![http](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/http.png)
![http2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/http2.png)