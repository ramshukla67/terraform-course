## [cd80f7a] - 2024-04-21
### feat(proj05-tf-cloud-oidc): add files

Added a complete Terraform Cloud OIDC integration project (`proj05-tf-cloud-oidc`) that demonstrates secure, keyless authentication between Terraform Cloud and AWS. The project includes AWS IAM OpenID Connect provider configuration, an admin automation role with assume role policy conditions, S3 bucket resource example, and full Terraform configuration with variables and provider setup. This enables organizations to eliminate static AWS credentials from Terraform Cloud by using OIDC-based federation.

## [a89f827] - 2024-03-25
### feat(proj03-import-lambda): add files

Added proj03-import-lambda, a new Terraform project demonstrating the resource import feature. This project shows how to adopt an existing AWS Lambda function and its supporting infrastructure (IAM role, policy, and CloudWatch logs) into Terraform management. Includes a Node.js 18.x handler, Lambda Function URL for public HTTP access, and complete IAM/logging configuration. Useful as a reference for migrating legacy infrastructure to Terraform.

## [b738d1a] - 2024-03-13
### feat(10-functions): add files
Added three new example files to the 10-functions directory: a Terraform functions example file demonstrating string manipulation (startswith, lower), mathematical operations (pow), and data transformation functions (yamldecode, jsonencode), along with supporting provider configuration and YAML data files. These are educational example files with no impact on the production codebase.
