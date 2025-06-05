In this lesson, we’ll continue working on the Terraform configuration file we started in [[Terraform - Creating an EC2 Instance]].

- Create **input variables** to parametrize configuration
- Export resource information using output values
- Organize Terraform workspace effectively
 
Instead of hard-coded values inside code blocks, you can use **input variables** to customize your infrastructure without manually editing the configuration file every time. Input variables allow you to specify different values when creating resources, making your configuration more dynamic and adaptable.

![[terraform_config_hardcoded_value.webp]]

## The Input block

Let’s start by creating input variables. We’ll define two variables: one for the region name and another for the server name. Here’s how you declare them using the `variable` keyword:

```hcl
# input
variable "region" {
  description = "region for aws resources"
  type        = string
  default     = "us-east-1"
}

variable "server_name" {
  description = "name of the server running the website"
  type        = string
}
```

Each variable has three optional arguments:
1. **Description**: Documents the purpose of the variable.
2. **Type**: Specifies the data type (e.g., string, number, list).
3. **Default**: Assigns a default value. If no default is provided, Terraform will prompt you to enter a value when applying the configuration.

To use these variables in other blocks, reference them using the syntax `var.variable_name`. For example:
- In the **Provider block**, replace the hard-coded region with `var.region`.
- In the **Resource block**, replace the hard-coded instance name with `var.server_name`.
  
In this example, under the Input Variables section, I'm going to create one variable that represents the region name, and another one that represents the server's name. You can declare these variables like this using the variable keyword. 

### Assigning Values to Variables
To avoid being prompted for variable values, you can:
1. Use the `--var` flag in the command line:
   ```bash
   terraform apply --var "server_name=ExampleServer"
   ```
2. Define values in a `.tfvars` file. For example, create a file named `terraform.tfvars` in the same directory as your configuration file and assign values there:
   ```hcl
   server_name = "ExampleServer"
   ```

When you run `terraform apply`, Terraform will automatically use the values from the `.tfvars` file. In this case, since the EC2 instance name hasn’t changed, Terraform won’t detect any updates.

## The Output block

Every resource you create has a set of attributes. For example, an EC2 instance has attributes like its ID, ARN (Amazon Resource Name), and public DNS. You might want to export these attributes for use in other parts of your infrastructure or to reference them in other Terraform workspaces.

To do this, declare **output values**. Here’s how to export the ID and ARN of the EC2 instance:

```hcl
# output
output "server_id" {
  value = aws_instance.webserver.id
}

output "server_arn" {
  value = aws_instance.webserver.arn
}
```

Check the [documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) of the EC2 instance, to see a list of all of its attributes.

Each output value has a name (e.g., `server_id`, `server_arn`) and a `value` argument that references the resource attribute. You access attributes using the syntax `resource_type.resource_name.attribute`.

After applying the configuration with `terraform apply`, Terraform will display the output values in the command line. You can also query outputs later using:
- `terraform output` to list all outputs.
- `terraform output <output_name>` to query a specific output.

## Organizing Terraform Workspace

As your configuration grows, managing everything in a single file becomes cumbersome. A better practice is to split your configuration into multiple files. For example:

- **variables.tf**: Declare all input variables.
- **outputs.tf**: Define all output values.
- **providers.tf**: Specify provider configurations.
- **main.tf**: Define resources.

You can even split `main.tf` further by declaring each resource in a separate `.tf` file. Terraform will automatically concatenate all `.tf` files in the directory as if they were written in a single file.

Here’s how I’ve organized the workspace:
1. Created `variables.tf`, `providers.tf`, and `outputs.tf`.
2. Moved variables to `variables.tf`.
3. Moved output values to `outputs.tf`.
4. Moved Terraform settings and provider blocks to `providers.tf`.

This modular approach makes your configuration easier to maintain infrastructure.

Next, we'll learn how to use **modules** to further organize the workspace and introduce **data sources** to fetch information from cloud provider.