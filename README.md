# -Day-02-Push-Your-Docker-Images-to-AWS-with-Amazon-ECR

Welcome to Day 2 of my 30-day tech blogging journey! Today we explore Amazon Elastic Container Registry (ECR) — a fully managed Docker image repository service from AWS.

What is Amazon ECR?
Amazon ECR allows you to store, manage, and deploy container images securely and at scale. It integrates seamlessly with Amazon ECS, AWS Fargate, and Amazon EKS.

Step-by-Step: Push Docker Image to Amazon ECR
Let’s walk through how to push a Docker image to ECR.



1️⃣ Authenticate Docker to Amazon ECR
Run this command to authenticate your Docker CLI:
![Screenshot 2025-06-07 175847](https://github.com/user-attachments/assets/333600e1-f8d6-4648-a3e3-d0fc4581a6ac)

Create an ECR Repository
Create your repository via CLI or console:

bashCopyEditaws ecr create-repository --repository-name my-app

3️⃣ Build Your Docker Image
Make sure you're in the directory with your Dockerfile:

bashCopyEditdocker build -t my-app .


4️⃣ Tag the Docker Image
Tag the image using your repository URI:

bashCopyEditdocker tag my-app:latest <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:latest

5️⃣ Push the Docker Image to ECR
Now push the tagged image to your ECR:

bashCopyEditdocker push <aws_account_id>.dkr.ecr.<region>.amazonaws.com/my-app:latest


Deploy with ECS or Fargate
Once your image is in ECR, you can use ECS or Fargate to run it.
![Screenshot 2025-06-07 181344](https://github.com/user-attachments/assets/a9433d33-bc1f-47c5-a6a9-e6bde610194c)

Create a Task Definition: Use the image URL from ECR.

Assign IAM Roles: Ensure the task has AmazonEC2ContainerRegistryReadOnly permission.

Deploy the Task: Launch it in an ECS cluster
![Screenshot 2025-06-07 180934](https://github.com/user-attachments/assets/e2a29641-507f-4b5c-9847-a5770ae85849)



Automate Image Cleanup with Lifecycle Policies
ECR allows automatic cleanup of old/untagged images using Lifecycle Policies.
![Screenshot 2025-06-07 182056](https://github.com/user-attachments/assets/1fcdb648-9f07-4b55-ae1b-a42673da31a4)



Final output:
![Screenshot 2025-06-07 182112](https://github.com/user-attachments/assets/17a6bba4-bfeb-4815-b621-a8944b0ee3a2)

