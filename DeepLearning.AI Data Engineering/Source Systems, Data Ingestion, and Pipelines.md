In the [[Introduction to Data Engineering]], you gained a high-level overview of the field, explored the principles of effective data architecture, and learned how to translate stakeholder needs into system requirements and tools. Building on that foundation, this course focuses on the first two stages of the data engineering lifecycle: **data generation and source systems**, and **data ingestion**.

We’ll dive into understanding source systems, ingesting data effectively, and orchestrating and monitoring pipelines to ensure data quality, performance, and reliability. These principles apply across a wide range of data workflows, whether you’re working with structured tabular data or unstructured data like text, images, and video. Even in cutting-edge AI applications, such as training large language models, a significant portion of the effort is dedicated to addressing data-related challenges.

In this course, we’ll cover not only structured data from databases but also unstructured data, which is becoming increasingly prevalent. As the volume of unstructured data continues to grow, data engineers must adapt to these evolving demands. While structured data has historically driven most of the value in data engineering, the future will likely see a shift as our ability to process and derive insights from unstructured data improves.

## Common source systems

In this module, we’ll explore the various types of source systems and how you can interact with them. While, as a data engineer, you typically aren’t responsible for generating this data or maintaining these systems, **ingestion from source systems** is where your data pipelines begin.

This makes it essential to understand:

- How is data generated?
- Where and how is it stored?
- What are its characteristics?

With this knowledge, you’ll be equipped to build robust data pipelines that effectively leverage these upstream systems as your data source.

We’ll dive into the details of some common source systems, including **different types of databases, object storage, and streaming sources**. In the lab exercises, you’ll get to work directly with these systems on **AWS**, gaining practical experience that will set the foundation for the rest of the course.

## Setting up ingestion from source system

Data engineer role involves three key steps:

1. Get raw data
2. Turn it into something useful
3. Make it available for downstream use cases

The first step—**get raw data** from its source. This source could be a database, an API, a set of files, or even a streaming system. We’ve already performed data ingestion in several labs. For example: 

- [Ingested data from an Amazon RDS MySQL database into S3 storage using an AWS Glue ETL job]([[An Example of the Data Engineering Lifecycle]]).  
- [Ingested data from AWS Kinesis Data Streams, using Kinesis Firehose to deliver events to an S3 bucket]([[Building End-to-End Batch and Streaming Pipelines Based on Stakeholder Requirements]]).
- [Troubleshooted common connection issues when connecting to a database]([[Troubleshooting Database Connectivity on AWS]]).

We’ve already built a solid foundation in data ingestion and we’ll add depth and detail on this existing knowledge. Here’s what we’ll cover:

1. [**Batch and Streaming Ingestion Patterns**]([[Data Ingestion on a Continuum]]): We’ll explore how to process data in chunks (batch) versus continuous stream of data (streaming).  
2. **[[Conversation with a Marketing Analyst]]**: Identify requirements for batch ingestion from a REST API.  
3. **[[Conversation with a Software Engineer]]**: Investigate requirements for streaming ingestion, including characteristics of the data payload (individual messages), event rates, and how to configure the streaming pipeline to ensure data reaches its destination.  

Finally, we'll build on this knowledge into solutions for:

- [Batch data Processing from a Rest API]([[Batch Data Processing from an API]])
- [Streaming ingestion]([[Streaming Ingestion Lab]]) from a web server log

## DataOps undercurrent

DataOps is a set of practices and cultural habits centered around building robust data systems and delivering high-quality data products. It draws heavily from **DevOps**, a set of practices and cultural habits that allow software engineers to efficiently deliver and maintain high quality software products. It also blends elements of software engineering and data management. 

We’ll explore the **three pillars of DataOps**:  
1. **Automation**  
2. **Observability and Monitoring**  
3. **Incident Response**  

We’ll spend more time on automation and observability/monitoring, that’s not to say incident response is less important—it’s a critical part of DataOps, but it’s more focused on cultural habits, which are harder to simulate in a lab setting.

When it comes to automation, we’ll revisit concepts like Continuous Integration and Continuous Delivery (CI/CD) and dive deeper into Infrastructure as Code (IaC). IaC involves writing code to automatically deploy the resources needed for your data pipelines, rather than manually spinning up instances and installing software.

- [[DataOps Automation]]
- [[Infrastructure as Code]]

It's becoming common practice to do resources deployment through infrastructure as code frameworks rather than manually spinning up instances and installing software. IaC frameworks like **CloudFormation** and **Terraform** are becoming the standard. 

- [[Terraform - Creating an EC2 Instance]]
- [[Terraform - Defining Variables and Outputs]]
- [[Terraform - Defining Data Sources and Modules]]

You’ll get hands-on experience writing Terraform code to deploy infrastructure and on top of your infrastructure to include monitoring data quality and other observability metrics. 

- [[Implementing DataOps with Terraform]]

In subsequent labs, you’ll build on this foundation to implement **data quality monitoring** and other **observability metrics**.

- [[Data Observability]]
- [[Monitoring Data Quality]]
- [[Great Expectations]]
- [[Amazon CloudWatch]]

We’ve also lined up exclusive interviews with industry experts in DataOps, focusing on data quality and observability.

- [[Data Quality with Barr Moses]]

## Orchestration, monitoring, and automating data pipeline

Orchestration is a core component of DataOps, intertwined with two of its three key pillars: **Automation** and **Observability & Monitoring**. It’s also closely related to other aspects of the data engineering lifecycle, such as **data management** and **software engineering**.

We'll automate individual tasks within data pipeline and transition from the concept of infrastructure as code, data quality checks and monitoring to the concept of pipelines as code using orchestration platform. 

- [[Before Orchestration]]
- [[Evolution of Orchestration Tools]]
- [[Orchestration Basics]]

With airflow, you'll build in data quality checks and additional monitoring as well. You’ll learn how to build a simple **DAG (Directed Acyclic Graph)** in Airflow


There are a number of different orchestration tools on the market today, and many of the concepts we'll be covering this week are tool agnostic. However, the Number 1 tool being used in industry today is Airflow. 