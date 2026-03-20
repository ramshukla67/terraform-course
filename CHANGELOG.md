## [cd80f7a] - 2024-04-21
### feat(proj05-tf-cloud-oidc): add files

Added a complete Terraform Cloud OIDC integration project (`proj05-tf-cloud-oidc`) that demonstrates secure, keyless authentication between Terraform Cloud and AWS. The project includes AWS IAM OpenID Connect provider configuration, an admin automation role with assume role policy conditions, S3 bucket resource example, and full Terraform configuration with variables and provider setup. This enables organizations to eliminate static AWS credentials from Terraform Cloud by using OIDC-based federation.

## [a89f827] - 2024-03-25
### feat(proj03-import-lambda): add files

Added proj03-import-lambda, a new Terraform project demonstrating the resource import feature. This project shows how to adopt an existing AWS Lambda function and its supporting infrastructure (IAM role, policy, and CloudWatch logs) into Terraform management. Includes a Node.js 18.x handler, Lambda Function URL for public HTTP access, and complete IAM/logging configuration. Useful as a reference for migrating legacy infrastructure to Terraform.

## [b738d1a] - 2024-03-13
### feat(10-functions): add files
Added three new example files to the 10-functions directory: a Terraform functions example file demonstrating string manipulation (startswith, lower), mathematical operations (pow), and data transformation functions (yamldecode, jsonencode), along with supporting provider configuration and YAML data files. These are educational example files with no impact on the production codebase.

## [e57dd02] - 2024-02-25
### feat(06-resources): add files

Added the 06-resources Terraform module, a complete example of AWS infrastructure provisioning. This module demonstrates VPC creation with public subnets, internet gateway setup, routing configuration, and EC2 instance deployment with security groups. The infrastructure deploys a t2.micro EC2 instance running NGINX accessible via HTTP/HTTPS, serving as a practical learning example for AWS networking and compute resources using Terraform.

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
