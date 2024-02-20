Terraform output values let you export structured data about your resources. You can use this data to configure other parts of your infrastructure with automation tools, or as a data source for another Terraform workspace. Outputs are also how you expose data from a child module to a root module.

You can add output in `outputs.tf` file.

```js
// in outputs.tf
output "res_id" {
  description = "ID of Resource"
  value       = module.azure_Resource.res_id
}
```

After creating the outputs, use the terraform output command to query all of them.

#### Hide sensitive outputs

You can make the sensitive property true whilw declaring the output. For example:

```js
output "db_username" {
  description = "Database administrator username"
  value       = aws_db_instance.database.username
  sensitive   = true
}

output "db_password" {
  description = "Database administrator password"
  value       = aws_db_instance.database.password
  sensitive   = true
}

```

[More on output](https://developer.hashicorp.com/terraform/tutorials/cli/outputs#output-vpc-and-load-balancer-information)
