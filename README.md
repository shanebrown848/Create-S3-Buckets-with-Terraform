![Terraform Project Badge](./trophy-terraform.png)

# Create S3 Buckets with Terraform

**Project Link:** http://learn.nextwork.org/projects/aws-devops-terraform1  
**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com  

---

## Project Overview

This project demonstrates how to use **Terraform** to automate the creation and management of AWS infrastructure, specifically an **Amazon S3 bucket**. The goal was to gain hands-on experience with Infrastructure as Code (IaC) by defining, deploying, and managing cloud resources through configuration files rather than manual setup.

The project walks through the full Terraform workflow, from initialization and planning to applying changes and validating deployed resources. It also includes a project extension that uploads an object to the S3 bucket using Terraform.

---

## Tools and Technologies

**Services Used**
- Amazon S3
- Terraform
- AWS CLI

**Core Concepts**
- Infrastructure as Code (IaC)
- Terraform providers and resources
- Configuration blocks
- Terraform state management
- Resource tagging
- Command workflow: `init`, `plan`, `apply`

---

## What I Built

- A fully managed S3 bucket created with Terraform
- Environment tagging using `Environment = "Dev"`
- AWS authentication using AWS CLI access keys
- An uploaded S3 object managed by Terraform
- Verified deployment through both Terraform output and AWS Console

---

## Terraform Configuration Structure

The Terraform configuration is organized using modular blocks:

- **Provider Block**  
  Defines AWS as the cloud provider and establishes the environment context.

- **Resource Block**  
  Specifies the S3 bucket and its configuration, acting as the blueprint for the infrastructure.

- **Output Block**  
  Exposes useful information, such as the bucket name or ARN, after deployment.

This structure improves readability, maintainability, and scalability while allowing changes to be made safely and independently.

---

## Terraform Workflow

1. **terraform init**  
   Initializes the project and installs required provider plugins.

2. **terraform plan**  
   Previews infrastructure changes by comparing the desired state with the current environment.

3. **terraform apply**  
   Executes the plan and provisions real AWS resources.

Running these commands in sequence ensures safe, predictable deployments.

---

## AWS Authentication

During planning, I encountered the error:

