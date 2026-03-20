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

## State Manipulation Examples

This directory contains examples demonstrating various Terraform state manipulation techniques:

### Import (`import.tf`)

Demonstrates how to import existing AWS resources into Terraform state using the `import` block. The example imports an S3 bucket public access block configuration into state.

**Key concepts:**
- Using the `import` block to declare resources that should be imported
- Referencing the ID of existing AWS resources
- Managing resources that were created outside of Terraform

### Remove (`remove.tf`)

Demonstrates how to remove resources from Terraform state without destroying the actual infrastructure using the `removed` block.

**Key concepts:**
- Using the `removed` block to unmanage resources
- Setting `destroy = false` to prevent actual resource deletion
- Useful for resources that will be managed elsewhere or decommissioned separately

### Taint (`taint.tf`)

Contains example resources that can be marked as tainted to force Terraform to destroy and recreate them on the next apply.

**Key concepts:**
- Resources marked as tainted will be replaced during the next `terraform apply`
- Useful for forcing recreation of resources that may have drifted or need updates
- Can be tainted via CLI: `terraform taint <resource_address>`

### Module Structure

The `modules/compute/` directory contains reusable compute infrastructure patterns with proper variable typing and documentation.
