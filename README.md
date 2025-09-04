<!-- Project metadata -->
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)
![Duration](https://img.shields.io/badge/Time-30min-blue?style=for-the-badge)
![NextWork](https://img.shields.io/badge/NextWork-Project-orange?style=for-the-badge&logo=terraform)

<!-- Technologies -->
![Terraform](https://img.shields.io/badge/Terraform-v1.9-7B42BC?style=for-the-badge&logo=terraform)
![AWS](https://img.shields.io/badge/AWS-S3-FF9900?style=for-the-badge&logo=amazonaws)
![AWS CLI](https://img.shields.io/badge/AWS-CLI-232F3E?style=for-the-badge&logo=amazonaws)

<!-- Concepts -->
![IaC](https://img.shields.io/badge/Infrastructure_as_Code-IaC-green?style=for-the-badge)
![Cloud](https://img.shields.io/badge/Cloud-AWS-blue?style=for-the-badge)
![Automation](https://img.shields.io/badge/Automation-Terraform-yellow?style=for-the-badge)

<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Create S3 Buckets with Terraform

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-devops-terraform1)

**Author:** Bradley Davel  
**Email:** bradleydavel123@gmail.com

---

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Introducing Today's Project!

In this project, I will demonstrate how to set up and use Terraform with AWS S3.

Get ready to:
 1. Install and configure Terraform
 2. Configure your AWS credentials in the terminal
 3. Create and manage S3 buckets with Terraform
 4. Upload files to S3 using Terraform

The goal is to:
-Gain hands-on experience with Infrastructure as Code (IaC).
-Learn how to define and provision AWS resources declaratively.
-Understand how Terraform tracks and manages infrastructure changes.
-Build a foundation for automating cloud infrastructure deployments.

### Tools and concepts

Services I used were AWS S3 for object storage and the AWS CLI to configure my credentials and interact with my account. Key concepts I learnt include Infrastructure as Code (IaC) with Terraform, how to define infrastructure using providers and resource blocks, how to enforce security best practices with public access blocks, and how to manage not only infrastructure but also objects inside S3. I also learnt the importance of initializing, planning, and applying in Terraform to ensure my configuration matches my AWS environment.

### Project reflection

This project took me approximately 30 minutes to complete. The most challenging part was resolving the AWS credentials error, since Terraform couldn’t access my account until I configured the AWS CLI and access keys properly. It was most rewarding to see my S3 bucket created and my image uploaded successfully through Terraform, proving that I can automate real AWS infrastructure with just a few lines of code.

I chose to do this project today because I wanted to strengthen my hands-on skills with Terraform and AWS S3, building on what I’ve been studying. I chose to do this project today because it was a quick, practical way to practice infrastructure as code, troubleshoot real errors like credential setup, and gain confidence in automating cloud resources end-to-end.

---

## Introducing Terraform

Terraform is a tool that helps you build and manage your cloud infrastructure using code.

Instead of setting up resources manually in the AWS console or CLI, you write a script that tells Terraform exactly what you want in your cloud infrastructure, like servers, databases, and networks. Terraform then automatically builds all of this for you, using your script as a blueprint.

Infrastructure as Code (IaC) is the practice of describing your cloud setup (like your servers, storage, networks) in plain text files instead of clicking through a web console. When you run those files, the cloud builds everything exactly as you've written it written. Because the description lives in code, you can version-control it, share it with teammates, and recreate the same environment any time you need.

Terraform is a popular IaC tool because it understands all the big cloud providers - AWS, Azure, and Google Cloud. In the same configuration file, you can tell Terraform to create resources across any or all of them. Terraform's syntax is also designed to read almost like English, so you can pick it up quickly while still modeling complex setups once you’re ready.

Terraform uses configuration files (like main.tf) to define and manage infrastructure. These files describe the desired state of your infrastructure, and Terraform figures out how to achieve that state. main.tf is a central file in a Terraform project.

It's where you write down what you want your infrastructure to look like, using Terraform's language. Think of it as the blueprint for building your cloud resources.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_9i0j1k2l)

---

## Configuration files

My Terraform configuration is defined using blocks that describe what to build and how to secure it. I start with a provider block to set AWS as my cloud and eu-west-2 as the region. Then I add a resource block for an S3 bucket, giving it a globally unique name. To keep it secure, I define another resource block that applies a public access block, ensuring no ACLs or policies accidentally make the bucket public. The advantage of doing this is that my infrastructure is consistent, repeatable, and version-controlled, with security built in by default, instead of relying on manual console setup.

### My main.tf configuration has three blocks

The first block indicates the provider I’m using, which is AWS, and sets the deployment region. The second block provisions an S3 bucket with a globally unique name that Terraform will create in my AWS account. The third block manages the public access settings of that bucket, enforcing restrictions so it stays private and secure. This approach makes my infrastructure consistent, repeatable, and secure by default, while also allowing me to track every change in version control.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_ljvh9876)

---

## Customizing my S3 Bucket

For my project extension, I visited the official Terraform documentation to explore additional features I could add beyond just creating a bucket. The documentation shows detailed examples of how to configure advanced settings such as enabling versioning, setting lifecycle rules for automatic file expiration, and applying tags for better resource management. By following these guidelines, I can extend my configuration to make the S3 bucket more resilient, organized, and production-ready, while learning how to leverage Terraform’s flexibility to manage more complex infrastructure.

I chose to customise my bucket by adding tags, specifically setting the Environment tag to "Dev", because tagging makes it easier to organise, filter, and manage resources within AWS. Tags are especially useful when working with multiple environments (Dev, Test, Prod) or when tracking costs by project or team. When I launch my bucket, I can verify my customization by checking the Tags tab in the AWS Management Console for the S3 bucket, or by running the AWS CLI command aws s3api get-bucket-tagging --bucket <bucket-name> to confirm that the Environment=Dev tag has been applied.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_ffe757cd3)

---

## Terraform commands

Terraform init is the first command you run for a new Terraform project. It sets up your project by:

-Downloading necessary plugins: It grabs the providers which handle the connection with cloud services like AWS.

-Setting up the backend: Terraform needs to set up a backend that keep its own record of your infrastructure, so future commands can see what has already been created.

-Preparing modules: If your setup uses reusable code blocks (called modules) this is where the code is downloaded from their source to replace placeholders in your code.

-Creating a lock file: This file keeps track of the versions of everything Terraform is using, making sure that everyone on your team is using the same setup to avoid inconsistencies.

'terraform plan' previews the changes Terraform will make to your infrastructure. It compares your current configuration (.tf files) against the real state of your AWS environment and then shows you:

-What resources will be created (marked with a +)
-What resources will be changed (marked with a ~)
-What resources will be destroyed (marked with a -)

The key advantage is that it lets you review changes safely before applying them, so you don’t accidentally create or delete resources you didn’t intend to.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_3g4h5i6j)

---

## AWS CLI and Access Keys

When I tried to plan my Terraform configuration, I received an error message that says “No valid credential sources found” because Terraform couldn’t locate my AWS credentials. Since I’m not running this from an EC2 instance with a role, Terraform needs access keys from my local machine to authenticate with AWS. Without those credentials, it cannot connect to my account to preview or create resources.

To resolve my error, first I installed AWS CLI, which is a command-line tool provided by Amazon that lets me interact with AWS services directly from my terminal. It allows me to configure credentials, run commands to manage resources (like S3 buckets, EC2 instances, IAM users), and test connectivity to my AWS account. By setting up AWS CLI, Terraform can use the stored credentials to authenticate and build the infrastructure I define in my configuration.

I set up AWS access keys to give Terraform a secure way to authenticate with my AWS account. The access key ID and secret access key act like a username and password pair for programmatic access, allowing Terraform to create, update, and manage resources on my behalf. Without these keys, Terraform has no way to connect to AWS, so configuring them ensures my infrastructure code can actually be applied.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_7j8k9l0m)

---

## Lanching the S3 Bucket

I ran terraform apply to actually provision the infrastructure I described in my configuration. Running terraform apply will affect my AWS account by creating, updating, or deleting resources so that my real environment matches my code. In my case, this command creates the S3 bucket I defined in main.tf, turning my configuration into a live resource inside AWS.

If you run terraform apply before terraform init, you would run into an error because terraform init needs to set up your project first by downloading necessary plugins and setting up the state file, which is a file Terraform uses to track the current state of your infrastructure.

There actually aren't any errors if you skip terraform plan. This is because terraform apply will automatically run a plan and ask for confirmation before making any changes. But, skipping the explicit terraform plan means you might miss reviewing these changes in detail. It's best practice to run a plan to catch any potential errors or unexpected results before they affect your live infrastructure.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_1q2w3e4r)

---

## Uploading an S3 Object

I created a new resource block to upload an object (image.png) into my S3 bucket because the bucket alone only provides storage—it doesn’t contain any files until I explicitly add them. By defining an aws_s3_object resource, I can automate the upload of files directly from my local machine into the bucket as part of my Terraform configuration. This shows how Terraform can not only provision infrastructure but also manage the content inside it, making my project more practical and complete.

I need to run terraform apply again because I updated my configuration by adding a new resource block for the S3 object. Terraform only makes changes when I apply them, so re-running the command ensures my new code is executed and the image file is uploaded into the bucket. Without applying again, the changes exist only in my configuration file and won’t be reflected in my AWS environment.

To validate that I’ve updated my configuration successfully, I checked the S3 bucket in the AWS Management Console and confirmed that image.png appeared under the bucket’s objects. I could also verify the upload by running the AWS CLI command aws s3 ls s3://<bucket-name> to list the contents and ensure my file was present. This confirmed that Terraform not only created the bucket but also uploaded my object as expected.

![Image](http://learn.nextwork.org/sparkling_indigo_heroic_bat/uploads/aws-devops-terraform1_9o0p1a2s)

---

---
