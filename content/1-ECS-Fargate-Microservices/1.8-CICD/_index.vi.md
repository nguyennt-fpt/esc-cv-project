---
title: "CI/CD"
date: "2024-01-01"
weight: 8
chapter: false
pre: " <b> 1.8 </b> "
---
Triển khai CI/CD cho Build, Deploy và Rolling Update tự động

Bây giờ tôi sẽ triển khai quy trình CI/CD để bất cứ khi nào developer push phiên bản mới của ứng dụng lên GitHub, code sẽ được tự động build, Docker image sẽ được push lên ECR, và ECS service sẽ thực hiện rolling update với zero downtime

1. Tạo CodeBuild Project

Đi đến AWS CodeBuild và tạo project mới

Source provider: Chọn GitHub

Nếu đây là lần đầu kết nối với GitHub, hãy authorize kết nối

Chọn repository chứa source code của ứng dụng (Trong trường hợp này là getting-started-app)

![code1](/images/1-ECS-Fargate-Microservices/1.8-CICD/code1.png)

Đối với tùy chọn webhook, chọn: "Manually create a webhook for this repository in the GitHub console"

![code2](/images/1-ECS-Fargate-Microservices/1.8-CICD/code2.png)

Trong phần Buildspec, chọn "Use a buildspec file"

Để trống filename vì trong thư mục getting-started-app đã có sẵn file tên buildspec.yml
CodeBuild sẽ tự động phát hiện file này
(Nếu bạn sử dụng tên file khác, hãy nhập tên ở đây)

![code3](/images/1-ECS-Fargate-Microservices/1.8-CICD/code3.png)

Copy webhook URL được cung cấp bởi CodeBuild

![code4](/images/1-ECS-Fargate-Microservices/1.8-CICD/code4.png)

Thêm webhook trong GitHub, đi đến GitHub repository của bạn → Settings → Webhooks, click Add webhook

![code5](/images/1-ECS-Fargate-Microservices/1.8-CICD/code5.png)

Dán webhook URL đã copy từ CodeBuild, lưu webhook

![code6](/images/1-ECS-Fargate-Microservices/1.8-CICD/code6.png)

2. Đảm bảo quyền IAM cho CodeBuild

Đảm bảo rằng service role của CodeBuild có các quyền cần thiết để có thể:

* Pull dependencies

* Build Docker images

* Push images lên Amazon ECR

* Tương tác với CloudWatch Logs

* Tương tác với S3 (nếu artifacts được lưu trữ ở đó)

* Không có những quyền này, quá trình build sẽ thất bại

![iam](/images/1-ECS-Fargate-Microservices/1.8-CICD/iam.png)

3. Tạo CodePipeline

Đi đến AWS CodePipeline và tạo pipeline mới

Chọn "Build a custom pipeline"

![pipe1](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe1.png)

Đối với Source stage:

* Chọn GitHub

* Chọn repository

* Đặt Webhook event type = Push

![pipe2](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe2.png)

![pipe3](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe3.png)

Đối với Build stage:

* Chọn AWS CodeBuild

* Chọn CodeBuild project đã tạo trước đó

![pipe4](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe4.png)

Đối với Deploy stage:

* Input artifact: chọn BuildArtifact

* Deploy provider: Amazon ECS

* Chọn ECS cluster và service đã được tạo trước đó

* Click Create để khởi tạo pipeline

![pipe5](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe5.png)

Đảm bảo role của CodePipeline có quyền thực hiện công việc

![iam2](/images/1-ECS-Fargate-Microservices/1.8-CICD/iam2.png)

4. Kiểm tra CI/CD Pipeline

Bây giờ thực hiện một thay đổi nhỏ trong source code và push lên GitHub

![git1](/images/1-ECS-Fargate-Microservices/1.8-CICD/git1.png)

![git2](/images/1-ECS-Fargate-Microservices/1.8-CICD/git2.png)

Khi push hoàn tất:

* CodePipeline sẽ tự động bắt đầu chạy

* Build stage sẽ build Docker image và push lên ECR

* Deploy stage sẽ cập nhật ECS service

![git3](/images/1-ECS-Fargate-Microservices/1.8-CICD/git3.png)

Quan sát Rolling Update

Sau một thời gian ngắn, trong ECS service:

* Số lượng running tasks tăng lên 4 (2 tasks cũ + 2 tasks mới được tạo cho rolling update)

* Sau khi các tasks mới pass health checks, ECS sẽ terminate 2 tasks cũ

* Điều này xác nhận rằng rolling update đã hoạt động chính xác

![git4](/images/1-ECS-Fargate-Microservices/1.8-CICD/git4.png)

Cuối cùng, truy cập website lại

![git5](/images/1-ECS-Fargate-Microservices/1.8-CICD/git5.png)

Ứng dụng bây giờ hiển thị phiên bản đã cập nhật, có nghĩa là CI/CD pipeline đang hoạt động như mong đợi

Điều hướng đến ECR, có một image mới đã được push vào repository

![git6](/images/1-ECS-Fargate-Microservices/1.8-CICD/git6.png)