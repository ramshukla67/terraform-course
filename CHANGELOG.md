## [7acb6eb] - 2024-04-02
### chore: code cleanup
This commit contains only code formatting and whitespace cleanup across multiple Terraform files, including indentation standardization, alignment adjustments, and removal of commented-out code. No functional behavior, features, or logic changes are introduced.

## [2dad4f2] - 2024-03-23
### feat(16-state-manipulation): add move-state file

Added new example directory demonstrating Terraform state manipulation using the `moved` block. This includes a complete example of refactoring EC2 instances from list-indexed resources to map-indexed resources and modules. The implementation shows how to migrate infrastructure state without triggering resource replacements, including a compute module for encapsulation, provider configuration, and multiple state migration examples. This serves as a practical reference for teams performing infrastructure refactoring while maintaining uptime.
