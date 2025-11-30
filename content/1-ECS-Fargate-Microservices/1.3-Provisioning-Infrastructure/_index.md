---
title : "Provisioning Infrastructure"
date: "2024-01-01"
weight : 3
chapter : false
pre : " <b> 1.3. </b> "
---

Before you begin, make sure Terraform is installed on your machine

You can download and install it from the official website: https://developer.hashicorp.com/terraform

After installing, verify it using: terraform -v
![terraform version](/images/1-ECS-Fargate-Microservices/1.3-Provisioning-Infrastructure/terraformversion.png)

You now have all the necessary tools to start provisioning the infrastructure

Step 1: Open the project folder

* Navigate to the ecs-project folder and open a terminal inside this directory

Step 2: Run Terraform commands

* You will use three main Terraform commands. Here is what each one does:

    1. terraform init
    * This command initializes the project
    * It downloads the necessary providers (such as AWS) and prepares Terraform to run

    2. terraform plan
    * This command shows you what Terraform will do before making any changes
    * It generates a detailed execution plan so you can review all resources that will be created, modified, or removed

    3. terraform apply
    * This command actually builds the infrastructure
    * Terraform will ask you to confirm before proceeding. Once approved, it starts creating all the resources defined in your configuration files
![terraform cmd](/images/1-ECS-Fargate-Microservices/1.3-Provisioning-Infrastructure/terraformcmd.png)

Step 3: Wait for deployment

* The full provisioning process may take 15–20 minutes depending on the resources being created