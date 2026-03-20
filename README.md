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

This example shows how to leverage certified public modules from the Terraform AWS Modules project to build a complete, production-ready infrastructure setup with minimal code duplication and best practices built-in.

## Architecture

The configuration deploys the following AWS resources:

- **VPC (Virtual Private Cloud)**: Configured with public and private subnets across multiple availability zones
- **EC2 Instance**: An Ubuntu 22.04 t2.micro instance deployed in a public subnet
- **Security Groups**: Default security group for the VPC managing ingress/egress rules

## Files

### Prerequisites

- Terraform >= 1.7
- AWS CLI configured with appropriate credentials
- Access to eu-west-1 region

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

## Project Structure

```
13-local-modules/
├── modules/
│   └── networking/          # Reusable VPC and Subnet module
│       ├── vpc.tf           # Core VPC, subnet, IGW, and routing resources
│       ├── variables.tf     # Input variables with validation
│       ├── outputs.tf       # Module outputs (VPC ID, subnet info)
│       ├── providers.tf     # Provider configuration
│       ├── README.md        # Module documentation
│       ├── LICENSE          # MIT License
│       └── examples/
│           └── complete/    # Complete usage example
├── networking.tf            # Module instantiation
├── compute.tf               # EC2 instance in private subnet
├── outputs.tf               # Root outputs
├── providers.tf             # AWS provider configuration
└── .terraform.lock.hcl      # Dependency lock file
```

### How It Works

1. **Import Blocks**: Each file begins with `import` blocks that reference existing AWS resources by their IDs
2. **Data Sources**: Policy documents are generated using `data.aws_iam_policy_document` to ensure consistency
3. **Code Archiving**: The `archive_file` data source automatically zips the Lambda code
4. **Outputs**: The Lambda Function URL is exported for easy access

## Usage

### Key Files Explained

**provider.tf**: Configures AWS provider for `eu-west-1` region with Terraform version constraints (1.7+) and required providers (AWS 5.0+, Archive 2.0+).

**iam.tf**: Defines IAM role, policy, and their relationship. Includes `import` blocks to adopt existing role and policy into Terraform state.

**lambda.tf**: Contains the Lambda function definition, Function URL configuration, and code archiving logic. The `import` block references the existing Lambda function by name.

**cloudwatch.tf**: Creates or imports the CloudWatch log group where Lambda logs are stored.

**build/index.mjs**: Simple Node.js 18.x handler that returns a welcome message.

**outputs.tf**: Exports the Lambda Function URL for convenient access to the deployed function.

## Notes

- The `.terraform.lock.hcl` file ensures reproducible builds by locking provider versions
- All resources are tagged with the project name for easy identification and billing
- The t2.micro instance type is suitable for testing and development; use larger instances for production workloads

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

## Key Concepts

**Remote State Benefits:**
- Centralized state management accessible by multiple team members
- State locking to prevent concurrent modifications
- Secure storage in AWS S3 with encryption options
- State versioning and audit trail capabilities
- Separation of concerns between development and production environments

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

# Terraform Object Validation Example

This project demonstrates advanced Terraform validation patterns including object validation, postconditions, and check assertions in Terraform 1.7+.

### 1. Postcondition Validation

**Instance Type Validation** (compute.tf)
```hcl
postcondition {
  condition     = contains(local.allowed_instance_types, self.instance_type)
  error_message = "Self invalid instance type"
}
```
Enforces that launched instances must use approved types (t2.micro, t3.micro).

**Subnet AZ Validation** (networking.tf)
```hcl
postcondition {
  condition     = contains(data.aws_availability_zones.available.names, self.availability_zone)
  error_message = "Invalid AZ"
}
```
Ensures each subnet is created in a valid availability zone.

### 2. Check Blocks

**Cost Center Check** (compute.tf)
Verifies that the EC2 instance has a CostCenter tag, helping enforce organizational tagging policies.

**High Availability Check** (networking.tf)
Ensures subnets are distributed across multiple AZs to prevent single-zone deployments.

## Configuration

## Variables

### Provider Configuration

- **Region**: eu-west-1 (Ireland)
- **Terraform Version**: ~> 1.7
- **AWS Provider Version**: ~> 5.0

## Validation Rules Summary

| Component | Validation Rule | Enforcement |
|-----------|-----------------|-------------|
| EC2 Instance | Allowed instance types (t2.micro, t3.micro) | Postcondition (hard fail) |
| EC2 Instance | CostCenter tag must exist and not be empty | Check assertion (warning) |
| Subnets | Must exist in a valid availability zone | Postcondition (hard fail) |
| Subnets | Must be distributed across 2+ AZs | Check assertion (warning) |

## Testing Validation

To test the validation rules:

1. **Instance Type Violation**: Modify `variables.tf` to use an unauthorized instance type (e.g., "t2.small") → applies will fail at postcondition check
2. **Missing Tags**: Remove the CostCenter tag from instance tags → check assertion will report a warning
3. **Single AZ Deployment**: Modify the subnet count or AZ logic to deploy to a single AZ → high_availability_check will warn

## Requirements

- Terraform >= 1.0
- AWS Provider >= 5.0
- AWS credentials configured with appropriate permissions

## Example 14: Using External Terraform Modules

This example demonstrates how to use and consume Terraform modules published on the Terraform Registry (Terraform Cloud or similar registries).

### Configuration Details

#### VPC Configuration
- **CIDR Block**: 10.0.0.0/16
- **Name**: 13-local-modules

#### Subnets
1. **Subnet 1** (Private)
   - CIDR: 10.0.0.0/24
   - Availability Zone: eu-west-1a

2. **Subnet 2** (Public)
   - CIDR: 10.0.1.0/24
   - Availability Zone: eu-west-1b
   - Public access enabled

### proj02-iam-users

A Terraform module that provisions AWS IAM users and roles based on a YAML configuration.

#### Features
- **User Management**: Creates IAM users from YAML configuration file (`user-roles.yaml`)
- **Role-Based Access**: Supports four predefined roles:
  - `readonly`: Read-only access to AWS resources
  - `developer`: Full access to VPC, EC2, and RDS
  - `admin`: Administrator access
  - `auditor`: Security audit access
- **Automated Policy Attachment**: Automatically attaches AWS managed policies to roles
- **Login Profiles**: Generates initial login profiles with auto-generated passwords for all users

#### Configuration

Edit `proj02-iam-users/user-roles.yaml` to define users and their roles:

```yaml
users:
  - username: john
    roles: [readonly, developer]
  - username: jane
    roles: [admin, auditor]
  - username: lauro
    roles: [readonly]
```

#### Deployment

```bash
cd proj02-iam-users
terraform init
terraform plan
terraform apply
```

#### Requirements
- Terraform >= 1.7
- AWS Provider >= 5.0
- AWS credentials configured for `eu-west-1` region

#### Outputs
- `passwords`: A map of automatically generated initial passwords for each user (store securely)

# Terraform Learning Course

A comprehensive learning resource for Terraform, covering foundational concepts through advanced patterns.

## Modules

### 08-input-vars-locals-outputs

**Purpose:** Demonstrates Terraform input variables, local values, and outputs in a practical multi-resource setup.

**Key Concepts:**
- **Input Variables** (`variables.tf`):
  - String variables with validation rules
  - Object-type variables with nested structure (ec2_volume_config)
  - Map variables for flexible tagging (additional_tags)
  - Sensitive variables that are not displayed in logs or output
  - Default values and validation blocks

- **Local Values** (`shared-locals.tf`):
  - Simple local variables for project metadata (project, owner, cost center)
  - Computed locals that aggregate values using functions (merge)
  - Referencing other locals within local blocks
  - Using locals with variables to build dynamic tag structures

- **Outputs** (`outputs.tf`):
  - Standard output declarations with descriptions
  - Sensitive output flag to prevent value display
  - Exposing resource attributes (S3 bucket name) for state queries
  - Controlling sensitive data visibility in terraform output

- **Variable Files** (`terraform.tfvars`, `override.tfvars`):
  - Default values using .tfvars files
  - Override behavior and file precedence
  - Different organization strategies for complex configurations

**Resources:**
- `aws_s3_bucket`: S3 bucket with dynamic naming using random ID suffix
- `random_id`: Ensures unique bucket names across deployments
- `aws_ami`: Data source querying Ubuntu 22.04 LTS images

**Configuration:**
- Provider: AWS (eu-west-1), Terraform ~> 1.7.0
- Dependencies: aws ~> 5.0, random ~> 3.0

## 17-workspaces

This directory contains a Terraform configuration demonstrating the use of **Terraform workspaces** for managing multiple environments with a single codebase.

### Environment Configuration

Each environment is defined with a separate `.tfvars` file:

- **dev.tfvars** - Development environment: deploys 1 S3 bucket
- **int.tfvars** - Integration environment: deploys 1 S3 bucket
- **staging.tfvars** - Staging environment: deploys 2 S3 buckets
- **prod.tfvars** - Production environment: deploys 3 S3 buckets

## Key Concepts Demonstrated

- **Module Reusability**: Using public modules reduces code duplication and leverages community best practices
- **Terraform Registry**: How to source and version modules from the official Terraform Registry
- **Locals and Data Sources**: Organizing configuration with local values and querying AWS for dynamic data (e.g., availability zones, AMI)
- **Resource Tagging**: Applying consistent tags across all resources for organization and cost tracking
- **Provider Pinning**: Using version constraints to ensure reproducible infrastructure

# Terraform Projects

A collection of Terraform infrastructure-as-code projects for AWS.

### proj01-s3-static-website

A static website hosting solution using AWS S3 and Terraform.

**What it does:**
- Creates an S3 bucket with a randomized name suffix to ensure uniqueness
- Configures the bucket for public static website hosting
- Uploads two HTML files: `index.html` (homepage) and `error.html` (error page)
- Sets up bucket policy to allow public read access via `s3:GetObject`
- Disables S3 block public access settings to enable public hosting
- Outputs the S3 website endpoint for accessing the site

**Prerequisites:**
- Terraform >= 1.7.0 and < 2.0.0
- AWS credentials configured (region: eu-west-1)
- AWS provider ~> 5.0
- Random provider ~> 3.0

**Usage:**

```bash
cd proj01-s3-static-website
terraform init
terraform plan
terraform apply
```

**Outputs:**
- `static_website_endpoint`: The public endpoint URL of the S3 static website

**Files:**
- `provider.tf`: Terraform version and provider configuration
- `s3.tf`: S3 bucket creation, policy, website configuration, and file uploads
- `outputs.tf`: Output definitions
- `.terraform.lock.hcl`: Dependency lock file (auto-generated by `terraform init`)
- `build/index.html`: Homepage content
- `build/error.html`: Custom error page content

## System Architecture

```mermaid
graph TD
    Root["Root Module (13-local-modules)"]
    Net["Networking Module"]
    VPC["AWS VPC"]
    PublicSN["Public Subnets"]
    PrivateSN["Private Subnets"]
    IGW["Internet Gateway"]
    RTB["Route Table"]
    RTAssoc["Route Table Association"]
    EC2["EC2 Instance"]
    
    Root -->|uses| Net
    Root -->|deploys| EC2
    Net -->|creates| VPC
    VPC -->|contains| PublicSN
    VPC -->|contains| PrivateSN
    PublicSN -->|associated with| RTB
    RTB -->|routes to| IGW
    IGW -->|attached to| VPC
    EC2 -->|deployed in| PrivateSN
```

## 02-hcl Directory

This directory contains HCL (HashiCorp Configuration Language) examples demonstrating core Terraform constructs:

## File Structure

- **provider.tf**: Terraform version and AWS provider configuration
- **data.tf**: Local values including project name
- **networking.tf**: VPC and subnet resources using `for_each`
- **compute.tf**: EC2 instances using both `count` and `for_each` with AMI data sources
- **variables.tf**: Input variable definitions with validation rules
- **terraform.tfvars**: Example variable values

### Use Cases

These examples are useful for:
- Learning HCL syntax and structure
- Understanding Terraform resource and data source management
- Seeing patterns for variable and output organization
- Referencing module composition patterns

## Module: 05-providers

This module demonstrates Terraform provider configuration best practices, including:

- **Provider Declaration**: Configures the AWS provider with version constraints (~> 5.0) and Terraform version constraints (~> 1.0).
- **Multi-Region Setup**: Establishes two AWS provider instances:
  - Default provider for `eu-west-1`
  - Aliased provider `aws.us-east` for `us-east-1`
- **Provider Aliasing**: Shows how to use the `alias` parameter to manage resources across multiple regions or AWS accounts.
- **Resources**: Creates example S3 buckets in both regions, demonstrating explicit provider assignment using the `provider` argument.

# Terraform Multiple Resources Example

This example demonstrates how to provision multiple AWS resources using Terraform's `count` and `for_each` meta-arguments.

### subnet_config

A map of subnet configurations. Each subnet requires:

- `cidr_block` (string): Valid CIDR notation for the subnet

**Validation**: All CIDR blocks must be valid (checked via `cidrnetmask` function)

```hcl
subnet_config = {
  default = {
    cidr_block = "10.0.0.0/24"
  }
  subnet_1 = {
    cidr_block = "10.0.1.0/24"
  }
}
```

### ec2_instance_config_list

A list of EC2 instance configurations (used with `count`). Each instance requires:

- `instance_type` (string): AWS instance type (only t2.micro allowed)
- `ami` (string): AMI selector – either "ubuntu" or "nginx"
- `subnet_name` (string, optional): Name key from subnet_config map (defaults to "default")

**Validation**:
- Only `t2.micro` instance types are allowed
- Only "ubuntu" and "nginx" AMI values are supported

### ec2_instance_config_map

A map of EC2 instance configurations (used with `for_each`). Each instance requires:

- `instance_type` (string): AWS instance type (only t2.micro allowed)
- `ami` (string): AMI selector – either "ubuntu" or "nginx"
- `subnet_name` (string, optional): Name key from subnet_config map (defaults to "default")

**Validation**:
- Only `t2.micro` instance types are allowed
- Only "ubuntu" and "nginx" AMI values are supported

### for_each vs count

This example demonstrates both iteration approaches:

- **count**: Used for instances provisioned from a list. Good when you need numeric indexing.
- **for_each**: Used for both subnets (from a map) and optionally for instances. Better for named resources and map-based configurations.

### AMI Data Sources

The module uses data sources to dynamically retrieve the latest AMIs:

- **Ubuntu**: Canonical-provided Ubuntu 22.04 LTS (owner ID: 099720109477)
- **Nginx**: Bitnami Nginx 1.25.4 on Debian 12

AMI IDs are stored in a local map for easy reference by instances.

### Input Validation

Comprehensive validation ensures:

- Only valid CIDR blocks are accepted
- Only cost-effective t2.micro instances are provisioned
- Only pre-approved AMI types (ubuntu, nginx) can be used

This prevents configuration drift and accidental expensive resources.

## Provider Requirements

- Terraform >= 1.7
- AWS Provider >= 5.0
- Region: eu-west-1

# Terraform Backends Module

This module demonstrates Terraform remote state management using AWS S3 as a backend storage solution.

### `providers.tf`

Configures Terraform requirements and AWS provider:
- Requires Terraform >= 1.7.0
- Specifies AWS provider version ~> 5.0 and random provider ~> 3.0
- Defines S3 backend configuration for remote state storage
- Sets default AWS region to eu-west-1

### `s3.tf`

Defines the S3 bucket resource:
- Creates an S3 bucket with a randomly generated suffix to ensure global uniqueness
- Uses the `random_id` resource to generate a 6-byte hex suffix
- Outputs the created bucket name for reference

### Backend Configuration Files

#### `dev.s3.tfbackend`
Backend configuration for the development environment (for illustration purposes):
```hcl
bucket = "terraform-course-lauromueller-remote-backend"
key    = "04-backends/dev/state.tfstate"
region = "eu-west-1"
```

#### `prod.s3.tfbackend`
Backend configuration for the production environment (for illustration purposes):
```hcl
bucket = "terraform-course-lauromueller-remote-backend"
key    = "04-backends/prod/state.tfstate"
region = "eu-west-1"
```

### `.terraform.lock.hcl`

Lock file containing pinned versions of dependencies:
- AWS Provider: 5.37.0
- Random Provider: 3.6.0

This file ensures consistent provider versions across team members and CI/CD environments.

# Terraform Learning Modules

A comprehensive collection of Terraform examples demonstrating core HCL concepts and expressions.

### 09-expressions

Demonstrates HCL expressions and data transformation techniques in Terraform.

**Contents:**

- **operators.tf** - Basic mathematical, equality, comparison, and logical operators
  - Math operators: `*`, `/`, `+`, `-` (and unary negation)
  - Equality operators: `==`, `!=`
  - Comparison operators: `<`, `<=`, `>`, `>=`
  - Logical operators: `||` (OR), `&&` (AND), `!` (NOT)

- **for-lists.tf** - For-loops for list transformation
  - Creating derived lists through transformation (e.g., doubling numbers)
  - Filtering lists with conditional logic
  - Extracting attributes from list of objects
  - String interpolation within for-loops

- **for-maps.tf** - For-loops for map transformation
  - Creating derived maps by transforming values
  - Filtering maps based on value conditions
  - Maintaining or transforming keys during iteration

- **splat.tf** - Splat syntax for concise attribute extraction
  - Using `[*]` notation to extract attributes from lists of objects
  - Combining splat syntax with value extraction functions
  - Alternative to for-loops for simple attribute collection

- **lists-maps.tf** - Complex transformations combining lists and maps
  - Converting list of objects to map with custom keys
  - Handling complex nested data structures
  - Extracting and transforming data across multiple iterations
  - Grouping values by key (splat operator with `...`)

- **variables.tf** - Variable definitions
  - List of numbers
  - Map of numbers
  - List of objects with firstname/lastname
  - List of user objects with username/role
  - String variable for filtering

- **terraform.tfvars** - Sample input values for demonstration

- **provider.tf** - Terraform version requirement (>= 1.7)

## Running the Example

```bash
cd 09-expressions
terraform init
terraform plan
terraform apply
```

All outputs will be displayed showing the results of various expression transformations.

# 12-public-modules

This directory contains a Terraform configuration example demonstrating the use of public modules from the Terraform Registry to provision AWS infrastructure.

## Directory Structure

```
12-public-modules/
├── provider.tf          # Terraform version and AWS provider configuration
├── shared-data.tf       # Shared locals (project name, common tags)
├── networking.tf        # VPC module configuration with subnets
├── compute.tf           # EC2 instance module configuration
└── .terraform.lock.hcl  # Terraform dependency lock file
```

## Configuration Files

### provider.tf

Defines Terraform and AWS provider requirements:
- Terraform version: ~> 1.7
- AWS provider version: ~> 5.0 (locked at 5.40.0 in the lock file)
- AWS region: eu-west-1

### shared-data.tf

Contains shared local values used across all modules:
- `project_name`: "12-public-modules"
- `common_tags`: Standard tags applied to all resources for tracking and management

### networking.tf

Configures VPC infrastructure using the official terraform-aws-modules/vpc module (v5.5.3):
- **VPC CIDR**: 10.0.0.0/16
- **Public Subnets**: 10.0.128.0/24
- **Private Subnets**: 10.0.0.0/24
- Automatically discovers available AWS availability zones in the region

### compute.tf

Configures EC2 instances using the official terraform-aws-modules/ec2-instance module (v5.6.1):
- **Instance Type**: t2.micro (eligible for AWS free tier)
- **AMI**: Latest Ubuntu 22.04 LTS image from Canonical
- **Placement**: Public subnet of the VPC
- **Security**: Default VPC security group

## Public Modules Used

This configuration leverages certified public modules from the Terraform Registry:

1. **[terraform-aws-modules/vpc/aws](https://registry.terraform.io/modules/terraform-aws-modules/vpc/aws)** v5.5.3
   - Provides a fully-featured VPC with best practices
   - Handles subnets, route tables, and internet gateways
   - Integrates with availability zones for high availability

2. **[terraform-aws-modules/ec2-instance/aws](https://registry.terraform.io/modules/terraform-aws-modules/ec2-instance/aws)** v5.6.1
   - Simplifies EC2 instance creation
   - Handles instance tagging and naming conventions
   - Integrates with VPC for network configuration

### Initialize Terraform

```bash
terraform init
```

This downloads the required modules and providers specified in the configuration.

### Plan Infrastructure

```bash
terraform plan
```

Review the planned changes before applying.

### Apply Configuration

```bash
terraform apply
```

Provisions the VPC, subnets, and EC2 instance.

### Destroy Infrastructure

```bash
terraform destroy
```

Removes all provisioned resources.

## Outputs

No outputs are currently defined. You can add outputs for instance IDs, VPC details, or subnet information by creating an `outputs.tf` file.

## Benefits of Using Public Modules

- **Reduced Complexity**: Focus on business logic rather than infrastructure details
- **Best Practices**: Modules are maintained by community experts and AWS
- **Consistency**: Ensures resources are created with recommended configurations
- **Maintainability**: Updates to modules can be applied across your infrastructure
- **Community Support**: Well-documented with examples and active maintenance

# Terraform Local Modules Project

A comprehensive example project demonstrating the creation and usage of reusable Terraform modules, specifically focusing on networking infrastructure automation.

## Project Overview

This project is structured around the `13-local-modules` example, which showcases best practices for organizing Terraform code into modular, reusable components. The project deploys a complete AWS networking infrastructure including VPCs, public/private subnets, Internet Gateways, and route tables.

## Networking Module

The networking module provides a flexible, reusable way to create AWS VPC infrastructure. It handles the creation of VPCs with customizable subnet configurations, automatic Internet Gateway deployment for public subnets, and proper route table associations.

### Module Features

- **VPC Creation**: Create a VPC with a configurable CIDR block
- **Flexible Subnet Configuration**: Define multiple subnets with individual CIDR blocks and availability zones
- **Public/Private Subnets**: Mark subnets as public or private via configuration
- **Automatic IGW Deployment**: Internet Gateway is automatically created and attached when at least one public subnet exists
- **Route Table Management**: Public subnets are automatically associated with a route table that routes traffic to the Internet Gateway
- **Validation**: Built-in CIDR block validation and availability zone verification

### Module Inputs

#### `vpc_config` (Required)
Object containing VPC configuration:
- `cidr_block` (string): CIDR block for the VPC (e.g., "10.0.0.0/16")
- `name` (string): Name tag for the VPC

#### `subnet_config` (Required)
Map of subnet configurations keyed by subnet identifier:
- `cidr_block` (string): CIDR block for the subnet
- `public` (optional boolean): Set to `true` for public subnets, default is `false` (private)
- `az` (string): AWS availability zone (e.g., "eu-west-1a")

### Module Outputs

- `vpc_id`: The AWS ID of the created VPC
- `public_subnets`: Map of public subnets with subnet_id and availability_zone
- `private_subnets`: Map of private subnets with subnet_id and availability_zone

### Example Usage

```hcl
module "vpc" {
  source = "./modules/networking"

  vpc_config = {
    cidr_block = "10.0.0.0/16"
    name       = "my-vpc"
  }

  subnet_config = {
    subnet_1 = {
      cidr_block = "10.0.0.0/24"
      az         = "eu-west-1a"
      # public defaults to false, so this is a private subnet
    }
    subnet_2 = {
      cidr_block = "10.0.1.0/24"
      public     = true
      az         = "eu-west-1b"
    }
  }
}

output "vpc_id" {
  value = module.vpc.vpc_id
}
```

## Deploy Instructions

1. **Initialize Terraform**:
   ```bash
   cd 13-local-modules
   terraform init
   ```

2. **Validate Configuration**:
   ```bash
   terraform validate
   ```

3. **Plan Deployment**:
   ```bash
   terraform plan
   ```

4. **Apply Configuration**:
   ```bash
   terraform apply
   ```

5. **View Outputs**:
   ```bash
   terraform output
   ```

## AWS Permissions Required

The AWS credentials must have permissions to:
- Create/manage VPCs
- Create/manage Subnets
- Create/manage Internet Gateways
- Create/manage Route Tables
- Create/manage EC2 Instances
- Describe Availability Zones
- Query AMI data

## License

MIT License - See LICENSE file for details

## State Manipulation Examples

This directory contains examples demonstrating various Terraform state manipulation techniques:

### Import (`import.tf`)

Demonstrates how to import existing AWS resources into Terraform state using the `import` block. The example imports an S3 bucket public access block configuration into state.

**Key concepts:**
- Using the `import` block to declare resources that should be imported
- Referencing the ID of existing AWS resources
- Managing resources that were created outside of Terraform

### Remove (`remove.tf`)

Demonstrates how to remove resources from Terraform state without destroying the actual infrastructure using the `removed` block.

**Key concepts:**
- Using the `removed` block to unmanage resources
- Setting `destroy = false` to prevent actual resource deletion
- Useful for resources that will be managed elsewhere or decommissioned separately

### Taint (`taint.tf`)

Contains example resources that can be marked as tainted to force Terraform to destroy and recreate them on the next apply.

**Key concepts:**
- Resources marked as tainted will be replaced during the next `terraform apply`
- Useful for forcing recreation of resources that may have drifted or need updates
- Can be tainted via CLI: `terraform taint <resource_address>`

### Module Structure

The `modules/compute/` directory contains reusable compute infrastructure patterns with proper variable typing and documentation.
