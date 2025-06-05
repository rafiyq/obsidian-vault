At its core, nearly all data can be thought of as a continuous stream of events. These events could represent real-world occurrences, such as stock price fluctuations, a sports team scoring a goal, or a user clicking a button on a website. In this context, we focus on the digital data generated when such events are recorded through code execution.

![[stock_exchange.webp]]
![[customer_shopping.webp]]

When it comes to data ingestion, the key idea is that data is generated as an unbounded, continuous stream of events—meaning it has no specific beginning or end. If you process these events individually as they occur, that’s **stream ingestion**. If, however, you impose boundaries on the stream and process the data within those boundaries as a single unit, that’s **batch ingestion**.

![[stream_ingestion.svg]]
![[batch_ingestion.svg]]

There are several ways to define these boundaries. For example, you could segment data by size (e.g., 10 GB chunks), by the number of records (e.g., every 1,000 events), or, most commonly, by time (e.g., daily or weekly intervals). As you increase the frequency of batch ingestion—say, from hourly to minute-by-minute—you eventually approach the realm of streaming. 

![[size-based_batch_ingestion.svg]]
![[batch_ingestion_weekly.svg]]
![[time-based_batch_ingestion.svg]]

This illustrates that batch and stream processing aren’t entirely distinct; rather, they exist on a continuum. Where your data pipeline falls on this continuum depends on the *source system* and the *end use case* you’re addressing.

## Ingestion Frequency

Historically, batch processing involved moving and processing large chunks of bounded data as single units. However, as tools and technologies have advanced, it’s become possible to process smaller chunks of data more frequently. In recent decades, **micro-batch processing** tools have emerged, which blurs the line between batch and streaming. 

![[Ingesting_Frequency.svg]]

There’s no strict industry standard for what constitutes batch versus micro-batch, or how close to real-time processing must be to qualify as streaming. In practice, your approach will depend on:

- the source systems you’re working with
- the end use case
## Ways to Ingest Data from Databases

For some databases, you can use connectors like JDBC or ODBC,%%  as we briefly discussed last week %% allow you to:

-  Ingest data either at regular intervals 
-  Ingest when a specific volume of new data is recorded 

Alternatively, you can leverage serverless ingestion tools like AWS Glue ETL, which can be configured to connect to a source database and automate data ingestion on a scheduled basis.

![[ingest_from_databases-connector.svg]]
![[ingest_from_databases-glueETL.svg]]

## Ways to Ingest Data from APIs

When [[Batch Data Processing from an API|ingesting data from APIs]], you’ll need to establish a connection based on the API’s specific protocols and adhere to its constraints and limitations.
These limitations may include 

 - How much can you ingest in one go?
 - How frequently can you call the API?

Unfortunately, there’s no universal standard for API-based data exchange, which can make this process challenging. It often involves

- Reading API documentation
- Communicating with data owners
- Writing custom API connection code

The industry is moving toward vendor-provided API client libraries that remove the complexity of API access and managed data platforms that simplify connectivity. If possible, leverage existing solutions and reserve your custom connection work for situations where no alternatives exist.

## Ways to Ingest Data from Files

For file-based ingestion, you might work with object storage systems or, in some cases, **manually download files** sent directly to you. Common **file transfer protocols** include 

- SFTP: Secure File Transfer Protocol
- SCP: Secure Copy
## Ways to Ingest Data from Streaming Systems

If you’re dealing with IoT or sensor data, you’ll likely need to set up a message queue or streaming system, regardless of whether you ultimately plan to process the data in batches or as a stream.

![[Message_Queue_or_Streaming_Platform.svg]]
## Conclusion

The best way to become comfortable with these ingestion patterns is through hands-on practice. This week’s materials are designed as two case studies:

- [[Batch Data Processing from an API|Batch ingestion from an API]]
- [[Streaming Ingestion Lab]] from a Kinesis data stream

Learn more about [[Batch and Streaming Tools]]. Next, we’ll have a [conversation with a marketing analyst]([[Conversation with a Marketing Analyst]]) who needs to ingest external data from an API.