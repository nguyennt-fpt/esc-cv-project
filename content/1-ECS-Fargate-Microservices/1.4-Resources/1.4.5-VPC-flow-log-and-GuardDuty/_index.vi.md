---
title : "VPC Flow Log, GuardDuty"
date: "2024-01-01"
weight : 5
chapter : false
pre : " <b> 1.4.5 </b> "
---

Kiến trúc cũng bao gồm AWS GuardDuty và VPC Flow Logs để tăng cường giám sát bảo mật

AWS GuardDuty là một dịch vụ phát hiện mối đe dọa liên tục giám sát các tài khoản AWS và workloads của bạn để tìm hoạt động độc hại hoặc không được ủy quyền. Nó phân tích dữ liệu từ các nguồn như VPC Flow Logs, CloudTrail events, và DNS logs để phát hiện các mối đe dọa như instances bị xâm phạm, hoạt động trinh sát, hoặc các API calls bất thường

![guardduty](/images/1-ECS-Fargate-Microservices/1.4-Resources/guardduty.png)

VPC Flow Logs ghi lại thông tin về IP traffic đi đến và đi từ các network interfaces trong VPC của bạn. Điều này cho phép bạn giám sát hoạt động mạng, khắc phục sự cố kết nối, và hỗ trợ phân tích bảo mật bằng cách cung cấp khả năng hiển thị traffic chi tiết

![flowlog](/images/1-ECS-Fargate-Microservices/1.4-Resources/flowlog.png)

Cùng nhau, GuardDuty và VPC Flow Logs giúp dự án phát hiện, điều tra và phản ứng với các mối đe dọa bảo mật tiềm ẩn, cải thiện bảo mật cloud tổng thể