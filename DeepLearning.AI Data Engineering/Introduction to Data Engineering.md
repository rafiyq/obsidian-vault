You’ve just been hired as a data engineer, and your company is counting on you to build the data systems that will help them achieve their goals. To succeed, you’ll need to translate the needs of stakeholders into clear system requirements and then select the right tools and technologies to bring those systems to life.

![[requirements_gathering_big_picture.svg]]
It’s all too common for data engineers to jump straight into implementation—choosing tools and technologies before fully understanding how their systems will deliver value to the organization. This approach can lead to disaster: wasted time, squandered resources, and even job loss.

That’s why, we’ll spend a significant amount of time focusing on the big picture. We’ll explore a set of principles that apply to all data engineering projects, build a mental framework for designing successful data systems. We’ll also dive into the technical side of things. Through hands-on lab exercises, you’ll work with cutting-edge tools and technologies to build data systems on the AWS Cloud.

## High level look at the field of data engineering

- [[Data Engineering Defined|Data Engineering lifecycle]]
- [[A Brief History of Data Engineering]]
- [[The Data Engineer Among Other Stakeholders]]
- [[Business Value]]
- [[System Requirements]]
- [[Requirements Gathering Conversation]]
- [[Translate Stakeholder Needs into Specific Requirements]]
- [[Thinking Like a Data Engineer]]

This module is all about **how to think like a data engineer**. Developing the mindset of a data engineer is the foundation for success in this field. With the right high-level knowledge and mindset, everything else in data engineering becomes achievable. Without it, no amount of technical expertise or coding skills will be enough to save you. 

## Data engineering lifecycle and undercurrents

It’s important to note that this module material focuses on building a **high-level mental framework** for data engineering rather than diving into the technical details of building data infrastructure. Establishing this foundational understanding is critical to your success as a data engineer. Once you have this framework in place, you’ll be better equipped to tackle the practical aspects of your work.

### The lifecycle

**Data engineering life cycle** begins with **data generation** from source systems. This stage typically occurs before your role as a data engineer begins. From there, we’ll explore the key stages of the lifecycle:

1. [[Data Generation in Source Systems]]
2. [[Ingestion]]
3. [[Storage]]
4. [[Queries, Modeling, and Transformation]]
5.  [[Serving Data]]

In simpler terms, you’ll learn how to take raw data from its source, transform it into something valuable, and make it accessible for downstream applications.

### The undercurrent

A decade ago, the role of a data engineer was largely focused on the technical layer. However, with the abstraction and simplification of tools, the scope of the role has expanded. Today, data engineering encompasses much more than just tools and technologies—it’s moving up the **value chain**, which is excellent news for data engineers.

Modern data engineering now integrates **traditional enterprise practices** like data management and cost optimization, as well as **emerging practices** such as **DataOps**. These practices are essential and apply throughout the entire data engineering life cycle. We refer to these practices as the **undercurrents** of the data engineering life cycle:

1. [[Security]]
2. [[Data Management]]
3. [[Data Architecture]]
4. [[DataOps]]
5. [[Orchestration]]
6. [[Software Engineering]]

### Practical Examples on AWS

There are several cloud providers available, including Microsoft Azure, Google Cloud Platform, and smaller niche providers. As a data engineer, the platform you work on will depend on your organization’s needs. However, the core concepts you’ll learn in these lessons are universally applicable, regardless of the cloud platform. The main differences will lie in the specific tools and implementation details.

We’ll focus on AWS, a leading cloud provider, as an example. This will allow you to develop the technical skills required for data engineering using tools and technologies widely adopted by thousands of companies worldwide.

We’ll introduce you to some of the key tools and explain how they fit into the data engineering lifecycle and undercurrents. In the lab exercise, we’ll get hands-on experience building **end-to-end cloud data pipeline** and exploring how this framework applies in practice on the **AWS Cloud**.

## Principles of good data architecture

In module 2, we explored the fundamentals of data architecture and discussed how adopting an architect’s mindset can set you up for success as a data engineer—even if "data architect" isn’t your official title. We’ll take a deeper dive into what it means to design effective data architecture.

We’ll begin by examining how data architecture fits into the larger picture of enterprise architecture—the overarching framework that shapes your entire organization. From there, we’ll explore real-world examples of data architecture and discuss how to translate stakeholder needs into informed technology decisions for your data systems. Along the way, I’ll share key principles to guide you as you develop your architectural thinking.

In the lab exercises, you’ll evaluate critical trade-offs—such as cost, performance, scalability, and security—within a real-world data architecture on the AWS cloud. You’ll also have the opportunity to explore the **AWS Well-Architected Framework**, a set of best practices designed to help you build robust and efficient data systems.



## Design and build out a data architecture

### Requirements Gathering

![C1_W4_2-4.svg](attachment:28bab494-570d-4bf7-8a12-fbeecce46d9c:C1_W4_2-4.svg)

In the first module of this course, we explored the fundamentals of requirements gathering and its importance in your role as a data engineer. We examined how a typical conversation might unfold between you and a data scientist at your company, focusing on their needs for analytics and machine learning projects. Through this example, you saw how such discussions often reveal the need to engage with additional stakeholders, such as the marketing team and software engineers, to fully understand the scope of the project.

### Thinking Like a Data Engineer

We also introduced a framework to help you think like a data engineer. This framework begins with identifying business goals and stakeholder needs, followed by defining system requirements based on those needs. Next, you choose tools and technologies that meet your requirements, and finally, you build and deploy your system.

![C1_W4_5.svg](attachment:9a1cb3aa-cb9c-4fdd-8626-86b50d75d0c9:C1_W4_5.svg)

While this framework provides a high-level overview, each step involves deeper layers of detail. For instance, the first step involves understanding the actions stakeholders will take, while the second step requires translating their needs into specific system requirements. The third step includes prototyping and testing, and the final step focuses on evolving and maintaining your system over time.

### The Complete Mental Model

Despite this framework, many nuances and practical considerations remain unspoken. Module 2 and 3 of this course were designed to address these gaps, helping you build a more comprehensive mental model of the data engineering workflow, the field itself, and what your role as a data engineer will entail in practice.

![C1_W4_9.svg](attachment:97a97ad7-9c0c-4b28-bfa4-99dac3e942be:C1_W4_9.svg)

In module 2, we delved into the stages and undercurrents of the data engineering life cycle. Here, we not only explored the technical components of data systems but also emphasized the importance of collaboration with key stakeholders, such as source system owners and downstream end users.

Module 3 took a deep dive into the principles of good data architecture. You learned about critical considerations like planning for failure and choosing common components or elements of your system design, which are essential to system design from the start. By now, you’ve gained all the foundational pieces needed to form a robust mental model for your work as a data engineer.

![C1_W4_7.svg](attachment:f775f97a-6f27-49ff-bc1f-0c138e0b47b8:C1_W4_7.svg)

### Practical on-the-job scenario

This Module, we’ll bring all these elements together in the context of a practical, real-world scenario. We’ll start with requirements gathering, move on to choosing tools and technologies, and conclude with system implementation.

![C1_W4_8.svg](attachment:69b8014e-c5b9-4b09-9705-f9cd4c68fbed:C1_W4_8.svg)

Specifically, we’ll revisit the requirements gathering conversations from Module 1 and expand on them by defining and documenting both functional and nonfunctional requirements. We’ll also explore the tools and technologies that can help you build a system to meet those requirements.