## [329aca9] - 2024-12-22
### Update README.md
Added a single course link (The Definitive Helm Course) to the existing course list in README.md. This is a minor content update with no impact on project functionality, code architecture, or system behavior.

## [456abd7] - 2024-03-17
### refactor: standardize Terraform required versions
Standardized Terraform required_version constraints across seven project directories to use the consistent "~> 1.7" version specification, replacing various previously inconsistent version constraints (">= 1.7.0", "~> 1.0", ">= 1.7.0, < 2.0.0", and "~> 1.7.0"). This is a configuration standardization that does not alter functionality or user-facing behavior.

## [e09f917] - 2024-03-16
### feat(13-local-modules): add files

Added a complete Terraform project demonstrating local module usage and reusability. This includes a fully-functional networking module that manages VPC creation, subnet configuration (public and private), Internet Gateway deployment, and route table management. The module validates CIDR blocks and availability zones, outputs subnet information indexed by configuration key, and automatically handles infrastructure decisions based on subnet types. The root project instantiates this module with example configurations and deploys an EC2 instance in a private subnet for demonstration purposes.

## [b44587c] - 2024-10-31
### Update README.md
Added a promotional link to "The Complete Docker and Kubernetes Course" in the README's course listing section. This is a content update to reference material with no impact on the project's functionality, features, or technical documentation.

