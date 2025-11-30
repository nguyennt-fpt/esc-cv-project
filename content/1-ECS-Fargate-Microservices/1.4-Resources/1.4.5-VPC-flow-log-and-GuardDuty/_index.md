---
title : "VPC Flow Log, GuardDuty"
date: "2024-01-01"
weight : 5
chapter : false
pre : " <b> 1.4.4 </b> "
---

The architecture also includes AWS GuardDuty and VPC Flow Logs to enhance security monitoring

AWS GuardDuty is a threat detection service that continuously monitors your AWS accounts and workloads for malicious or unauthorized activity. It analyzes data from sources like VPC Flow Logs, CloudTrail events, and DNS logs to detect threats such as compromised instances, reconnaissance activities, or unusual API calls

![guardduty](/images/1-ECS-Fargate-Microservices/1.4-Resources/guardduty.png)

VPC Flow Logs capture information about the IP traffic going to and from network interfaces in your VPC. This allows you to monitor network activity, troubleshoot connectivity issues, and support security analysis by providing detailed traffic visibility

![flowlog](/images/1-ECS-Fargate-Microservices/1.4-Resources/flowlog.png)

Together, GuardDuty and VPC Flow Logs help the project detect, investigate, and respond to potential security threats, improving overall cloud security