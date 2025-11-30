---
title : "Prerequiste"
date: "2024-01-01" 
weight : 2 
chapter : false
pre : " <b> 1.2. </b> "
---

Follow the steps below to prepare your environment before deploying the infrastructure

1. Clone the project from GitHub

* Open your terminal and clone the repository: git clone https://github.com/nguyennt-fpt/ecs-fargate-microserviecs

* Inside the project folder, you will find two main components:
    * getting-started-app/ – the source code used to build the Docker container
    * ecs-project/ – the Infrastructure as Code (IaC) built with Terraform

2. Install required tools

* Make sure the following tools are installed on your machine: Terraform, Git, AWS CLI, Docker

3. Configure AWS CLI with an Access Key

* Step 1 — Create an Access Key

    * Log in to the AWS Console, navigate to IAM, select Users, choose the user you want to use, go to the Security credentials tab, click Create access key
![accesskey](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/accesskey.png)
    * Follow the instructions then copy the: Access Key ID, Secret Access Key
![accesskey1](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/accesskey1.png)

* Step 2 — Configure a new AWS CLI profile

    * Open your terminal and run: aws configure --profile terraform

    * Enter the Access Key, Secret Access Key, region (e.g., ap-southeast-1), and output format

* Step 3 — Set this profile as default

    * On Windows PowerShell or CMD: setx AWS_PROFILE "terraform"

    * Close the terminal and open it again so the environment variable takes effect
![aws profile](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/awscli.png)

4. Create an ECR repository

* You need an Amazon ECR repository to store your Docker image

* In the AWS Console, search for ECR, click Create repository

* Enter a repository name, click Create
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/ecr.png)

* After creating it, open the repository and click View push commands.

* Keep this window open — you will need those commands to push your image.

5. Build and push the Docker image

* Make sure Docker Desktop is installed and running

* Open the folder: getting-started-app/

* Open a terminal inside this folder

* Paste and execute the push commands copied from ECR (These commands will log in to ECR, build the image, tag it, and push it)
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/buildimg.png)

* After completing the commands, go back to the ECR console.

* You should now see an image inside your repository.
![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/imgonecr.png)

6. Update the Terraform configuration

* Copy the repository URI from your ECR repository
(Example: 123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/my-app)

* Go to the folder: ecs-project/ then rename the file: terraform.tfvars.example → terraform.tfvars

* Find the variable container_image and paste the repository URI with the latest tag:

    container_image = "123456789012.dkr.ecr.ap-southeast-1.amazonaws.com/my-app:latest"

![ecr](/images/1-ECS-Fargate-Microservices/1.2-Prerequisite/changeimguri.png)
