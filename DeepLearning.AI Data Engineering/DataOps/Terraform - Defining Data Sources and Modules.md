In addition to the **input** and **output** blocks, Terraform also allows you to declare **data blocks** within configuration files. Data blocks are used to reference resources created outside of Terraform or in another Terraform workspace. These referenced resources are known as **data sources**. To understand how to declare these resources, you can refer to the [provider documentation](https://registry.terraform.io/providers/hashicorp/aws/latest/docs) available in the Terraform Registry.

You’ll notice that for each resource supported by a provider, you can declare it either as a **resource** (to create and manage it) or as a **data source** (to read from an external resource). Let’s explore two examples to demonstrate how data blocks work.

### Example 1: Launching an EC2 Instance in a Specific Subnet

In [[Terraform - Creating an EC2 Instance|previous tutorial]], We created a configuration file to launch an EC2 instance within the default VPC. Now, let’s say we want to launch the EC2 instance in a subnet of a VPC that was created outside the current workspace. 

![[creating_terraform_ec2_public_subnet.svg|500]]

To access this subnet, you can declare a **data block** as shown below. 

```hcl
# data source
data "aws_subnet" "selected_subnet" {
    id = "subnet-0a4518da5927f157e"
}
```

Similar to a resource block, a data block begins with the `data` keyword, followed by two strings:

1. The **resource type** (e.g., `aws_subnet`), which you can find in the provider’s documentation.
2. A **name** you assign to this data source, which can be referenced throughout the configuration file.

Inside the data block, you specify the arguments required to identify the desired subnet. For example, if you know the subnet ID, you can assign it to the `id` argument. Once the data source is declared, you can access its attributes using the following syntax:

```hcl
data.aws_subnet.selected_subnet.id
```

This expression retrieves the ID of the subnet. In the EC2 instance’s resource block, you can then use this expression to assign the `subnet_id` attribute, ensuring the instance is launched in the desired subnet.

While you could directly reference the subnet ID in the resource block, using a data block is beneficial when you don’t have the ID readily available. Instead, you can use other arguments (e.g., tags, filters) to identify the subnet dynamically.

### Example 2: Automating AMI Selection

To avoid manually retrieved an AMI ID from the AWS console, you can use a data block to instruct Terraform to search for and retrieve the latest Linux AMI. Here’s an example:

```hcl
data "aws_ami" "latest_amazon_linux" {
  most_recent = true
  owners      = ["amazon"]
  filter {
    name   = "architecture"
    values = ["x86_64"]
  }
  filter {
    name   = "name"
    values = ["al202*-ami-202*"]
  }
}
```

This data block asks Terraform to find the most recent Amazon-owned AMI with a Linux-based architecture. You can then reference this AMI in the EC2 instance resource block using:

```hcl
ami = data.aws_ami.latest_amazon__linux.id
```

### Applying the Configuration

After updating the configuration, run `terraform apply` to see the changes. Terraform will plan to destroy the previous instance and create a new one with the updated network settings. It will also perform the search to find the latest AMI. Once you confirm by typing `yes`, Terraform will apply the updates.

## Using Modules in Terraform 

A **module** is essentially a subdirectory within your main directory that packages resources, input variables, and output values.

A module is a subdirectory inside your main directory that you can use to group resources that are used together. So you can think of it as a way to package those resources. 

For example, let’s create a `website` module to group all resources related to a web server. To do this:

1. Move the `main.tf` file (containing the web server definition) into the `website` module.
2. Since a module is like a root directory, it requires its own provider declarations, input variables, and output values. Move these files into the `website` module as well.

However, the root directory can no longer directly access the module’s resources, variables, or outputs. To resolve this, declare a **module block** in the root directory to call the module:

```hcl
# main.tf
module "website" {
  source = "./website"
  server_name = var.server_name_root
}
```

Here, `server_name` is an input variable for the module, and `var.server_name_root` is a variable declared in the root directory’s `variables.tf` file. 

```hcl
# variable.tf
variable "server_name=my_server "variable "server_name_root" {
	description = "name of the server running the website"
	type = string
}
```

You’ll also need to specify the value of `server_name_root` in the root directory’s `terraform.tfvars` file.

```hcl
# terraform.tfvars
server_name_root="ExampleServer"
```

To export the module’s outputs (e.g., `server_id` and `server_arn`) to the root directory, create an `outputs.tf` file in the root directory and reference the module’s outputs:

```hcl
# output.tf
output "server_id" {
  value = module.website.server_id
}

output "server_arn" {
  value = module.website.server_arn
}
```

Whenever you add, remove, or modify module blocks, run `terraform init` to allow Terraform to install or adjust the modules. Then, run `terraform apply` to apply the changes.

## Exercise

You learned how you can create an EC2 instance using Terraform. In this optional exercise, you’ll create a database instance in Terraform. The goal of this exercise is for you to practice using Terraform and its documentation. 

### Question 

You are given the ID of a VPC created in the us-east-1 region. You will need to create a MySQL RDS database instance inside a subnet of the given VPC. The VPC contains two private subnets; the IDs of these subnets are not given to you. 

Here are the specifications of the database:

- username: should be defined as a variable with a default value of “admin_user”
- password: should be defined as a variable. Its value is specified in the tfvars file.
- port number: 3306
- database instance class: db.t3.micro (this is to determine the [memory and computation capacity of the database](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.DBInstanceClass.html))
- allocated storage: 10 GiB

From this database instance, you want to return the database hostname, username, password and port number as output values.

Here are some useful links:

- Resource [aws_db_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance), list of its [arguments](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance#argument-reference) and [attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_instance#attribute-reference).
- Resource [aws_db_subnet_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_subnet_group), list of its [arguments](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_subnet_group#argument-reference) and [attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/db_subnet_group#argument-reference).
- Data source [aws_subnets](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnets), list of its [attributes](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnets#attribute-reference).

How should you replace the question marks in these configuration files?

![[terraform_exercise_files.webp]]


> [!hint]
> - If you look at the arguments of `aws_db_instance`, you will notice that you need to specify a name for a subnet group when you don’t want the database to be launched in the default VPC. In Terraform, you can create the subnet group as another resource block in the main file and then use its attributes in the database resource block. The subnet group should consist of at least two subnet ids, and each subnet should reside in a different availability zone. This is an AWS requirement (for more info, check [here](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_VPC.WorkingWithRDSInstanceinaVPC.html#Overview.RDSVPC.Create)). You can assume that the given VPC contains two subnets where each subnet belongs to a different availability zone.
> - In the main file, the first data block (of type aws_subnets) gets you the subnet IDs of the given VPC.

> [!success]- Solution
> When you're ready, check out the solution provided below
> ![[terraform_exercise_solution.webp]]

---
Next, let's [[Implementing DataOps with Terraform]]!