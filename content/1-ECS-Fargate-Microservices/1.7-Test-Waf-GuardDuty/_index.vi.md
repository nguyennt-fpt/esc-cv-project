---
title : "Kiểm tra WAF và GuardDuty"
date: "2024-01-01"
weight : 7
chapter : false
pre : " <b> 1.7. </b> "
---

Kiểm tra bảo vệ của AWS WAF

Tiếp theo, tôi đã thực hiện một vài lệnh đơn giản để xác minh liệu AWS WAF có hoạt động chính xác và chặn các mẫu tấn công phổ biến hay không

Tôi đã gửi một số requests độc hại mô phỏng (như SQL Injection và XSS payloads)

![attack](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/attack.png)

Phản hồi trả về là 403 Forbidden, điều này xác nhận rằng WAF đã chặn thành công các requests

![result](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/result.png)

Sau đó tôi kiểm tra dashboard WAF trong AWS Management Console

Sau một vài lần thử nghiệm, số lượng requests bị chặn đã tăng lên 13, cho thấy WAF đang hoạt động đúng cách và thực thi các rules đã cấu hình như mong đợi

![block](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/block.png)

🔍 Kiểm tra Amazon GuardDuty

Sau khi xác minh WAF, tôi tiến hành kiểm tra Amazon GuardDuty

Vì không có cuộc tấn công thực sự nào xảy ra, tôi đã sử dụng tính năng tích hợp sẵn của AWS "Generate Sample Findings" để mô phỏng các phát hiện bảo mật

Ngay sau khi tạo sample findings, GuardDuty hiển thị:

* Tổng số findings: 374

* Tài nguyên có findings: 16

* Tài khoản có findings: 1

![guardduty](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/guardduty.png)

Những kết quả này xác nhận rằng GuardDuty đang hoạt động chính xác. Nó có thể phát hiện mối đe dọa, tạo findings và hiển thị thông tin bảo mật chi tiết trong thời gian thực.