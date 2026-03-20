# Mastering Terraform: From Beginner to Expert

### Course link (with a big discount 🙂): https://www.lauromueller.com/courses/mastering-terraform

**Check my other courses:** 

- 👉 The Complete Docker and Kubernetes Course: From Zero to Hero - https://www.lauromueller.com/courses/docker-kubernetes
- 👉 The Definitive Helm Course: From Beginner to Master - https://www.lauromueller.com/courses/definitive-helm-course
- 👉 Mastering GitHub Actions: From Beginner to Expert - https://www.lauromueller.com/courses/mastering-github-actions
- 👉 Write better code: 20 code smells and how to get rid of them -  https://www.lauromueller.com/courses/writing-clean-code

Welcome everyone! I'm very happy to see you around, and I hope this repository brings lots of value for those learning more about Terraform. Make sure to check the link above for a great discourse on the course in Udemy, where I not only provide theoretical explanations around all the concepts here, but also go in details through the entire coding of the examples in this repository.

Here are a few tips for you to best navigate the contents of this repository:
1. The `exercises` folder contains descriptions for all the implemented exercises. You can use it as a guide to try to implement them by yourself before following the solution recordings.
2. The `projects` folder contains six bigger projects that you can also tackle for an extra challenge 🙂 The solutions for these projects are implemented within their respective folders, **except for project 00, which is implemented inside of the folder `06-resources`**.
3. The other folders roughly mirror the structure of the course, but there are some course sections that span more than one folder.

Happy learning! 🚀

## Additional Links and Courses:

**Other repositories included in the course:**
* Networking Module Repository - https://github.com/lm-academy/terraform-aws-networking-tf-course
* Terraform Cloud VCS Integration Repository - https://github.com/lm-academy/terraform-course-example-terraform-cloud

**Other courses I published in Udemy:**
* Mastering GitHub Actions: From Beginner to Expert - https://www.lauromueller.com/courses/mastering-github-actions
* Write Clean Code: 20 Code Smells and How to Get Rid of Them - https://lauromueller.com/courses/writing-clean-code/

## Projects

This repository contains a comprehensive collection of hands-on AWS and Terraform projects designed to build practical infrastructure-as-code skills:

### Project 0: Deploying an NGINX Server in AWS

**File:** `projects/proj00-vpc-ec2.md`

Learn to deploy an NGINX server in AWS by creating a new VPC, configuring public and private subnets, and launching an EC2 instance. This project covers VPC setup, security groups, EC2 management, and resource tagging using Terraform.

### Project 1: Deploying a Static Website with S3

**File:** `projects/proj01-s3-static-website.md`

Gain hands-on experience with Amazon S3 and Terraform by hosting a static website. This project covers bucket creation, access management, bucket policies, and infrastructure-as-code principles.

### Project 2: Managing IAM Users and Roles with Terraform

**File:** `projects/proj02-iam-users.md`

Master AWS Identity and Access Management (IAM) by automating user and role creation with Terraform. This project integrates YAML-based configuration with Terraform to manage users, roles, policies, and secure role assumption.

### Project 3: Importing Lambda Resources into Terraform

**File:** `projects/proj03-import-lambda.md`

Learn to import existing AWS resources into Terraform code. This project focuses on importing Lambda functions, understanding infrastructure components, and leveraging Terraform's code generation capabilities.

### Project 4: Creating an RDS Module

**File:** `projects/proj04-rds-module.md`

Build a reusable, production-grade RDS module for Terraform. This project emphasizes module design patterns, variable validation, security best practices, and creating reusable infrastructure components.

### Project 5: Enabling OIDC for AWS Authentication from Terraform Cloud

**File:** `projects/proj05-tf-cloud-oidc.md`

Set up OpenID Connect (OIDC) authentication between Terraform Cloud and AWS for secure, keyless authentication. This project covers identity providers, role trust relationships, and multi-workspace configurations.
