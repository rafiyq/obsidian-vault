To create resources in Terraform, you’ll follow a consistent workflow. 

1. You write the configuration files to define your resources
2. Terraform prepare your workspace
	- **Installs necessary files** to communicate with cloud APIs
	- **Create an execution plan** outlining the resources it will create, update, or destroy. 
3. You approve the execution plan
4. Terraform applies the proposed steps and provisions your infrastructure

In this first tutorial, we'll dive into the details of preparing configuration files to create an EC2 instance. In the process, you'll learn more about the inner workings of Terraform and be ready to create any other resources in Terraform. 

## Creating an EC2 Instance

Let’s say you want to create an EC2 instance and launch it in the default VPC of your selected region. For this example, I’ll use the us-east-1 (West Virginia) region. I’m choosing the default VPC for simplicity, but you should launch resources in custom VPCs and reserve the default VPC for quick experimentation only.

![[creating_terraform_ec2.svg|265]]

### Writing the Configuration File

To define the EC2 instance, you’ll start by creating a configuration file.

1. Use any IDE of your choice
2. Install Terraform in your environment
3. Use AWS credentials to authenticate Terraform. 

Detailed instructions for these steps are available on the [Terraform Documentation](https://developer.hashicorp.com/terraform/docs).

Let’s create the first configuration file and name it `main.tf`. Terraform recognizes any file with a `.tf` extension as a configuration file. Terraform configuration files are typically structured into five sections:

1. **Terraform Settings**: Specify Terraform settings and required providers.
2. **Providers**: Configure the providers declared in the first section.
3. **Resources**: Define the resources you want to create.
4. **Input** (Optional): Define variables to parameterize your configuration.
5. **Output** (Optional): Define outputs to display after Terraform applies the configuration.

Each section consists of blocks of code. In Terraform, a block has a JSON-like structure. It starts with a keyword indicating the block type, followed by optional labels (as strings), and a body enclosed in curly braces. Within the body, you define arguments or nested blocks.

### The Terraform Block

The first block you’ll create is the **Terraform block**, which specifies the Terraform settings, including the required providers that Terraform will use to create your resources.

In Terraform, a **provider** is a plugin or binary file that Terraform will use to create your resources. You can find all the available providers in the [Terraform registry](https://registry.terraform.io/). Some providers allow Terraform to interact with cloud platforms (like AWS), while others provide additional functionalities.

![[terraform_provider_aws_doc.webp]]

For example, the **AWS provider** is the plugin that allows Terraform to interact with resources on AWS. It’s not referring to AWS itself. You can find the AWS provider’s documentation in the Terraform Registry, which lists all available resources and their usage examples. This documentation is invaluable, as it shows the required and optional arguments for each resource.

![[terraform_settings_codeblock.webp]]

 In our example, since we’re only using AWS resources, we’ll declare the AWS provider as a required provider. For each provider, you need to specify:
 
- A **local name**: A unique identifier for the provider within the configuration file.  
- A **source location**: The global identifier specifying where Terraform can download the provider.  
- An optional **version constraint**: To ensure compatibility.  

When working with Terraform, this documentation can be really helpful because it shows you the arguments that you need to specify, in this case for any AWS resource. 

### The Providers block  
Next, you’ll create a **provider block** to configure the AWS provider. Here, you’ll specify the AWS region:

```hcl
provider "aws" {
  region = "us-east-1"
}
```  

The name `aws` corresponds to the local name assigned in the Terraform block.  

### The Resources block 

Now, let’s define the EC2 instance in the **resource block**. A resource block starts with the keyword `resource`, followed by the resource type and a name. The resource type is a string combining the provider and resource, separated by an underscore. For example, `aws_instance` refers to an EC2 instance managed by the AWS provider.

![[terraform_resources_codeblock.webp]]

You can always search for the resource type in the Terraform documentation of the AWS provider to find the name of the desired resource type you want to configure with Terraform. 

- `aws_instance` is the resource type.  
- `webserver` is the name you’ve chosen for this resource. 

Together, these form a unique ID (`aws_instance.webserver`) that you can reference elsewhere in your configuration. 

Inside the resource block, you specify the resource’s arguments. For an EC2 instance, the two required arguments are:  
1. **AMI**: A software template defining the instance’s operating environment (e.g., operating system, system architecture).  
2. **Instance Type**: The hardware specifications for the instance.

AWS provides a long list of AMIs that you can find in the AMI catalog in the AWS console.

In this example, we’ve used a recent Linux-based AMI and the `t2.micro` instance type. I’ve also added an optional tag to name the instance. 

Note that I did not specify the subnet for launching the EC2 instance. This is because I want to launch it in any available subnet within the default VPC.

## Applying the Configuration

With the configuration file ready, you can now create the EC2 instance. 


Start by running `terraform init`. This command installs the providers defined in your configuration file. In this case, Terraform downloads the AWS provider and stores it in a hidden `.terraform` subdirectory.

![[terraform_init_output.webp]]

Next, run `terraform plan`. This command generates an execution plan, showing what Terraform will create, update, or destroy based on the configuration file. 

- `+` sign indicates resources to be created, 
- `-` sign indicates resources to be destroyed, and 
- `~` sign indicates resources to be updated.

![[terraform_plan_output.webp]]
 
Finally, run `terraform apply`. Terraform will display the execution plan and wait for your approval. Type `yes` to proceed. Once completed, Terraform will create the EC2 instance as specified.

![[terraform_apply_command_output.webp]]

You can verify the instance in the AWS console.

## Conclusion

In this tutorial, we learned how to:

1. Set up a Terraform configuration file with Terraform and provider blocks.
2. Define an EC2 instance using a resource block.
3. Initialize, plan, and apply your Terraform configuration.

Next, we’ll explore other Terraform blocks and discuss how to organize your Terraform directory effectively: [[Terraform - Defining Variables and Outputs]].