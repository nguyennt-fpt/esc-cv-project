---
title : "Yêu cầu tiên quyết"
date: "2024-01-01" 
weight : 2 
chapter : false
pre : " <b> 1.2. </b> "
---

Thực hiện các bước dưới đây để chuẩn bị môi trường trước khi triển khai hạ tầng

1. Clone dự án từ GitHub

* Mở terminal và clone repository: git clone https://github.com/nguyennt-fpt/ecs-fargate-microserviecs

* Bên trong thư mục dự án, bạn sẽ tìm thấy hai thành phần chính:
    * getting-started-app/ – mã nguồn được sử dụng để build Docker container
    * ecs-project/ – Infrastructure as Code (IaC) được xây dựng bằng Terraform

2. Cài đặt các công cụ cần thiết

* Đảm bảo các công cụ sau được cài đặt trên máy của bạn: Terraform, Git, AWS CLI, Docker

3. Cấu hình AWS CLI với Access Key

* Bước 1 — Tạo Access Key

    * Đăng nhập vào AWS Console, điều hướng đến IAM, chọn Users, chọn user bạn muốn sử dụng, vào tab Security credentials, click Create access key
![accesskey](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/accesskey.png)
    * Làm theo hướng dẫn sau đó copy: Access Key ID, Secret Access Key
![accesskey1](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/accesskey1.png)

* Bước 2 — Cấu hình profile AWS CLI mới

    * Mở terminal và chạy: aws configure --profile terraform

    * Nhập Access Key, Secret Access Key, region (ví dụ: ap-southeast-1), và output format

* Bước 3 — Đặt profile này làm mặc định

    * Trên Windows PowerShell hoặc CMD: setx AWS_PROFILE "terraform"

    * Đóng terminal và mở lại để biến môi trường có hiệu lực
![aws profile](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/awscli.png)

4. Tạo ECR repository

* Bạn cần một Amazon ECR repository để lưu trữ Docker image

* Trong AWS Console, tìm kiếm ECR, click Create repository

* Nhập tên repository, click Create
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/ecr.png)

* Sau khi tạo xong, mở repository và click View push commands.

* Giữ cửa sổ này mở — bạn sẽ cần những lệnh đó để push image.

5. Build và push Docker image

* Đảm bảo Docker Desktop được cài đặt và đang chạy

* Mở thư mục: getting-started-app/

* Mở terminal bên trong thư mục này

* Dán và thực thi các lệnh push đã copy từ ECR (Những lệnh này sẽ đăng nhập vào ECR, build image, tag nó, và push nó)
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/buildimg.png)

* Sau khi hoàn thành các lệnh, quay lại ECR console.

* Bây giờ bạn sẽ thấy một image bên trong repository của mình.
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/imgonecr.png)

6. Cập nhật cấu hình Terraform

* Copy repository URI từ ECR repository của bạn
(Ví dụ: 123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/my-app)

* Đi đến thư mục: ecs-project/ sau đó đổi tên file: terraform.tfvars.example → terraform.tfvars

* Tìm biến container_image và dán repository URI với tag latest:

    container_image = "123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/my-app:latest"

![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/changeimguri.png)