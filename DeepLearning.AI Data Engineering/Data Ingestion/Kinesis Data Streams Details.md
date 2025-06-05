Similar to Kafka, Kinesis uses **event producers** to push data into a stream and **consumers** to read data from it. Let’s explore some key details about Kinesis, especially when you’re managing the entire system—producers, consumers, and the stream itself.

## How Kinesis Data Streams Work

In **Amazon Kinesis Data Streams**, producer push data to a specific **streams** (similar to Kafka’s topics). One stream consists of multiple **shards**, which provide the units of capacity for the stream. To scale your stream and handle more data, you add more shards.

![[kinesis_data_streams_diagram.svg]]

In order to determining the number of shards you need depends on the size and rate of your **write** and **read** operations:
- **Write operations**: Producers write data to the stream.
- **Read operations**: Consumers read data from the stream.

Each shard supports:
- Up to **1,000 write records per second**, with a maximum total write rate of **1 MB/second**.
- Up to **5 read operations per second**, with a maximum total read rate of **2 MB/second**.

To calculate the number of shards required, you’ll need to analyze the expected size and rate of your read/write operations. Sometimes, estimating these can be challenging, especially for new applications or systems with highly variable traffic (e.g., e-commerce platforms). For such cases, Kinesis offers **on-demand mode** and **provisioned mode**.

 Kinesis in "on-demand" Mode:
 - Automatically manage the scaling of the shards up or down as needed
 - Only charged for what you use
 - More convenient from an operational perspective

Kinesis in "Provisioned" Mode:
- Specified the number of shards necessary for your application based on the expected write and read request rate
- Manually add more shards or re-shard when needed
- A good fit if
	- you have predictable application traffic
	- you are able to control your costs more carefully

## Data Records in Kinesis

Each data record sent to a Kinesis stream includes:

- A **partition key**: Used to determines which shard the record is placed into. When setting up the data producer for your system, you need to choose a partition key.
- A **sequence number**: Assigned by Kinesis to maintain the order of records within a shard.
- **Binary Large Object (BLOB):** A format used to store the data itself.

For example, let's say you create a stream of e-commerce transactions, you might use the **customer ID** as the partition key. This ensures all transactions for a single customer are stored in the same shard, making it easier for downstream consumers to pool records related to a single customer for aggregation and analysis.

## Processing Data in Kinesis

Producers write data to shards, and consumers read from them. It's common to have multiple consumers reading data from a shard. By default, multiple consumers share a shard’s read capacity (known as **shared fan-out**), which can lead to contention for read capacity. To avoid this, you can enable **enhanced fan-out**, allowing each consumer to read at the full **2 MB/second** capacity of the shard.

> [!info] Shared Fan-Out
> When customers share a shard's read capacity 

> [!info] Enhanced Fan-Out
> When customers are able to read at the full read capacity of the shard

You can process data in Kinesis using:
- Managed services like **AWS Lambda**, **Amazon Managed Service for Apache Flink**, or **AWS Glue**.
- Custom consumers built with the **Amazon Kinesis Client Library (KCL)**.

Kinesis also supports chaining streams, where the output of one stream becomes the input for another, enabling complex real-time data workflows. Additionally, consumers can integrate with services like **Amazon Kinesis Data Firehose** to store data in **Amazon S3**.

## Conclusion

Kinesis Data Streams allows multiple applications to work with the same stream simultaneously. Each application can consume data independently and send it to different downstream systems.

Next, you’ll get hands-on with **[[Streaming Ingestion Lab|streaming ingestion using Kinesis]]**.