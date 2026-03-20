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

# Terraform Course - Infrastructure as Code

A comprehensive guide to mastering Terraform and Infrastructure as Code (IaC) practices. This repository contains 61 hands-on exercises covering everything from basic AWS console operations to advanced Terraform Cloud features.

## Course Overview

This course is structured around practical, real-world scenarios and progresses from foundational concepts to advanced patterns.

### Part 1: Foundations (Exercises 01-06)

- **Exercise 01**: Manual VPC and subnet creation in AWS Console
- **Exercise 02**: Creating VPCs and subnets with Terraform
- **Exercise 03**: Understanding Terraform lifecycle stages (init, plan, apply, destroy)
- **Exercise 04**: HashiCorp Configuration Language (HCL) syntax overview
- **Exercise 05**: First Terraform project with S3 buckets and random IDs
- **Exercise 06**: Terraform CLI commands and validation

### Part 2: State Management & Backends (Exercises 07-08)

- **Exercise 07**: Configuring S3 remote backends for state storage
- **Exercise 08**: Partial backend configuration for multiple environments (dev/prod)

### Part 3: Providers & Data Sources (Exercises 09-13)

- **Exercise 09**: Working with multiple AWS provider instances across regions
- **Exercise 10**: Using data sources to fetch AMI information
- **Exercise 11**: Fetching AWS caller identity and region information
- **Exercise 12**: Retrieving VPC information from manually-created resources
- **Exercise 13**: Creating IAM policies with data sources

### Part 4: Variables, Locals & Outputs (Exercises 14-21)

- **Exercise 14**: Managing AWS regions via variables (and pitfalls to avoid)
- **Exercise 15**: Customizing EC2 instance size with variable validation
- **Exercise 16**: Using objects for complex configuration
- **Exercise 17**: Working with `.tfvars` files for different environments
- **Exercise 18**: Working with `auto.tfvars` for automatic variable loading
- **Exercise 19**: Using locals for shared configuration
- **Exercise 20**: Defining and retrieving outputs
- **Exercise 21**: Handling sensitive values in Terraform

### Part 5: Expressions & Functions (Exercises 22-26)

- **Exercise 22**: Operators in Terraform (math, equality, comparison, logical)
- **Exercise 23**: `for` expressions with lists
- **Exercise 24**: `for` expressions with maps
- **Exercise 25**: Transforming lists to maps and vice versa
- **Exercise 26**: Working with built-in functions (string, math, file encoding)

### Part 6: Meta-Arguments (Exercises 27-31)

- **Exercise 27**: Creating multiple resources with `count`
- **Exercise 28**: Referencing and distributing resources created with `count`
- **Exercise 29**: Creating EC2 instances from list variables
- **Exercise 30**: Extending AMI support (Ubuntu + NGINX)
- **Exercise 31**: Adding validation to list inputs

### Part 7: Map-Based Configuration (Exercises 32-34)

- **Exercise 32**: Creating EC2 instances from map variables with `for_each`
- **Exercise 33**: Validating map variable inputs
- **Exercise 34**: Passing subnet configuration dynamically

### Part 8: Public Modules (Exercises 35-36)

- **Exercise 35**: Using the AWS VPC public module
- **Exercise 36**: Using the AWS EC2 public module

### Part 9: Custom Modules (Exercises 37-43)

- **Exercise 37**: Creating your first VPC module
- **Exercise 38**: Migrating to object variable types
- **Exercise 39**: Extending modules to receive subnet configuration
- **Exercise 40**: Validating Availability Zones in modules
- **Exercise 41**: Creating public and private subnets
- **Exercise 42**: Defining module outputs
- **Exercise 43**: Testing modules with EC2 instances

### Part 10: Lifecycle Management (Exercises 44-50)

- **Exercise 44**: Precondition blocks for validation before resource creation
- **Exercise 45**: Postcondition blocks for validation after resource creation
- **Exercise 46**: Check blocks for best practice enforcement
- **Exercise 47**: Refactoring with `moved` blocks and CLI
- **Exercise 48**: Importing existing infrastructure with `import` blocks
- **Exercise 49**: Removing resources with `removed` blocks
- **Exercise 50**: Replacing resources with taints

### Part 11: Workspaces (Exercises 51-53)

- **Exercise 51**: Creating CLI-based workspaces
- **Exercise 52**: Managing multiple workspaces
- **Exercise 53**: Using `.tfvars` files for workspace-specific configuration

### Part 12: Terraform Cloud (Exercises 54-61)

- **Exercise 54**: Creating Terraform Cloud workspaces
- **Exercise 55**: Deploying resources via Terraform Cloud
- **Exercise 56**: Authenticating AWS with environment variables
- **Exercise 57**: Understanding workspace variables
- **Exercise 58**: VCS integration with GitHub
- **Exercise 59**: Generating speculative plans from pull requests
- **Exercise 60**: Publishing modules in private registries
- **Exercise 61**: Cleaning up Terraform Cloud resources

## Prerequisites

- AWS account with appropriate permissions
- Terraform CLI (~> 1.7)
- Git and GitHub account (for Terraform Cloud exercises)
- Basic command-line knowledge

## Getting Started

1. Clone this repository
2. Navigate to the exercises folder
3. Read the exercise introduction and desired outcome
4. Follow the step-by-step guide
5. Practice the concepts with real infrastructure

## Key Concepts Covered

- **Infrastructure as Code (IaC)**: Define and manage infrastructure through code
- **Terraform Workflow**: Init → Plan → Apply → Destroy
- **State Management**: Local and remote state storage
- **Modules**: Reusable components and private registries
- **Variables & Validation**: Input validation and complex data types
- **Data Sources**: Querying existing infrastructure
- **Lifecycle Management**: Creating, modifying, and destroying resources safely
- **Terraform Cloud**: Collaboration, state management, and VCS integration

## AWS Services Covered

- VPC (Virtual Private Cloud)
- Subnets (Public & Private)
- Internet Gateways
- Route Tables
- EC2 Instances
- S3 Buckets
- IAM Policies
- Security Groups
- Availability Zones

## Best Practices Emphasized

- Using variables for configuration flexibility
- Validating inputs to prevent misconfigurations
- Organizing code with modules for reusability
- Managing state remotely for collaboration
- Using workspaces for environment separation
- Leveraging Terraform Cloud for team workflows
- Preconditions and postconditions for reliability
- Check blocks for best practice enforcement

## Important Notes

- Always run `terraform plan` before `terraform apply`
- Use `terraform destroy` to clean up resources and avoid unexpected charges
- Keep `.tfstate` files secure and version-controlled (when remote)
- Test modules thoroughly before publishing to registries
- Document your modules with clear descriptions
- Use meaningful variable names and descriptions

## Continuing Your Learning

After completing all 61 exercises, you'll have the skills to:
- Design scalable infrastructure with Terraform
- Create reusable modules for your organization
- Implement best practices for state management
- Collaborate on infrastructure using Terraform Cloud
- Manage multiple environments effectively

## Support

Refer to the official Terraform documentation at [terraform.io](https://www.terraform.io) for additional resources and detailed API documentation.
