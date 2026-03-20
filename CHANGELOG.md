## [329aca9] - 2024-12-22
### Update README.md
Added a single course link (The Definitive Helm Course) to the existing course list in README.md. This is a minor content update with no impact on project functionality, code architecture, or system behavior.

## [456abd7] - 2024-03-17
### refactor: standardize Terraform required versions
Standardized Terraform required_version constraints across seven project directories to use the consistent "~> 1.7" version specification, replacing various previously inconsistent version constraints (">= 1.7.0", "~> 1.0", ">= 1.7.0, < 2.0.0", and "~> 1.7.0"). This is a configuration standardization that does not alter functionality or user-facing behavior.
