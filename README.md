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

# 16-State-Manipulation

This directory demonstrates Terraform state manipulation techniques using the `moved` block to refactor resource configurations without destroying and recreating infrastructure.

## Overview

State manipulation in Terraform allows you to reorganize how resources are tracked in state without triggering unnecessary resource replacements. The `moved` block (introduced in Terraform 1.1) enables you to:

- Rename resources
- Move resources into or out of modules
- Change resource addressing schemes (e.g., from list indexing to map indexing)
- Refactor resource organization while preserving running infrastructure

## Key Features

### Resource Refactoring Chain

The `move-state.tf` file demonstrates a multi-step refactoring process:

1. **List to Map Indexing**: Converts two EC2 instances from list indices (`[0]`, `[1]`) to map keys (`["instance1"]`, `["instance2"]`)
2. **Resource to Resource**: Moves one instance to a standalone resource (`aws_instance.new_final`)
3. **Resource to Module**: Moves another instance into a module (`module.compute.aws_instance.this`)

This showcases the flexibility of state management in real-world refactoring scenarios.

### Architecture

The project is structured as follows:

- **move-state.tf**: Main configuration containing the `moved` blocks and resource definitions
- **provider.tf**: Root module provider and version constraints
- **modules/compute/**: Reusable compute module encapsulating EC2 instance logic
- **.terraform.lock.hcl**: Dependency lock file for reproducible provider versions

## Files

### move-state.tf

Demonstrates state migration using `moved` blocks:

- Defines two EC2 instances initially as list items
- Uses `moved` blocks to refactor into:
  - Map-indexed resources for better manageability
  - A standalone resource
  - A module-encapsulated resource
- Includes a data source to fetch the latest Ubuntu 22.04 AMI

### modules/compute/

A reusable module for deploying EC2 instances:

- **compute.tf**: Defines the `aws_instance` resource
- **variables.tf**: Accepts `ami_id` as input
- **provider.tf**: Declares AWS provider requirement

## Usage

### Prerequisites

- Terraform >= 1.7
- AWS provider ~> 5.0
- Valid AWS credentials configured

### Deployment

```bash
cd 16-state-manipulation
terraform init
terraform plan
terraform apply
```

### Observing State Changes

To see the state refactoring in action:

1. Comment out all `moved` blocks and apply to establish initial state
2. Uncomment `moved` blocks one at a time and run `terraform plan`
3. The plan will show state migrations without resource replacement

## State Management Concepts

### Why Use `moved` Blocks?

- **Zero Downtime**: Refactor infrastructure organization without destroying resources
- **Cost Efficiency**: Avoid unnecessary resource recreation and associated costs
- **Cleaner Migrations**: Explicit state transitions make refactoring auditable
- **Module Adoption**: Gradually move resources into modules for better code organization

### Best Practices

1. **Test in Non-Production**: Always test state refactoring in development environments first
2. **Version Control**: Commit `moved` blocks so the refactoring is transparent to team members
3. **Incremental Changes**: Use `terraform plan` frequently to verify migrations
4. **State Backup**: Create a backup of `terraform.tfstate` before major refactoring
5. **Documentation**: Document the reason for each state migration for future reference

## Cleanup

To destroy all resources:

```bash
terraform destroy
```
