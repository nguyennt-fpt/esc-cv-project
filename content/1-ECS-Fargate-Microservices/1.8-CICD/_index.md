---
title: "CICD"
date: "2024-01-01"
weight: 8
chapter: false
pre: " <b> 1.8 </b> "
---
Implementing CI/CD for Automated Build, Deployment, and Rolling Update

Now I will implement a CI/CD workflow so that whenever a developer pushes a new version of the application to GitHub, the code will be automatically built, the Docker image will be pushed to ECR, and the ECS service will perform a rolling update with zero downtime

1. Creating the CodeBuild Project

Go to AWS CodeBuild and create a new project

Source provider: Select GitHub

If this is the first time connecting to GitHub, authorize the connection

Choose the repository that contains the application source code(In this case is getting-started-app)

![code1](/images/1-ECS-Fargate-Microservices/1.8-CICD/code1.png)

For the webhook option, select: "Manually create a webhook for this repository in the GitHub console"

![code2](/images/1-ECS-Fargate-Microservices/1.8-CICD/code2.png)

In the Buildspec section, select "Use a buildspec file"

Leave the filename empty because in the getting-started-app folder, there is already a file named buildspec.yml
CodeBuild will automatically detect this file
(If you use a different filename, enter the name here)

![code3](/images/1-ECS-Fargate-Microservices/1.8-CICD/code3.png)

Copy the webhook URL provided by CodeBuild

![code4](/images/1-ECS-Fargate-Microservices/1.8-CICD/code4.png)

Add webhook in GitHub, go to your GitHub repository → Settings → Webhooks, click Add webhook

![code5](/images/1-ECS-Fargate-Microservices/1.8-CICD/code5.png)

Paste the webhook URL copied from CodeBuild, save the webhook

![code6](/images/1-ECS-Fargate-Microservices/1.8-CICD/code6.png)

2. Ensuring IAM Permissions for CodeBuild

Make sure that the CodeBuild service role contains the necessary permissions so it can:

* Pull dependencies

* Build Docker images

* Push images to Amazon ECR

* Interact with CloudWatch Logs

* Interact with S3 (if artifacts are stored there)

* Without these permissions, the build process will fail

![iam](/images/1-ECS-Fargate-Microservices/1.8-CICD/iam.png)

3. Creating the CodePipeline

Go to AWS CodePipeline and create a new pipeline

Choose "Build a custom pipeline"

![pipe1](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe1.png)

For the Source stage:

* Select GitHub

* Choose the repository

* Set Webhook event type = Push

![pipe2](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe2.png)

![pipe3](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe3.png)

For the Build stage:

* Select AWS CodeBuild

* Choose the CodeBuild project created earlier

![pipe4](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe4.png)

For the Deploy stage:

* Input artifact: choose the BuildArtifact

* Deploy provider: Amazon ECS

* Choose the ECS cluster and service that were created previously

* Click Create to initialize the pipeline

![pipe5](/images/1-ECS-Fargate-Microservices/1.8-CICD/pipe5.png)

Make sure the role of CodePipeline has permission to do the job

![iam2](/images/1-ECS-Fargate-Microservices/1.8-CICD/iam2.png)

4. Testing the CI/CD Pipeline

Now make a small change in the source code and push it to GitHub

![git1](/images/1-ECS-Fargate-Microservices/1.8-CICD/git1.png)

![git2](/images/1-ECS-Fargate-Microservices/1.8-CICD/git2.png)

Once the push is completed:

* CodePipeline will automatically start running

* The build stage will build the Docker image and push it to ECR

* The deploy stage will update the ECS service

![git3](/images/1-ECS-Fargate-Microservices/1.8-CICD/git3.png)

Observing the Rolling Update

After a short time, in the ECS service:

* The number of running tasks increases to 4 (2 old tasks + 2 new tasks created for the rolling update)

* After the new tasks pass health checks, ECS will terminate the 2 old tasks

* This confirms that the rolling update worked correctly

![git4](/images/1-ECS-Fargate-Microservices/1.8-CICD/git4.png)

Finally, visit the website again

![git5](/images/1-ECS-Fargate-Microservices/1.8-CICD/git5.png)

The application now shows the updated version, meaning the CI/CD pipeline is functioning as expected

Navigate to ECR, there are a new image was push on the repository

![git6](/images/1-ECS-Fargate-Microservices/1.8-CICD/git6.png)