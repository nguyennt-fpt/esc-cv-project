---
title : "Create https Protocal"
date: "2024-01-01"
weight : 5
chapter : false
pre : " <b> 1.5. </b> "
---

Enabling HTTPS for the Web Application

To enable HTTPS, you first need a hosted zone in Route 53, which requires a registered domain name. You can purchase a domain from any domain provider and point its nameservers to Route 53

Step 1: Create a Record in Route 53

* Open Route 53 and go to your hosted zone

* Click Create record

![record1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record1.png)

* For Record type, select A – Routes traffic to an IPv4 address and some AWS resources

* Under Route traffic to, select Alias to Application and Classic Load Balancer

* Choose your existing ALB and click Create record

![record2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record2.png)

* Now you can see a new record was created

![record3](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/record3.png)

Step 2: Add an HTTPS Listener to the ALB

* Go to the EC2 console → Load Balancing → select your ALB

![listener1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/listener1.png)

* Click Add listener and choose Protocol: HTTPS

* Select the target group (ecs-fargate-microservices-tg)

![listener2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/listener2.png)

* Under Default SSL/TLS certificate, click Request a new ACM certificate

![acm1](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm1.png)

* Copy the domain name from the record you created in Route 53 into the ACM domain name field

* Leave other settings as default and click Create

![acm2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm2.png)

* Click Create record in Route 53 to validate the certificate

![acm3](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm3.png)

* A new record was created in Route 53 

![acm4](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm4.png)

* Wait approximately 2 minutes for the certificate to be issued

![acm5](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm5.png)

* Return to the Add listener page, select the newly created certificate, and click Create

![acm6](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/acm6.png)

Step 3: Redirect HTTP to HTTPS

* Select the listener on port 80 → Manage listener → Edit listener

![redirect](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/redirect.png)

* Choose Redirect to URL and set Port: 443, then save the rule 

![redirectconfig](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/redirectconfig.png)

Step 4: Test the Configuration

* Access your web application using HTTPS → it should load successfully

![https](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/https.png)

* Access it using HTTP → it should automatically redirect to HTTPS
![http](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/http.png)
![http2](/images/1-ECS-Fargate-Microservices/1.5-Create-https-Protocal/http2.png)