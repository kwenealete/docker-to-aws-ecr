# Push Docker Image to AWS ECR

This repository demonstrates how to build and push a Docker image to AWS Elastic Container Registry (ECR).

---

## Prerequisites
1. **AWS CLI** installed and configured.
- Install: https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html
- Configure: Run `aws configure` and provide:
- AWS Access Key ID
- AWS Secret Access Key
- Default region
2. **Docker** installed.
- Install: https://docs.docker.com/get-docker/
3. **AWS ECR Repository** created:
- Create an ECR repository in AWS Management Console

---

## Steps to Push Docker Image to AWS ECR

### 1. Authenticate Docker to AWS ECR
Run the following AWS CLI command to authenticate Docker with your AWS ECR:
```bash
aws ecr get-login-password --region <your-region> | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.<your-region>.amazonaws.com

• Replace:
• <your-region> with your AWS region (e.g., us-east-1).
• <aws_account_id> with your AWS account ID.

![login-to-aws-ecr](app/images/login.png)

![login-to-aws-ecr1](app/images/login1.png)

2. Build the Docker Image

Navigate to the folder with your Dockerfile and build the image:

docker build -t <image-name> .

• Replace <image-name> with a descriptive name for your image.

![build](app/images/build.png)

3. Tag the Docker Image

Tag your image for AWS ECR:

docker tag <image-name>:latest <aws_account_id>.dkr.ecr.<your-region>.amazonaws.com/<repository-name>:<tag>

• Replace:
• <repository-name> with your ECR repository name.
• <tag> with a version (e.g., v1 or latest).

![tag](app/images/tag.png)

![tag1](app/images/tag1.png)

4. Push the Image to AWS ECR

Push the tagged image to AWS ECR:

docker push <aws_account_id>.dkr.ecr.<your-region>.amazonaws.com/<repository-name>:<tag>

![push](app/images/push.png)
![push1](app/images/push1.png)

5. Verify the Image in ECR

Go to the AWS Management Console → ECR → Your Repository to see the pushed image.

![image](app/images/images.png)

Example Commands

# Authenticate Docker to AWS ECR
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 123456789012.dkr.ecr.us-east-1.amazonaws.com

# Build the Docker image
docker build -t my-node-app .

# Tag the Docker image
docker tag my-node-app:1.0 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-node-app:1.0

# Push the Docker image
docker push 123456789012.dkr.ecr.us-east-1.amazonaws.com/my-node-app:1.0