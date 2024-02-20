These are the values for the configuration of the infrastructure and they can be reused. **Unlike other programming languages, the input variables do not change values during a Terraform execution** Instead they allow safe customization by assigning different values to the variables before exection begins, rather than editing configuration files manually.
In ARM template, the JSON has to be changed for different requirement each time, but not in this.

### Using variables:

They can be defined anywhere in the configuration file but it is recommended to use a `variables.tf` file .

For example:

```js
variable "location" {
  description = "Azure region" // Short description for readability purposes
  type        = string // data type , can be a complete Object Type
  default     = "westeurope" // default value
}

```

You can refer to variables in your configuration with `var.<variable_name>`. For example,

```js
// in main.tf
 provider "azure" {

+  region  = var.location
 }
```

### Assigning a value to the variable

##### Using command line flag

For example, consider the following codes:

```js
// in variables.tf
variable "azure_resource_group_name" {
  description = "Azure resource group name"
  type        = string
}
```

```js
//in main.tf
module "azure_resource_groups" {
    source = "./modules/azure-instance"

    instance_type  = var.azure_resource_group_name
}
```

The value for `azure_resource_group_name` can be passed in CLI while applying.

```
terraform apply -var azure_resource_group_name="AZ_RG_1"
```

This is tedious for cases more than one value, which is most definitely the case.

##### Using an assigning file

You can create a file named `terraform.tfvars` and put the values in there. At run time, terraform automatically loads all files in the current directory with the exact name `terraform.tfvars` or `*.auto.tfvars`. To use other file names use the `-var-file` tag

For exammple, in the case defined above

```js
// in terraform.tfvars
azure_resource_group_name = "AZ_RG_1";
```

#### Using variables between strings

You can use `${variable-name}` for interpolation.
For example:

```js
//in main.tf
module "azure_resource_groups" {
    source = "./modules/azure-instance"

    instance_type  = "AZURE_RESOURCE_${var.azure_resource_group_name}"
}
```

##### Adding validators to variables

Based on your case you can add validators to a variable as follows:

```js
variable "test_Variable"{
    description = "Test variable"
    type = int
    default = 0
    validation{
        condition = var.test_Variable > 10
        error_message = "The number should be less than or equal to 10"
    } // this is just a dummy validation on test_Variable
}
```

[More information on Variables](https://developer.hashicorp.com/terraform/tutorials/cli/variables#interpolate-variables-in-strings)
