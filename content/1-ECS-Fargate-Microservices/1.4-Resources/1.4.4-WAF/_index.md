---
title : "Web Application Firewall"
date: "2024-01-01"
weight : 4
chapter : false
pre : " <b> 1.4.4 </b> "
---

The architecture includes an AWS Web Application Firewall (WAF) with several managed rules to protect the web application:

* AWSManagedRulesCommonRuleSet (700 WCU) – protects against common web exploits such as XSS, path traversal, and other generic attacks

* AWSManagedRulesSQLiRuleSet (200 WCU) – specifically protects against SQL Injection (SQLi) attacks that try to manipulate your database queries

* RateLimitRule – limits the number of requests from a single client within a time period to prevent abuse, brute-force attacks, or DDoS attempts

Together, these rules help the application filter malicious traffic, prevent common web vulnerabilities, and improve security and compliance

![waf](/images/1-ECS-Fargate-Microservices/1.4-Resources/waf.png)

Note: Since the budget is limited, only basic managed rules are applied. If you want to enhance security, you can add additional WAF rules to cover more advanced threats