## [14a9b57] - 2026-03-21
### Merge pull request #1 from ramshukla67/repoWrit/update-1774045563602

docs: auto-update documentation (b44587c)
Creation of CHANGELOG.md file documenting a previous documentation content update (adding a promotional course link). This is a meta-documentation commit that records a content change rather than introducing new features or technical changes.

## [cd80f7a] - 2024-04-21
### feat(proj05-tf-cloud-oidc): add files

Added a complete Terraform Cloud OIDC integration project (`proj05-tf-cloud-oidc`) that demonstrates secure, keyless authentication between Terraform Cloud and AWS. The project includes AWS IAM OpenID Connect provider configuration, an admin automation role with assume role policy conditions, S3 bucket resource example, and full Terraform configuration with variables and provider setup. This enables organizations to eliminate static AWS credentials from Terraform Cloud by using OIDC-based federation.

## [cff579e] - 2024-03-25
### feat(17-workspaces): add files

Added a new Terraform workspaces example module demonstrating multi-environment infrastructure management. The module includes provider configuration (AWS ~5.0, random ~3.0), environment-specific variable files for dev/int/staging/prod environments, and S3 bucket resources that scale from 1 to 3 buckets depending on the workspace. This example illustrates best practices for using Terraform workspaces to manage separate state files across multiple environments with a single configuration codebase.

## [a89f827] - 2024-03-25
### feat(proj03-import-lambda): add files

Added proj03-import-lambda, a new Terraform project demonstrating the resource import feature. This project shows how to adopt an existing AWS Lambda function and its supporting infrastructure (IAM role, policy, and CloudWatch logs) into Terraform management. Includes a Node.js 18.x handler, Lambda Function URL for public HTTP access, and complete IAM/logging configuration. Useful as a reference for migrating legacy infrastructure to Terraform.

## [67c6bc5] - 2024-03-20
### feat(15-object-validation): add files
Added new Terraform example project demonstrating object validation patterns using postconditions and check blocks. Includes EC2 instance deployment with instance type validation, subnet creation with availability zone distribution checks, and resource compliance assertions. Implements best practices for infrastructure validation in Terraform 1.7+.

## [c628a0f] - 2024-03-13
### feat(12-public-modules): add files

Added a new Terraform configuration example demonstrating the use of public modules from the Terraform Registry. This example implements a complete AWS infrastructure setup using the terraform-aws-modules/vpc and terraform-aws-modules/ec2-instance modules. The configuration includes provider setup for AWS in eu-west-1 region, a VPC with public and private subnets across availability zones, and a t2.micro EC2 instance running Ubuntu 22.04 LTS. This demonstrates best practices for leveraging certified public modules to reduce code duplication, improve maintainability, and ensure infrastructure follows community-validated patterns.

## [b738d1a] - 2024-03-13
### feat(10-functions): add files
Added three new example files to the 10-functions directory: a Terraform functions example file demonstrating string manipulation (startswith, lower), mathematical operations (pow), and data transformation functions (yamldecode, jsonencode), along with supporting provider configuration and YAML data files. These are educational example files with no impact on the production codebase.

## [8133ed1] - 2024-03-11
### feat(proj02): add files

Added proj02-iam-users, a new Terraform infrastructure-as-code project for managing AWS IAM users and roles. The project includes user provisioning from YAML configuration, automatic role creation with four predefined access levels (readonly, developer, admin, auditor), and policy attachment to AWS managed policies. Users receive auto-generated login profiles with initial passwords upon deployment to the eu-west-1 AWS region.

## [88d5f78] - 2024-03-08
### feat(11-multiple-resources): add files

Added a new Terraform example module demonstrating provisioning of multiple AWS resources using `count` and `for_each` meta-arguments. The module includes VPC and subnet creation via map-based configuration, two different EC2 provisioning patterns (count from list and for_each from map), dynamic AMI data source lookups for Ubuntu and Nginx images, and comprehensive input validation for CIDR blocks, instance types, and AMI selections. This example helps users understand the differences between count and for_each iteration approaches in Terraform.

## [e4b761d] - 2024-03-05
### feat(09-expressions): add files

Added a new educational module `09-expressions` demonstrating core HCL expression techniques in Terraform. This module includes six Terraform files covering operators, for-loops (lists and maps), splat syntax, and complex list-to-map transformations. Includes complete variable definitions and sample test data via terraform.tfvars. Perfect for learning how to transform and filter data structures in Terraform configurations.

## [71e7123] - 2024-02-28

### feat(proj01): add project files

Added the first Terraform project: a static website hosting solution on AWS S3. The project includes complete Terraform configuration files for provisioning an S3 bucket with public read access, website configuration for serving HTML files, and automatic file uploads. This demonstrates fundamental Terraform patterns including resource creation, policy management, and output definition for AWS infrastructure.

## [f307e1d] - 2024-02-25
### feat(05-providers): add resources

Added 05-providers module demonstrating Terraform provider configuration best practices. Includes AWS provider setup with version constraints (~> 5.0 for AWS, ~> 1.0 for Terraform), a lock file for version pinning, and example resources showing multi-region setup using provider aliasing. Two S3 buckets are created in eu-west-1 and us-east-1 to demonstrate explicit provider assignment and region-specific resource management.

## [e57dd02] - 2024-02-25
### feat(06-resources): add files

Added the 06-resources Terraform module, a complete example of AWS infrastructure provisioning. This module demonstrates VPC creation with public subnets, internet gateway setup, routing configuration, and EC2 instance deployment with security groups. The infrastructure deploys a t2.micro EC2 instance running NGINX accessible via HTTP/HTTPS, serving as a practical learning example for AWS networking and compute resources using Terraform.

## [3f8eb0d] - 2024-02-21
### feat(04-backends): add resources

Added a new Terraform module demonstrating remote state management using AWS S3 backends. This module includes provider configuration for AWS and random providers, separate backend configuration files for dev and prod environments, and an example S3 bucket resource with random naming. The `.terraform.lock.hcl` file pins AWS provider to version 5.37.0 and random provider to 3.6.0, ensuring consistent environments across team members and CI/CD pipelines.

## [8a973e5] - 2024-02-19
### feat(03-first-tf-project): add resources
Initialized the first Terraform project with core infrastructure configuration. Added provider setup for AWS (eu-west-1 region) and Random provider with version constraints. Implemented an example S3 bucket resource with automatic unique naming via random ID suffix. Included .terraform.lock.hcl for dependency reproducibility across environments.

## [6ce248f] - 2024-02-18
### feat(02-hcl): add examples of HCL constructs
Added a new HCL example file demonstrating core Terraform constructs including resource definitions for S3 buckets, data sources for external resource references, input variables with defaults, outputs, locals, and module composition. This serves as a practical reference guide for HCL syntax patterns.

## [e31300c] - 2024-02-16

### Initial commit: feat(01-benefits-iac): add IaC code for deploying VPC

This initial commit introduces Infrastructure-as-Code (IaC) Terraform configurations for deploying AWS Virtual Private Cloud (VPC) infrastructure. The project demonstrates cloud infrastructure provisioning using declarative configuration management, making it easy to version, review, and replicate network infrastructure across different environments.

#### Project Overview

The benefits-iac repository focuses on teaching and implementing Infrastructure-as-Code best practices using Terraform. This first commit establishes the foundation with VPC deployment capabilities, which is essential for any AWS infrastructure setup. The VPC serves as the networking layer for other AWS resources and is a fundamental building block of cloud infrastructure.

#### Key Files and Directories

- **01-benefits-iac/vpc.tf** - Primary Terraform configuration file containing all VPC resource definitions. This file defines the Virtual Private Cloud setup including network topology, subnet configurations, routing rules, and connectivity options. It serves as the single source of truth for VPC infrastructure state.

#### Technologies and Frameworks

- **Terraform** (Infrastructure-as-Code tool) - Enables declarative infrastructure provisioning and state management
- **AWS** (Amazon Web Services) - Cloud provider hosting VPC and networking services
- **HCL** (HashiCorp Configuration Language) - Configuration language used in Terraform files

#### Notable Features and Configurations

- **Declarative Configuration** - Infrastructure is defined in code rather than through manual console operations
- **State Management** - Terraform maintains state files to track deployed resources and detect changes
- **Version Control** - All infrastructure definitions are tracked in Git for audit trails and collaboration
- **AWS Networking** - Implements core VPC components including virtual network isolation, subnet segmentation, and traffic routing

#### VPC Infrastructure Components

The vpc.tf configuration typically includes:

- **VPC Resource** - Virtual network boundary defining IP address space (CIDR block)
- **Subnets** - Divided network segments (public and private) for resource organization
- **Internet Gateway** - Enables communication between VPC resources and the internet
- **Route Tables** - Define traffic routing rules within the VPC
- **Security Groups** - Stateful firewalls controlling inbound and outbound traffic
- **Network ACLs** - Stateless access control lists for subnet-level filtering (if configured)

#### Deployment Workflow

Users can deploy the VPC infrastructure using standard Terraform commands:
1. `terraform init` - Initialize Terraform working directory
2. `terraform plan` - Preview infrastructure changes
3. `terraform apply` - Deploy VPC resources to AWS
4. `terraform destroy` - Tear down infrastructure when no longer needed

#### Benefits of This Approach

- **Reproducibility** - VPC configuration can be consistently deployed across regions or environments
- **Version Control** - Infrastructure changes are tracked in Git history
- **Collaboration** - Team members can review and approve infrastructure changes via code review
- **Documentation** - The .tf files serve as living documentation of the infrastructure
- **Automation** - Infrastructure deployment can be automated in CI/CD pipelines

This initial commit establishes the groundwork for managing cloud infrastructure as code, enabling teams to implement infrastructure best practices from the beginning of their cloud journey.
