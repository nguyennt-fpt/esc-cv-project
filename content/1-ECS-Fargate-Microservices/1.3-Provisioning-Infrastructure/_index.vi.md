---
title : "Triển khai hạ tầng"
date: "2024-01-01"
weight : 3
chapter : false
pre : " <b> 1.3. </b> "
---

Trước khi bắt đầu, hãy đảm bảo Terraform đã được cài đặt trên máy của bạn

Bạn có thể tải xuống và cài đặt từ trang web chính thức: https://developer.hashicorp.com/terraform

Sau khi cài đặt, xác minh bằng cách sử dụng: terraform -v
![terraform version](/images/1-ECS-Fargate-Microservices/1.3-Provisioning-Infrastructure/terraformversion.png)

Bây giờ bạn đã có tất cả các công cụ cần thiết để bắt đầu cung cấp hạ tầng

Bước 1: Mở thư mục dự án

* Điều hướng đến thư mục ecs-project và mở terminal bên trong thư mục này

Bước 2: Chạy các lệnh Terraform

* Bạn sẽ sử dụng ba lệnh Terraform chính. Đây là những gì mỗi lệnh thực hiện:

    1. terraform init
    * Lệnh này khởi tạo dự án
    * Nó tải xuống các provider cần thiết (như AWS) và chuẩn bị Terraform để chạy

    2. terraform plan
    * Lệnh này cho bạn thấy Terraform sẽ làm gì trước khi thực hiện bất kỳ thay đổi nào
    * Nó tạo ra một kế hoạch thực thi chi tiết để bạn có thể xem xét tất cả các tài nguyên sẽ được tạo, sửa đổi hoặc xóa

    3. terraform apply
    * Lệnh này thực sự xây dựng hạ tầng
    * Terraform sẽ yêu cầu bạn xác nhận trước khi tiến hành. Sau khi được phê duyệt, nó bắt đầu tạo tất cả các tài nguyên được định nghĩa trong các file cấu hình của bạn
![terraform cmd](/images/1-ECS-Fargate-Microservices/1.3-Provisioning-Infrastructure/terraformcmd.png)

Bước 3: Chờ triển khai

* Quá trình cung cấp đầy đủ có thể mất 15–20 phút tùy thuộc vào các tài nguyên đang được tạo