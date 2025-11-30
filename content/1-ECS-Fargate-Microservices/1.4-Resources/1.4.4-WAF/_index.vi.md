---
title : "Web Application Firewall"
date: "2024-01-01"
weight : 4
chapter : false
pre : " <b> 1.4.4 </b> "
---

Kiến trúc bao gồm một AWS Web Application Firewall (WAF) với một số managed rules để bảo vệ ứng dụng web:

* AWSManagedRulesCommonRuleSet (700 WCU) – bảo vệ chống lại các cuộc tấn công web phổ biến như XSS, path traversal, và các cuộc tấn công chung khác

* AWSManagedRulesSQLiRuleSet (200 WCU) – bảo vệ cụ thể chống lại các cuộc tấn công SQL Injection (SQLi) cố gắng thao túng các truy vấn cơ sở dữ liệu của bạn

* RateLimitRule – giới hạn số lượng requests từ một client trong một khoảng thời gian để ngăn chặn lạm dụng, brute-force attacks, hoặc các nỗ lực DDoS

Cùng nhau, những rules này giúp ứng dụng lọc traffic độc hại, ngăn chặn các lỗ hổng web phổ biến, và cải thiện bảo mật cũng như tuân thủ

![waf](/images/1-ECS-Fargate-Microservices/1.4-Resources/waf.png)

Lưu ý: Vì ngân sách có hạn, chỉ các managed rules cơ bản được áp dụng. Nếu bạn muốn tăng cường bảo mật, bạn có thể thêm các WAF rules bổ sung để bao phủ các mối đe dọa nâng cao hơn