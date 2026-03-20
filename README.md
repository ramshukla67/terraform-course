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

**proj03-import-lambda** is a Terraform configuration that shows how to use Terraform's `import` block to adopt existing AWS resources that were created outside of Terraform. This is useful for:
- Bringing legacy infrastructure under Terraform management
- Migrating existing resources into Terraform without recreating them
- Building Terraform configurations from currently deployed infrastructure

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
- AWS CLI configured with appropriate credentials
- An existing Lambda function and related resources in your AWS account (named `manually-created-lambda`)
- AWS region: `eu-west-1`

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

## proj03-import-lambda

This project demonstrates Terraform's resource import functionality by importing a manually-created AWS Lambda function and its associated infrastructure into Terraform management.

### What Gets Imported

The project imports three types of AWS resources:

1. **Lambda Function** (`aws_lambda_function.this`)
   - Function name: `manually-created-lambda`
   - Runtime: Node.js 18.x
   - Handler: `index.handler`
   - Includes Function URL for public HTTP access (no authorization required)
   - CloudWatch logging enabled

2. **IAM Role** (`aws_iam_role.lambda_execution_role`)
   - Role name: `manually-created-lambda-role-apq5o1ty`
   - Service: Lambda execution
   - Trust relationship: Allows Lambda service to assume the role

3. **IAM Policy & Attachment** (`aws_iam_policy.lambda_execution`)
   - Provides CloudWatch Logs permissions
   - Allows creating log groups, streams, and writing log events
   - Scoped to the Lambda's specific log group

4. **CloudWatch Log Group** (`aws_cloudwatch_log_group.lambda`)
   - Log group: `/aws/lambda/manually-created-lambda`
   - Used for storing Lambda execution logs

### Project Structure

```
proj03-import-lambda/
├── provider.tf              # AWS provider configuration with required versions
├── iam.tf                   # IAM role and policy imports & definitions
├── lambda.tf                # Lambda function, URL, and code archive
├── cloudwatch.tf            # CloudWatch log group import
├── outputs.tf               # Output: Lambda function URL
├── build/
│   └── index.mjs            # Lambda handler function (Node.js 18.x)
├── .terraform.lock.hcl      # Terraform provider lock file
└── lambda.zip               # Generated zip archive of Lambda code
```

### How It Works

1. **Import Blocks**: Each file begins with `import` blocks that reference existing AWS resources by their IDs
2. **Data Sources**: Policy documents are generated using `data.aws_iam_policy_document` to ensure consistency
3. **Code Archiving**: The `archive_file` data source automatically zips the Lambda code
4. **Outputs**: The Lambda Function URL is exported for easy access

### Usage

To import these resources into your Terraform state:

```bash
cd proj03-import-lambda
terraform init
terraform plan   # Review the imported resources
terraform apply  # Bring resources under Terraform management
```

Once imported, you can modify the Terraform configuration and run `terraform apply` to manage these resources like any other Terraform-created resource.

### Key Files Explained

**provider.tf**: Configures AWS provider for `eu-west-1` region with Terraform version constraints (1.7+) and required providers (AWS 5.0+, Archive 2.0+).

**iam.tf**: Defines IAM role, policy, and their relationship. Includes `import` blocks to adopt existing role and policy into Terraform state.

**lambda.tf**: Contains the Lambda function definition, Function URL configuration, and code archiving logic. The `import` block references the existing Lambda function by name.

**cloudwatch.tf**: Creates or imports the CloudWatch log group where Lambda logs are stored.

**build/index.mjs**: Simple Node.js 18.x handler that returns a welcome message.

**outputs.tf**: Exports the Lambda Function URL for convenient access to the deployed function.

### Notes

- The import IDs must match existing resources in your AWS account
- Once imported, these resources are managed by Terraform and changes should go through Terraform workflows
- The Lambda code in `build/index.mjs` can be modified and redeployed by running `terraform apply`
