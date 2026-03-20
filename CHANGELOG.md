## [c4c620f] - 2024-12-23
### feat(proj02): add sensitive flag to passwords output
Added `sensitive = true` flag to the `passwords` output in the IAM users module to prevent sensitive password data from being displayed in Terraform logs, state output, and console output. This improves security by ensuring credentials are never accidentally exposed during plan or apply operations. Also upgraded AWS provider from 5.40.0 to 5.82.2.

## [b27ee17] - 2024-03-22
### feat(exercises): add files

Added comprehensive set of 61 hands-on exercises covering the complete Terraform and Infrastructure as Code (IaC) journey. This includes foundational concepts with AWS Console and basic Terraform workflows, progressing through state management, providers, data sources, variables, expressions, meta-arguments, modules, lifecycle management, workspaces, and Terraform Cloud integration. Exercises range from manual VPC creation to publishing private module registries, providing a complete learning path from beginner to advanced Terraform practitioner.

Also updated `.gitignore` to exclude `.prettierrc` configuration file.
