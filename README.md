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

## Overview

This repository contains practical Terraform examples demonstrating various AWS infrastructure patterns and best practices.

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

## Prerequisites

- Terraform 0.12 or higher installed
- AWS account with appropriate permissions (IAM credentials)
- AWS CLI configured with credentials or environment variables
- Basic understanding of AWS networking concepts (VPC, subnets, etc.)

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

```bash
terraform init
terraform plan
terraform apply
terraform output
```

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

# Benefits IaC - VPC Deployment

Terraform configuration for deploying AWS Virtual Private Cloud (VPC) infrastructure using Infrastructure-as-Code principles.

## Tech Stack

- **Terraform** - Infrastructure-as-Code tool for provisioning cloud resources
- **AWS** - Cloud provider (VPC services)
- **HCL** - HashiCorp Configuration Language

## Installation and Setup

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd benefits-iac
   ```

2. **Initialize Terraform working directory**
   ```bash
   terraform init
   ```

3. **Configure AWS credentials**
   - Export AWS credentials as environment variables:
     ```bash
     export AWS_ACCESS_KEY_ID="your-access-key"
     export AWS_SECRET_ACCESS_KEY="your-secret-key"
     export AWS_DEFAULT_REGION="us-east-1"
     ```
   - Or configure via `~/.aws/credentials`

4. **Review the execution plan**
   ```bash
   terraform plan
   ```

5. **Deploy the VPC infrastructure**
   ```bash
   terraform apply
   ```

## Usage Examples

### Deploy VPC to specific region

Modify `vpc.tf` or pass variables during apply:

```bash
terraform apply -var="aws_region=us-west-2"
```

### Destroy VPC infrastructure

When no longer needed, clean up resources:

```bash
terraform destroy
```

### View current state

```bash
terraform show
```

## Architecture Overview

The project structure is organized as follows:

- **01-benefits-iac/** - Main directory containing IaC configurations
  - **vpc.tf** - Terraform configuration file defining VPC resources, including VPC creation, subnet definitions, internet gateways, route tables, and security group configurations

## File Descriptions

### vpc.tf

This is the primary Terraform configuration file that defines the VPC infrastructure. It contains resource definitions for:
- VPC creation and configuration
- Public and private subnets
- Internet Gateway attachment
- Route table associations
- Network ACLs and security groups
- NAT Gateway configuration (if applicable)

## Key Features

- **Infrastructure as Code** - Version-controlled cloud infrastructure definitions
- **Modular Design** - Reusable Terraform configurations for VPC deployment
- **AWS-native** - Leverages AWS managed services for networking
- **Declarative Configuration** - Define desired state; Terraform handles implementation

## Getting Started with Terraform

For first-time users:

1. Review the `vpc.tf` file to understand the infrastructure design
2. Run `terraform fmt` to format code according to Terraform standards
3. Use `terraform validate` to check configuration syntax
4. Always review `terraform plan` output before applying changes
5. Store `terraform.tfstate` securely (consider remote backends like S3)

## Common Workflows

### Initialize and deploy

```bash
terraform init
terraform plan
terraform apply
```

### Update infrastructure

```bash
# Modify vpc.tf
terraform plan  # Review changes
terraform apply
```

### Clean up resources

```bash
terraform destroy
```

## Best Practices

- Always review `terraform plan` output before applying
- Use version control for all `.tf` files
- Store sensitive credentials in environment variables or AWS Secrets Manager
- Implement remote state management for team collaboration
- Tag resources for cost tracking and organization

## Troubleshooting

- **Authentication errors** - Verify AWS credentials are configured correctly
- **Resource conflicts** - Check if VPC or resources already exist in the region
- **Permission denied** - Ensure IAM user has necessary permissions (ec2:*, vpc:*)
- **State conflicts** - Clear local state with `terraform destroy` if needed

## References

- [Terraform AWS VPC Documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/vpc)
- [AWS VPC Documentation](https://docs.aws.amazon.com/vpc/)
- [Terraform Getting Started](https://www.terraform.io/intro/index.html)

# Terraform Infrastructure Learning Projects

A collection of Terraform modules for learning and implementing AWS infrastructure components.

## Projects

### 06-resources: VPC with EC2 Web Server

A complete AWS infrastructure setup demonstrating VPC networking and compute resource provisioning.

**Deployed Resources:**
- VPC with CIDR block 10.0.0.0/16
- Public subnet (10.0.0.0/24)
- Internet Gateway with route to 0.0.0.0/0
- Route table associated with the subnet
- EC2 t2.micro instance running NGINX with public IP assignment
- Security Group allowing HTTP (80) and HTTPS (443) ingress from anywhere

**Implementation Checklist:**
1. ✓ Deploy a VPC and a subnet
2. ✓ Deploy an internet gateway and associate it with the VPC
3. ✓ Setup a route table with a route to the IGW and associate it with the subnet
4. ✓ Deploy an EC2 instance inside of the created subnet and associate a public IP
5. ✓ Associate a security group that allows public ingress
6. ✓ Change the EC2 instance to use a publicly available NGINX AMI
7. ✓ Destroy everything

**Quick Start:**
```bash
cd 06-resources
terraform init
terraform plan
terraform apply
terraform destroy  # Clean up resources
```

**Configuration:**
- **Region:** eu-west-1 (Ireland)
- **Terraform Version:** >= 1.7.0, < 2.0.0
- **AWS Provider Version:** ~> 5.0
- **Instance Type:** t2.micro (eligible for free tier)
- **AMI:** NGINX AMI (ami-0dfee6e7eb44d480b)

# Terraform Examples Repository

## Module: 07-data-sources

### Purpose

This module demonstrates how to use Terraform data sources to dynamically query and retrieve information about existing AWS resources without managing them directly.

### Key Concepts

- **AWS Data Sources**: Query existing AWS resources (AMIs, VPCs, availability zones, caller identity)
- **Filtering**: Use filters to locate specific resources (e.g., Ubuntu 22.04 AMI)
- **Dynamic Configuration**: Reference queried data in resource definitions
- **Information Retrieval**: Extract account ID, region, and infrastructure details

### Contents

- **provider.tf**: Terraform version constraints and AWS provider configuration
  - Terraform version >= 1.7.0, < 2.0.0
  - AWS provider version ~> 5.0
  - Configured for eu-west-1 region

- **compute.tf**: Data sources and compute resources
  - `aws_ami`: Dynamically retrieves the most recent Ubuntu 22.04 HVM image
  - `aws_caller_identity`: Gets current AWS account information
  - `aws_region`: Retrieves current region details
  - `aws_vpc`: Queries VPCs by tags (e.g., Env = "Prod")
  - `aws_availability_zones`: Lists available zones in the region
  - `aws_iam_policy_document`: Defines S3 bucket policy for public read access
  - EC2 instance using dynamically discovered AMI
  - S3 bucket resource

### Example Outputs

The module exports several outputs demonstrating data source usage:

- `iam_policy`: JSON-formatted IAM policy for S3 public access
- `azs`: Available zones information
- `prod_vpc_id`: VPC ID of the Prod environment
- `ubuntu_ami_data`: Ubuntu 22.04 AMI ID
- `aws_caller_identity`: Current AWS account details
- `aws_region`: Current region information

### Learning Outcomes

After studying this module, you will understand:
- How to query existing AWS infrastructure using data sources
- How to filter resources by attributes and tags
- How to reference data source outputs in resource configurations
- How to work with AWS account and region information
- Best practices for dynamic resource selection
