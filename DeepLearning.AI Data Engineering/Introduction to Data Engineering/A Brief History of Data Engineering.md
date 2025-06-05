> [!quote] Data is everywhere

Data comprises the building blocks of information, and it can take many forms—words, numbers, or even intangible phenomena like photons from distant stars or the wind brushing against your face. These diverse forms of data can be recorded in various ways: as memories in your brain, as writings on paper, or in digital formats. 

In a sense, data has existed in some form since the dawn of time. However, we refer to data as **digitally recorded data**—the kind stored on computers or transmitted over the internet.

## The early days: 1980 to 2000, from data warehousing to the web

The story of digital data begins in the 1960s with the advent of computers. It was then that the first computerized databases were introduced. 

![[data_engineer_history_60s.svg]]

Then in the 1970s, relational databases emerged, which led IBM engineers to develop **Structured Query Language (SQL)**. 

![[data_engineer_history_70s.svg]]

In the 1980s, Bill Inmon pioneered the first data warehouse, designed to transform data into a form that could support analytical decision-making.

![[data_engineer_history_80s.svg]]

By the 1990s, as data systems expanded, businesses needed dedicated tools and data pipelines for reporting and business intelligence. It was during this time that Ralph Kimball and Bill Inmon developed their respective data modeling approaches for analytics.

![[data_engineer_history_90s.svg]]

The mid-1990s marked the mainstream adoption of the internet, giving rise to a new generation of web-first companies like Amazon. The subsequent  dot-com boom fueled rapid growth in web applications and the development of backend systems—servers, databases, and storage solutions—to support them. 

![[data_engineer_history_90s2.svg]]

## The early 2000s: The birth of contemporary data engineering

After the dot-com bust in the early 2000s, a few survivors, such as Yahoo, Google, and Amazon, emerged as tech giants. Initially, these companies relied on traditional relational databases and data warehouses from the 1990s. However, these systems couldn’t handle the unprecedented explosion of data they faced. This marked the beginning of the **big data era**.

![[data_engineer_history_20s.svg]]

> [!info] Big Data
> “*extremely large datasets that may be analyzed computationally to reveal patterns, trends, and associations, especially relating to human behavior and interactions.*” —The Oxford Dictionary

Another popular way to describe big data is through the **three Vs**: **velocity** (speed at which data is generated), **variety** (diversity of data types), and **volume** (sheer amount of data).

![C1_W1_page-0025.jpg](A%20Brief%20History%20of%20Data%20Engineering%20180c79dde3538047818af8e7fe4374dd/C1_W1_page-0025.jpg)

In 2004, Google published a groundbreaking paper on **MapReduce**, a ultra-scalable data processing paradigm. This was a pivotal moment in data technology and laid the cultural foundation for modern data engineering. 

![C1_W1_page-0026.jpg](A%20Brief%20History%20of%20Data%20Engineering%20180c79dde3538047818af8e7fe4374dd/2e1b39bd-c06c-4afc-97eb-97f8d6ab5567.png)

Inspired by Google’s work, Yahoo developed and open-sourced **Apache Hadoop** in 2006. Hadoop’s impact cannot be overstated—it attracted software engineers interested in large scale data problems and marked the birth of the **big data engineer**.

Around the same time, Amazon faced its own data challenges and created **Amazon Elastic Compute Cloud (EC2)**, a scalable computing environment, and **Amazon S3**, an infinitely scalable storage system. They also developed **DynamoDB**, a highly scalable NoSQL database, and other core data infrastructure. These innovations were offered to the public through **Amazon Web Services (AWS)**, the first popular public cloud platform. 

![[aws_pay-as-you-go.svg|500]]

AWS revolutionized the industry by providing a flexible, pay-as-you-go marketplace for compute and storage resources, eliminating the need for companies to invest in physical hardware. As AWS became a profitable growth engine for Amazon, other public clouds followed, including **Google Cloud Platform** and **Microsoft Azure**. The public cloud is arguably one of the most significant innovations of the 21st century, transforming how software and data applications are developed and deployed.

![[data_engineer_history_public-cloud.svg]]

The early big data tools and public cloud platforms laid the groundwork for today’s data ecosystem. The data landscape of today and data engineering as we know it now would not exist without these innovations. 

## The 2000s and 2010s: Big data engineering

By the late 2000s and early 2010s, small startups *gained access to the same cutting-edge data tools* previously reserved for tech giants. 

### Transition from batch computing to event streaming

Another revolution occurred with the shift from **batch computing** (processing data in chunks) to **event streaming** (handling data as a continuous flow of individual events), ushering in the era of **real-time big data**.

However, the term “big data” has lost some of its earlier momentum. While open-source big data tools were powerful, they were also complex and required significant maintenance. Companies often hired entire teams of big data engineers, spending millions of dollars to keep these systems running. Engineers spent more time managing tools than delivering actionable business insights.

Today, data is growing faster and larger than ever, but big data processing has become so accessible that it no longer needs a special label. Every company, regardless of size, aims to derive value from its data. As a result, **big data engineers** are now simply **data engineers**.

![[data_engineer_history_10s.svg]]

The 2010s saw the rise of **CloudFirst** strategies, open-source tools, and third-party products, making it easier than ever to work with data at scale. At the same time, data sources and formats continue to diversify and expand. Modern data engineering is increasingly about **interoperability**—connecting various technologies like Lego bricks to achieve business goals.

## The 2020s: Engineering for the data lifecycle

That brings us to the present. The role of the data engineer has never been more critical. Today, you have the opportunity to stand on the shoulders of giants, leveraging powerful, scalable tools and technologies developed by those who came before you. You also have the chance to contribute to the evolution of these tools and build the data solutions of tomorrow.

Building robust data systems is now central to business strategy across industries. As a data engineer, you play a direct role in achieving business objectives and delivering value. 

Next, we’ll look at where [data engineering fits within an organization](The%20Data%20Engineer%20Among%20Other%20Stakeholders%20180c79dde35380739abcca5257017566.md), how to identify end users and their needs, and how to translate those needs into system requirements.