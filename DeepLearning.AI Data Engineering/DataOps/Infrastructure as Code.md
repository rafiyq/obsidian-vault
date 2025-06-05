**Infrastructure as Code (IaC)** allows you to programmatically define, deploy, and manage your cloud infrastructure. This approach enables you to automate the creation of all the resources required for your cloud data pipelines, including networking, security, computing, storage, and other data management and analytics resources. 

## History

While IaC is closely associated with cloud computing, its roots trace back to the 1970s, when engineers began grappling with the challenges of configuring and managing physical machines efficiently. Back then, they used **BASH scripts** to automate certain tasks—a practice that can be seen as the early precursor to modern IaC.

The advent of **AWS EC2 in 2006** revolutionized cloud computing by allowing users to easily spin up resources on demand. This capability enabled engineers to build more scalable applications with complex dependencies. By the early 2010s, tools like **Terraform**, **CloudFormation**, and **Ansible** emerged, empowering developers to provision and configure infrastructure using code-based configuration files. Today, these tools allow you to manage infrastructure resources on the cloud with just a few lines of code, eliminating the need for manual setup or tedious BASH scripting.

For example, in the [[An Example of the Data Engineering Lifecycle|first lab exercise]], you provided with architecture diagram for a data pipeline. Behind the scenes, we used **CloudFormation** to automate the creation of networking resources including the VPC, subnets, an RDS database, and an S3 bucket. You also ran **Terraform scripts** to deploy other components, such as the Glue ETL job and Glue crawler.

![[first_lab_diagram.svg]]

For now, we’ll focus primarily on **Terraform**, as it’s the tool you’ll use in the upcoming lab. However, it’s worth noting that **CloudFormation** is another popular IaC tool, especially for AWS-native environments. Both tools are well-documented and widely supported, and depending on your organization, you may work with one or both.

## Terraform configuration file

Now, let’s dive into the **Terraform configuration files** you used to create the Glue ETL job and S3 bucket for your data pipeline. Here’s a closer look at part of the S3 configuration file:

![[terraform_config_file_anatomy.svg]]

1. Set up the S3 bucket
2. Configure the bucket and provide public access to it

The syntax is straightforward: It follows a simple pattern where you start with the keyword `resource`, specify the resource type (e.g., `aws_s3_bucket`), and assign a name (e.g., `data_lake`). Inside the curly braces, you define configuration options using key-value pairs.

## Terraform Language

This configuration file is written in **HCL (HashiCorp Configuration Language)**, a domain-specific language developed by HashiCorp, the creators of Terraform. HCL allows you to manage infrastructure across multiple cloud providers. For instance, here’s how you might create a VPC and EC2 instance in AWS:

![[HCL_syntax_vpc_ec2.svg]]
 
Similarly, you can provision a **GCP Compute Engine instance** using Terraform:

![[HCL_syntax_gcp.svg|400]]
 
Notice how the code follows the same pattern across providers, with only the resource type and provider-specific details changing.

HCL is a **declarative language**, meaning you just have to declare what you want the infrastructure to look like—what resources you want to create and what values you want the configuration parameters to take. This is also known as the desired end state of the infrastructure. Terraform then determines the steps required to achieve that state. This makes Terraform **idempotent**: running the same configuration multiple times will not create duplicate resources. Instead, Terraform ensures the infrastructure matches the desired state. For example, if you define five EC2 instances in your configuration, Terraform will:

1. Check if the instances already exist.
2. Create missing instances or update existing ones to match the desired configuration.
3. Do nothing if the infrastructure already matches the desired state and notify that it didn't make any changes. 

This contrasts with imperative or procedural languages like BASH, where running the same script repeatedly could result in duplicate resources or unintended changes.

## Conclusion

We’ll focus on Terraform because of its versatility across cloud providers and its popularity among software and data engineers. That said, there are other IaC tools available, each with its own strengths.

Next, we’ll explore [[Data Observability]]. But first, I’ll walk you through the steps of [[Terraform - Creating an EC2 Instance|creating resources in Terraform]].