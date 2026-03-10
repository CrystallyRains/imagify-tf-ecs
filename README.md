Imagify: AI SaaS Platform with Full DevOps Automation
Imagify is a high-performance AI Image SaaS platform that allows users to perform generative AI transformations like image restoration, background removal, and generative filling.

This project demonstrates a production-grade Cloud Engineering workflow, moving a full-stack Next.js application into a fully automated, scalable AWS environment using Terraform, Docker, and GitHub Actions.

🤖 Features
AI Image Restoration: Revive old or damaged images.

Generative Fill: Seamlessly modify or add elements within an image.

Object/Background Removal: Clean up photos with professional AI precision.

Image Recoloring: Change object colors using natural language prompts.

Credits System: Secure payment integration via Stripe.

Authentication: User management and route protection via Clerk.

🏗️ The Cloud Infrastructure
As a Cloud Engineer, I automated the entire infrastructure to ensure zero manual configuration in the AWS Console.

1. Infrastructure as Code (Terraform)
Located in the /terraform directory, the code provisions:

Custom VPC: Isolated network with Public and Private subnets across multiple Availability Zones.

AWS ECS Fargate: Serverless container orchestration for the Next.js app (no EC2 management required).

Application Load Balancer (ALB): Handles traffic distribution and health checks.

S3 & DynamoDB Backend: Managed state locking for Terraform to prevent concurrent update conflicts.

2. CI/CD Automation (GitHub Actions)
The project uses three specialized pipelines:

Infrastructure Workflow: Automates terraform apply when infra code is updated.

Build Workflow: Uses a multi-stage Docker build to optimize image size and pushes it to Amazon ECR.

Deploy Workflow: Performs a Rolling Update on the ECS service for zero-downtime releases.

🚀 Step-by-Step Setup Guide
Follow these steps to deploy this project to your own AWS account.

1. Prerequisites
AWS CLI and Terraform installed.

Docker installed locally.

Accounts for: Clerk, MongoDB, Cloudinary, and Stripe.

2. Bootstrap the Backend
Before deploying the main app, you need a place for Terraform to store its state.

Navigate to /infra-bootstrap.

Run terraform init and terraform apply.

This creates your S3 bucket and DynamoDB table.

3. Provision the AWS Stack
Navigate to /terraform.

Update your variables in terraform.tfvars.

Run terraform init and terraform apply.

Copy the ALB DNS Name from the output—this is your app's live URL.

4. Configure GitHub Secrets
Add the following to your GitHub Repository Secrets so the pipelines can run:

AWS_ACCESS_KEY_ID & AWS_SECRET_ACCESS_KEY

MONGODB_URL, STRIPE_SECRET_KEY, CLOUDINARY_API_KEY, etc.

Note: Any variable starting with NEXT_PUBLIC_ must be passed as a Build Argument in your GitHub Action to be available in the browser.

5. Deploy the App
Simply push your changes to the main branch.

The Build workflow will package the app.

The Deploy workflow will update the ECS containers automatically.

🛠️ Tech Stack
App: Next.js, TypeScript, Tailwind CSS, MongoDB

Cloud: AWS (VPC, ECS, ECR, ALB, S3, DynamoDB)

Automation: Terraform, Docker, GitHub Actions

Services: Clerk, Stripe, Cloudinary AI

