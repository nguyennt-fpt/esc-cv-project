---
title : "Testing WAF and GuardDuty"
date: "2024-01-01"
weight : 7
chapter : false
pre : " <b> 1.7. </b> "
---

Testing AWS WAF Protection

Next, I performed a few simple commands to verify whether AWS WAF is working correctly and blocking common attack patterns

I sent several simulated malicious requests (such as SQL Injection and XSS payloads)

![attack](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/attack.png)

The response returned was 403 Forbidden, which confirms that WAF successfully blocked the requests

![result](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/result.png)

I then checked the WAF dashboard in the AWS Management Console

After a few test attempts, the number of blocked requests increased to 13, indicating that WAF is functioning properly and enforcing the configured rules as expected

![block](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/block.png)

🔍 Testing Amazon GuardDuty

After verifying WAF, I proceeded to test Amazon GuardDuty

Because no real attack was occurring, I used the built-in AWS feature “Generate Sample Findings” to simulate security findings

Right after generating the sample findings, GuardDuty displayed:

* Total findings: 374

* Resources with findings: 16

* Accounts with findings: 1

![guardduty](/images/1-ECS-Fargate-Microservices/1.7-Test-Waf-GuardDuty/guardduty.png)

These results confirm that GuardDuty is working correctly. It is able to detect threats, generate findings, and display detailed security insights in real time.