# Mastering Terraform: From Beginner to Expert

### Course link (with a big discount 🙂): https://www.lauromueller.com/courses/mastering-terraform

Welcome everyone! I'm very happy to see you around, and I hope this repository brings lots of value for those learning more about Terraform. Make sure to check the link above for a great discourse on the course in Udemy, where I not only provide theoretical explanations around all the concepts here, but also go in details through the entire coding of the examples in this repository.

Here are a few tips for you to best navigate the contents of this repository:
1. The `exercises` folder contains descriptions for all the implemented exercises. You can use it as a guide to try to implement them by yourself before following the solution recordings.
2. The `projects` folder contains six bigger projects that you can also tackle for an extra challenge 🙂 The solutions for these projects are implemented within their respective folders, **except for project 00, which is implemented inside of the folder `06-resources`**.
3. The other folders roughly mirror the structure of the course, but there are some course sections that span more than one folder.

Happy learning! 🚀

## Additional Links and Courses:

**Other repositories included in the course:**
* Networking Module Repository - https://github.com/udemy-lauromueller/terraform-aws-networking-tf-course
* Terraform Cloud VCS Integration Repository - https://github.com/udemy-lauromueller/terraform-course-example-terraform-cloud

**Other courses I published in Udemy:**
* Mastering GitHub Actions: From Beginner to Expert - https://www.lauromueller.com/courses/mastering-github-actions
* Write Clean Code: 20 Code Smells and How to Get Rid of Them - https://lauromueller.com/courses/writing-clean-code/

# proj04-rds-module

A production-ready Terraform module for provisioning RDS PostgreSQL instances with strict security and networking validations.

## Overview

This project demonstrates best practices for RDS deployment on AWS using Terraform. It includes:

- **Custom VPC Setup**: Creates a custom VPC with private and public subnets across multiple availability zones
- **Security Group Validation**: Enforces that security groups only allow inbound traffic from other security groups, preventing direct IP-based access
- **Subnet Validation**: Validates that subnets are not in the default VPC and are properly tagged as private
- **RDS Module**: Reusable Terraform module for creating PostgreSQL instances with standardized configuration

## Module Structure

```
proj04-rds-module/
├── modules/
│   └── rds/                          # Reusable RDS module
│       ├── variables.tf              # Input variables with validation
│       ├── outputs.tf                # RDS instance outputs
│       ├── rds.tf                    # RDS, subnet group, and parameter group resources
│       ├── networking-validation.tf  # Network security validations
│       └── provider.tf               # Provider configuration
├── networking.tf                     # VPC, subnets, and security groups
├── rds.tf                            # Module instantiation
├── provider.tf                       # Root provider configuration
├── outputs.tf                        # Root outputs
└── README.md                         # This file
```

## Features

### Networking Validation

The module enforces several critical validation rules:

1. **Default VPC Prevention**: Subnets must not be part of the default VPC
2. **Private Subnet Verification**: Subnets must be tagged with `Access = "private"`
3. **Security Group Compliance**: Inbound rules must originate from security groups only, not IP CIDR blocks

### Database Configuration

Supported PostgreSQL versions:
- **postgres-latest**: PostgreSQL 16.1
- **postgres-14**: PostgreSQL 14.11

Configurable parameters:
- Instance class (default: `db.t3.micro` for free tier)
- Storage size: 5-10 GB (default: 10 GB)
- Database credentials with strict password validation
- Custom subnet group and parameter groups

### Password Requirements

Database passwords must meet these criteria:
- At least 8 characters long
- Contain at least 1 letter (a-z or A-Z)
- Contain at least 1 digit (0-9)
- Only use characters: a-z, A-Z, 0-9, +, _, ?, -

## Module Inputs

| Variable | Type | Default | Description |
|----------|------|---------|-------------|
| `project_name` | string | required | Project name (used for resource naming and tags) |
| `instance_class` | string | `db.t3.micro` | RDS instance class (free tier only) |
| `storage_size` | number | `10` | Allocated storage in GB (5-10) |
| `engine` | string | `postgres-latest` | PostgreSQL version (`postgres-latest` or `postgres-14`) |
| `credentials` | object | required | Database credentials (username, password) - sensitive |
| `subnet_ids` | list(string) | required | Private subnet IDs for RDS deployment |
| `security_group_ids` | list(string) | required | Security group IDs for RDS access control |

## Module Outputs

| Output | Description |
|--------|-------------|
| `rds_instance_endpoint` | RDS endpoint in `address:port` format |
| `rds_instance_address` | RDS instance hostname |
| `rds_instance_port` | RDS instance port (typically 5432) |
| `rds_instance_id` | RDS instance identifier |
| `rds_instance_arn` | RDS instance ARN |

## Usage Example

```hcl
module "database" {
  source = "./modules/rds"

  project_name = "my-app-db"
  engine       = "postgres-latest"
  instance_class = "db.t3.micro"
  storage_size = 10

  credentials = {
    username = "dbadmin"
    password = "SecurePass123+_"
  }

  subnet_ids = [
    aws_subnet.private1.id,
    aws_subnet.private2.id
  ]

  security_group_ids = [aws_security_group.db.id]
}
```

## Example Infrastructure

This project includes a complete example setup in the root directory:

- **VPC**: Custom VPC with CIDR block `10.0.0.0/16`
- **Private Subnets**: Two private subnets for RDS deployment (eu-west-1a, eu-west-1b)
- **Public Subnet**: One public subnet for future application deployments
- **Security Groups**:
  - `source-sg`: Source of database connections
  - `compliant-sg`: Properly configured security group (only references other security groups)
  - `non-compliant-sg`: Demonstrates invalid configuration (direct CIDR-based access)

## Validation Errors

### Default VPC Error

When attempting to use a subnet from the default VPC:

```
Error: Resource postcondition failed

The following subnet is part of the default VPC:
Name = my-default-subnet
ID = subnet-123abc

Please do not deploy RDS instances in the default VPC.
```

### Missing Private Tag Error

When a subnet lacks the required `Access = "private"` tag:

```
Error: Resource postcondition failed

The following subnet is not marked as private:
Name = my-public-subnet
ID = subnet-456def

Please ensure that the subnet is properly tagged by adding the following tags:
1. Access = "private"
```

### Security Group Compliance Error

When a security group allows inbound traffic from IP CIDR blocks:

```
Error: Resource postcondition failed

The following security group contains an invalid inbound rule:
ID = sg-789ghi

Please ensure that the following conditions are met:
1. Rules must not allow inbound traffic from IP CIDR blocks, only from other security groups.
```

## Requirements

- Terraform >= 1.7
- AWS Provider >= 5.0
- AWS account with appropriate permissions for RDS, VPC, and security group management

## Provider Configuration

The root provider is configured for the `eu-west-1` region. To use a different region, modify `provider.tf`.

## License

This is an educational project demonstrating Terraform best practices.
