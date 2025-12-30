<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create S3 Buckets with Terraform

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-terraform1)

**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com

---

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Introducing Today's Project!

In this project, I will demonstrate how to use Terraform to automate the creation and management of AWS resources, specifically an S3 bucket. The goal is to learn how infrastructure as code works in a real-world cloud environment, from configuring Terraform and AWS credentials to deploying and managing cloud storage in a repeatable and reliable way. This project focuses on reducing manual setup, improving consistency, and building practical DevOps skills that apply directly to modern cloud and platform engineering workflows.

### Tools and concepts

Services I used were AWS S3, Terraform, and the AWS CLI to create and manage cloud resources from my local machine. Terraform was used to define and deploy infrastructure, AWS S3 served as the storage service for the bucket and uploaded object, and the AWS CLI was used to authenticate and provide credentials for Terraform to interact with AWS.

Key concepts I learnt include infrastructure as code, where cloud resources are defined in configuration files instead of being created manually, Terraform providers and resources, configuration blocks, and the importance of the Terraform workflow using init, plan, and apply. I also learned how Terraform manages state, how tagging helps organize resources, and how Terraform can manage both infrastructure and the data inside cloud services like S3.

### Project reflection

This project took me approximately two hours to complete. The most challenging part was deciding whether to use Windows PowerShell or my WSL environment with Kali Linux, since each option required slightly different setup and configuration. It took some time to test both and determine which workflow felt more efficient and reliable for this project. It was most rewarding to successfully complete the setup using Kali Linux and see the Terraform configuration work end to end, from planning to launching the S3 bucket and uploading an object.

I chose to do this project today because I wanted hands-on experience using Terraform to manage real AWS infrastructure and strengthen my understanding of infrastructure as code. Working through the full workflow, from configuration to deployment, helped reinforce concepts that are important for real-world cloud and DevOps work. Something that would make learning with NextWork even better is providing more optional challenges or environment-specific tips, such as guidance for different operating systems or WSL setups, so learners can more easily choose the workflow that fits their system.

---

## Introducing Terraform

Terraform is an infrastructure as code tool that allows you to define, deploy, and manage cloud resources using configuration files instead of manual setup. It uses these files as a blueprint to automatically create and update infrastructure such as storage, compute, and networking across cloud providers like AWS, Azure, and Google Cloud. By treating infrastructure as code, Terraform makes cloud environments repeatable, version-controlled, and easier to manage at scale.

Terraform is one of the most popular tools used for infrastructure as code (IaC), which is the practice of defining and managing cloud infrastructure using code instead of manual configuration. With IaC, resources such as servers, storage, and networks are described in text-based files that can be version-controlled, shared with a team, and reused to create identical environments. This approach improves consistency, reduces human error, and makes it easier to deploy, update, and reproduce cloud infrastructure reliably.

Terraform uses configuration files to define the desired state of infrastructure in a clear, repeatable way. These files tell Terraform what resources should exist, how they should be configured, and how they relate to each other. Terraform reads these configurations and determines the steps needed to create, update, or remove resources so the real infrastructure matches what is defined in code.

main.tf is the primary configuration file in a Terraform project where this infrastructure definition begins. It acts as the blueprint for the project, containing the core instructions that describe what Terraform should build and manage. By writing infrastructure details in main.tf, you make your setup organized, version-controlled, and easy to reproduce or modify as the project grows.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Configuration files

The configuration is structured in Terraform using self-contained blocks, where each block has a specific role in defining the infrastructure. A provider block specifies which cloud platform Terraform should interact with, such as AWS, and sets the context for all resources. Resource blocks define what infrastructure components to create, like an S3 bucket, and describe their desired settings. Additional blocks, such as variables, outputs, data sources, and modules, support flexibility, reuse, and visibility by allowing values to be parameterized, results to be displayed, existing resources to be referenced, and common logic to be shared.

The advantage of defining the configuration this way is clarity and modularity. Each block focuses on one responsibility, which keeps the configuration readable and easy to maintain. Changes can be made to a single part of the infrastructure without affecting unrelated components. This structure also makes the setup more reusable, scalable, and safer

### My main.tf configuration has three blocks

The first block indicates the provider, which tells Terraform which cloud platform to work with and how to connect to it. In this project, it defines AWS as the provider, setting the context so Terraform knows where the infrastructure will be created.

The second block provisions the resource, which describes what Terraform should build. Here, it defines an S3 bucket and specifies its name and configuration, acting as the blueprint for the actual cloud resource Terraform will create.

The third block manages the results of the configuration, typically by exposing useful information after the infrastructure is created. This block allows Terraform to output details, such as the S3 bucket name or ARN, making it easier to verify the deployment and reference these values in later steps or other projects.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_ljvh9876)

---

## Customizing my S3 Bucket

For my project extension, I visited the official Terraform documentation to find the correct syntax and options for customizing an AWS S3 bucket using Terraform. The documentation shows how the aws_s3_bucket resource is defined, what arguments and settings are available, and which ones are required versus optional. It also includes example code, explanations of each configuration block, and best-practice guidance for things like encryption, versioning, public access settings, and tagging so I can confidently update my main.tf file without guessing.

I chose to customize my bucket by adding tags, specifically Environment = "Dev", because tags help organize and identify cloud resources based on their purpose or environment. This is especially useful when managing multiple resources, environments, or projects, as it makes filtering, cost tracking, and governance much easier over time.

When I launch my bucket, I can verify my customization by checking the S3 bucket’s details in the AWS Management Console and confirming that the Environment tag is applied with the value set to Dev.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_ffe757cd3)

---

## Terraform commands

I ran terraform init to initialize my Terraform project and prepare the working directory for use. This command downloads and installs the required provider plugins, such as the AWS provider, so Terraform can communicate with my cloud environment. It also sets up the backend configuration and prepares Terraform to track state and run future commands. Running terraform init is a required first step because it ensures the project is correctly configured before planning or applying any infrastructure changes.

Next, I ran terraform plan to preview the changes Terraform intends to make to my AWS environment based on the configuration in main.tf. This command compares the desired state defined in my Terraform files with the current state of my infrastructure and generates an execution plan showing what resources will be created or modified. Running terraform plan allows me to safely review the S3 bucket configuration, including tags and settings, and confirm everything looks correct before applying the changes and affecting real cloud resources.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_3g4h5i6j)

---

## AWS CLI and Access Keys

When I tried to plan my Terraform configuration, I received an error message that says “No valid credential sources found” because Terraform could not find any AWS credentials on my computer to authenticate with AWS. Since my access key and secret key were not configured yet, Terraform had no way to verify my identity or get permission to create resources in my AWS account. Setting up AWS credentials through the AWS CLI fixes this by giving Terraform a valid credential source it can use to connect to AWS and run the plan successfully.

To resolve my error, first I installed the AWS CLI, which is a command-line tool that allows me to interact with and manage AWS services directly from my local computer. It provides a secure way to authenticate with AWS using access keys and run commands without relying on the AWS Management Console. Installing the AWS CLI is important because Terraform uses it as a credential source to authenticate with AWS, enabling Terraform to create and manage resources such as the S3 bucket from my local environment.

I set up AWS access keys to securely authenticate my local machine with my AWS account so Terraform can interact with AWS services on my behalf. The access key and secret key act as credentials that prove my identity and define what permissions I have. By configuring these keys through the AWS CLI, I provided Terraform with a valid way to connect to AWS, allowing it to plan and create resources like the S3 bucket from my local environment.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_7j8k9l0m)

---

## Lanching the S3 Bucket

I ran terraform apply to execute the changes defined in my Terraform configuration and turn the infrastructure code in main.tf into real AWS resources. This command takes the execution plan that Terraform generated and carries out those actions, such as creating the S3 bucket and applying its configuration and tags.

Running terraform apply will affect my AWS account by actually provisioning and managing resources inside it. Terraform will create the S3 bucket in AWS, track it in the Terraform state, and take responsibility for managing future changes to that resource based on updates to the configuration.

The sequence of running terraform init, terraform plan, and terraform apply is crucial because each command prepares and validates the next step. terraform init initializes the project by setting up the working directory and downloading the required provider plugins so Terraform can communicate with AWS. terraform plan then reviews the configuration, compares the desired state with the current AWS environment, and shows exactly what changes will be made. This allows errors to be caught before anything is created. Finally, terraform apply executes the approved plan and makes real changes in the AWS account by creating and managing the defined resources. Running these commands in order ensures the deployment process is safe, predictable, and well-controlled.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_1q2w3e4r)

---

## Uploading an S3 Object

I created a new resource block to add an image to my S3 bucket using terraform.

We need to run terraform apply again because the Terraform configuration has changed. After adding the S3 object resource to main.tf, Terraform must re-evaluate the desired state and apply the new instructions. Running terraform apply allows Terraform to create the new object in the existing S3 bucket and update its state file so it can track and manage that file going forward. Without running apply again, the changes in the configuration would exist only in code and would not be reflected in the actual AWS environment.

To validate that I’ve updated my configuration successfully, I checked the results after running terraform apply and confirmed that Terraform reported the S3 object was created without errors. I then verified the upload by opening the AWS Management Console, navigating to my S3 bucket, and confirming that the file appears inside the bucket. Seeing the object listed in S3 confirmed that the updated Terraform configuration worked and that the file is now being managed by Terraform.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-devops-terraform1_9o0p1a2s)

---

---
