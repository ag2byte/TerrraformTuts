Once initialization is done, Terraform creates an execution plan before applying the changes. This include creation, updation and destroying resources. You can use the `terraform plan` command to compare your configuration to your resource's state, review changes before you apply them, or to refresh your workspace's status

### Warning:

Terraform plan files can contain sensitive data. Never commit a plan file to version control, whether as a binary or in JSON format.

You can uses the `- out` flag to save a plan and apply it later. For example,
`terraform plan -out 'tfplan'`

[More details on Plan](https://developer.hashicorp.com/terraform/tutorials/cli/plan)
