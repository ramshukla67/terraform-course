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

# Terraform Cloud OIDC Integration Projects

This repository contains Terraform projects demonstrating OIDC (OpenID Connect) integration between Terraform Cloud and various cloud providers.

## Project 05: Terraform Cloud to AWS OIDC

### Overview

The `proj05-tf-cloud-oidc` project establishes a secure, keyless authentication mechanism between Terraform Cloud and AWS using OpenID Connect. This eliminates the need for static AWS credentials in Terraform Cloud.

### Architecture

The project implements the following components:

- **AWS IAM OpenID Connect Provider**: Configured to trust Terraform Cloud's identity provider (app.terraform.io)
- **IAM Role**: `terraform-cloud-automation-admin` role that Terraform Cloud can assume via OIDC
- **Role Policy**: Administrator access attached to the automation role
- **S3 Bucket**: Example resource managed by Terraform Cloud

### Files

- `provider.tf` — Terraform and provider configuration
  - Specifies Terraform Cloud backend (organization: LauroMueller, workspace: terraform-cli)
  - Configures AWS provider for eu-west-1 region
  - Requires Terraform ~> 1.7, AWS provider ~> 5.0, TLS provider ~> 4.0

- `oidc.tf` — OIDC and IAM setup
  - Retrieves TLS certificate from Terraform Cloud for OIDC provider setup
  - Creates AWS IAM OpenID Connect provider for Terraform Cloud
  - Defines assume role policy document with conditions for audience and subject validation
  - Creates IAM role for Terraform Cloud automation with admin access
  - Includes import blocks for managing existing resources

- `s3.tf` — S3 bucket resource example
  - Creates an S3 bucket as a sample Terraform Cloud managed resource

- `variables.tf` — Input variables
  - `terraform_cloud_hostname`: Terraform Cloud hostname (default: app.terraform.io)
  - `terraform_cloud_audience`: OIDC audience claim (default: aws.workload.identity)
  - `admin_role_workspaces`: List of Terraform Cloud workspaces authorized to assume the admin role
  - `admin_role_project`: Terraform Cloud project name for role assumption authorization

- `terraform.tfvars` — Variable values
  - Specifies authorized workspaces: terraform-cli, terraform-cli2
  - Specifies project: terraform-oidc

- `.terraform.lock.hcl` — Dependency lock file
  - Locks AWS provider v5.46.0 and TLS provider v4.0.5

### Prerequisites

- Terraform >= 1.7
- AWS account with appropriate permissions
- Terraform Cloud account with organization "LauroMueller"
- Existing Terraform Cloud workspaces: terraform-cli and terraform-cli2

### Setup

1. Ensure your Terraform Cloud organization and workspaces exist
2. Update `terraform.tfvars` with your specific workspace and project names
3. Run `terraform init` to initialize the backend and download providers
4. Run `terraform plan` to review the resources to be created
5. Run `terraform apply` to establish the OIDC integration

### Security Considerations

- The `terraform-cloud-automation-admin` role has full AWS administrative access; restrict as needed
- OIDC conditions validate both the audience and workspace subject claims
- Supported workspaces are strictly defined in the assume role policy
