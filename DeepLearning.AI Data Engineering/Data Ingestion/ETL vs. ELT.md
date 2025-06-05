In the [[Conversation with a Marketing Analyst|previous conversation]], the marketing analysts shared their goals for a project involving the incorporation of external data into their product sales analysis. For this project, the analysts plan to focus primarily on historical trends in the data. In the future, they may shift to more explicit analysis of current data, though not necessarily in real time analysis. 

The data will be sourced from a third-party API. While there is some flexibility in how often or how much data is pulled, the process will be constrained to batch ingestion. This is because API calls function similarly to web requests: you send a request for data and receive a response, and the number of requests you can make within a given time frame is typically **limited**. As a result, data ingestion for this project will follow a batch process.![[marketing_analyst_goals.svg]]

## Batch Ingestion Patterns

In a previous course, I briefly introduced ETL (Extract, Transform, Load) and ELT (Extract, Load, Transform), two common batch ingestion patterns. While these processes technically include components of the transformation and storage stages of the data engineering lifecycle, their trade-offs must also be considered during the ingestion stage.

![[ETL_diagram.svg]]
First, I’ll explain the key differences between ETL and ELT, and then we’ll determine which approach might be a better fit for our marketing analysts’ use case.

### History of ELT

ETL is the original batch ingestion pattern, gaining popularity in the 1980s and 1990s. The process begins with extracting raw data from a source system, such as a database or API. The data is then transformed in an intermediate staging area before being loaded into a target storage destination, such as a database or data warehouse. 

In the 1980s and 1990s, storage and computing power were extremely limited. As a result, it was important to plan precisely what data to ingest, how to store and access it, and in what format. Data warehouses were expensive to set up and poorly suited for complex queries involving joins and transformations. Consequently, raw data transformations had to be carefully applied during the ingestion stage to ensure efficient storage and accessibility.

ETL remains a popular ingestion pattern today. However, with the relatively low cost of cloud storage and increased computational power, it’s no longer the only option.

### Emergence of Cloud Storage Systems

In the early 2010s, cloud storage systems became highly scalable, leading to the emergence of data lakes built on object storage systems like S3 and cloud data warehouses like Redshift and Snowflake. These advancements made it possible to 

- Store enormous amounts of data for relatively cheaply
- Perform data transformations directly in the data warehouse

This gave rise to ELT, or Extract, Load, Transform.

In the ELT process, raw data is extracted from source systems and loaded directly into the target database, data warehouse, or object storage without any transformations. The key advantage of ELT is that it eliminates the need to decide upfront how the data will be used.

![[ETL_vs_ELT.svg]]

With ETL, applying transformations to raw data and storing only the processed results can lead to the loss of some information during the process. In contrast, with ELT, all options remain open as the raw data is stores, you retain the flexibility to query and transform the data later as needed, ensuring that no information is ever lost.

## Advantages of Extract-Load-Transform

At first glance, ELT might seem inefficient—why store raw data without a clear plan for its use? 

- ELT is **faster to implement** because it doesn’t require detailed upfront planning.
- It makes **data available more quickly to end users**, albeit in raw form, since it eliminates the need for a staging server and in-flight transformations.
- **Transformations can still be done efficiently after the data is loaded** into storage, thanks to the processing power of the modern data warehouse.
- By storing all of your raw data, **you can decide later to adopt different transformations** or analyze the data in different ways—options that might not have been available if only transformed data had been stored initially.

## Downside of Extract-Load-Transform

ELT is also has its downsides. If not managed carefully, your pipeline can devolve into an “EL” pipeline—extracting and loading vast amounts of raw data into storage without ever transforming it into something useful. This can lead to what’s commonly known as a **data swamp**.
![[EL_pipeline.svg]]

> [!info] Data Swamp
> Data becomes unorganized, unmanageable, and essentially useless. 

![[data_swamp_illustration.webp]]
 *"a data engineer sitting in their data swamp, surrounded by piles of raw data they thought might be valuable someday. But now, even if they could remember what’s in there, they likely wouldn’t be able to find it."*
 
 In the early 2010s, data swamps were common as companies stored every scrap of raw data “just in case.” Today, many of these swamps have been cleaned up, partly due to regulations requiring companies to store data in an auditable and deletable manner—for example, when a user requests their data be removed from company systems.

## Summary of the Differences

|                                     | ETL                                                                                                                                                                                                                                                                                                                                 | ELT                                                                                                                                                                                                                                                                                                                   |
| ----------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **History**                         | - In the 80’s and 90’s, data warehouse cost was very expensive (millions of dollars), so engineers wanted to be very intentional about the data they were about to load into the data warehouse<br><br>- Data volume was still manageable.                                                                                          | - Cloud data warehouse reduced the cost of storing and processing data significantly (from millions of dollars to hundreds/thousands of dollars only) <br><br>- Data volume exploded.                                                                                                                                 |
| **Processing (transformation)**     | - Data is transformed into a predetermined format before it is loaded into a data repository. So, data engineers have to carefully model the data and transform it into this format.<br><br>- Transformations rely on the processing power of the processing tool that is used to ingest data (unrelated to the target destination) | - Raw data is loaded into the target destination. Then it is transformed just before analytics (Can be used with not well-defined data requests)<br><br>- Transformations rely on the processing power of the data repository, such as the data warehouse.                                                            |
| **Maintenance time**                | If the transformation is found to be inadequate, data needs to be re-loaded.                                                                                                                                                                                                                                                        | The original data is intact and already loaded and can be used when necessary for additional transformation: Less time required for data maintenance.                                                                                                                                                                 |
| **Load Time & transformation time** | Load time: it typically takes longer as it uses a staging area and system. <br><br>Transformation time: it depends on the data size, the transformation complexity and the tool that is used to perform the transformation.                                                                                                         | Load time: there is no transformation involved, the data is directly loaded into the destination system<br><br>Transformation time: it is typically faster because it relies on the processing power and parallelization of modern data warehouse<br><br>(generally considered more efficient)                        |
| **Flexibility (data types)**        | ETLs are typically designed to handle structured data.                                                                                                                                                                                                                                                                              | ELT can handle all types of data: structured, unstructured, semi-structured. Once the data is loaded into the target system, you can transform it.                                                                                                                                                                    |
| **Cost**                            | It depends on what ETL/ELT tool is used and to what target system the data is loaded. (And of course, it depends on the data volume).                                                                                                                                                                                               | It depends on what ETL/ELT tool is used and to what target system the data is loaded. (And of course, it depends on the data volume).                                                                                                                                                                                 |
| **Scalability**                     | Nowadays, most of the cloud tools are scalable. However the challenge here is that if you have lots of data sources and lots of targets, you would need to put in lots of effort to manage the code and handle data from multiple sources                                                                                           | ELT uses the scalable processing power of the data warehouse to enable transformation on a large scale.                                                                                                                                                                                                               |
| **Data quality/ security**          | It ensures data quality by cleaning it first. Transformations can also include masking personal information.                                                                                                                                                                                                                        | The data needs to be transferred first to the target system before transformations that enhance data quality or security are applied. <br><br>\*There’s a sub-pattern called EtLT where small t does not refer to business modeling but to transformation with limited scope (mask sensitive data, deduplicate rows). |

## Conclusion

Given the relatively low cost of storage and the processing power of modern data warehouses, both ETL and ELT are reasonable batch processing approaches. However, regardless of the approach, it’s important to have clear goals in mind and manage your data accordingly.

 For the marketing analysts’ project, where they’ll be ingesting data from a third-party API, which typically provides semi-structured data (e.g., JSON) and, in some cases, unstructured data like text or images. Since the analysts aim to perform exploratory analysis and can’t specify upfront what transformations will be needed, an **ELT pipeline** is probably the better choice. It offers more flexibility during the transformation and storage stages, aligning well with the project’s requirements.

One key aspect of this ingestion use case that we haven’t yet explored in detail is working with an API as a data source. Next, we'll take a closer look at [[REST API|API-based data ingestion]].