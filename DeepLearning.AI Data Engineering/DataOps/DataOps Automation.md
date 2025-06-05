DataOps evolved from DevOps, but there are significant differences in the requirements for delivering high-quality software applications versus high-quality data products. Here, we’ll focus on how DataOps adopts key automation concepts from DevOps.

## DevOps Automation

In software engineering, a cornerstone of automation is **continuous integration and continuous delivery (CI/CD)**. In software, CI/CD involves setting up systems for 

- Automatic review and testing of new code
- Automatic delivery or deployment into production

![[CICD_diagram.svg]]

Similarly, in DataOps, CI/CD can be applied directly to code and data within your data pipeline.
Whether it’s code for data transformations, database population, or the data itself, these elements can be managed like any other software application code.

![[dataops_cicd_diagram.svg]]

When it comes to automating data pipeline execution, there are several approaches:

- **No automation**: run all processes manually
- **Pure scheduling**: run stages of your pipeline according to a schedule
	![[dataops_CICD_schedule_diagram.svg]]
	
- **A directed acyclic graph (DAG)**: use orchestration tools like **Airflow**
	![[dataops_CICD_airflow_diagram.svg]]

We’ll dive deeper into DAGs and the automation of testing and deployment in next discussion on orchestration.

## Version Control

A critical foundation of any CI/CD system—whether for software or data product—is **version control**. Version control tracks changes to code, enabling teams to revert to previous versions if issues arise. You might already be familiar with tools like GitHub for managing code.

![[version_control_github.svg]]

In DataOps, version control extends to data as well. Just as you can track and roll back code changes, you can track changes in data moving through your pipelines and revert to earlier versions if needed.

![[version_control_dataops.svg]]

## Infrastructure as Code

Another concept DataOps borrows from DevOps is **infrastructure as code (IaC)**. Whether you’re building software applications or data pipelines with cloud platform resources, you can define your infrastructure programmatically. This allows you to deploy, modify, and version-control your infrastructure just like any other piece of code. If you need to roll back to a previous infrastructure setup, it’s as simple as reverting to an earlier version of your code.

## Conclusion

 As you can see, DataOps automation practices are integral to data engineering. They overlap with the other undercurrents of the data engineering lifecycle aspects, such as **software engineering** (through DevOps practices) and **data management** (through version control and data lifecycle management). These practices ensure better control, reliability, and value delivery for your data products.

Next, we’ll take a closer look at **[[Infrastructure as Code|infrastructure as code]]** in the context of DataOps automation. Then, in the upcoming lab, you’ll get hands-on experience writing code to define your own infrastructure.


