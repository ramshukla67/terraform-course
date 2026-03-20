## [cd80f7a] - 2024-04-21
### feat(proj05-tf-cloud-oidc): add files

Added a complete Terraform Cloud OIDC integration project (`proj05-tf-cloud-oidc`) that demonstrates secure, keyless authentication between Terraform Cloud and AWS. The project includes AWS IAM OpenID Connect provider configuration, an admin automation role with assume role policy conditions, S3 bucket resource example, and full Terraform configuration with variables and provider setup. This enables organizations to eliminate static AWS credentials from Terraform Cloud by using OIDC-based federation.
