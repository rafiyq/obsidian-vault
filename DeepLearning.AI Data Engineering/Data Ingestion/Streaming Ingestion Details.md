In [[Streaming Systems]], we explored message queues and event streaming platforms, from the perspective of these systems being data sources. In this context, your data pipeline acts as the consumer of these data sources. 

During our recent [[Conversation with a Software Engineer|conversation with the software engineer]], we outlined a plan for them to set up a Kinesis Data Stream, with your system acting as the consumer of messages from that stream. In this lesson, we'll delve deeper into the details of message streams.

### Apache Kafka: An Overview

Apache Kafka is an open-source event streaming platform. While there are many variations of streaming platforms, the core principles of event routing and storage are similar across platforms. At a high level: 

- **Event producers** send (or push) messages over the network to a **Kafka cluster**, which consists of one or more servers (called brokers).
- **Event consumers** read (or pull) messages from the Kafka cluster.

Within a cluster, message streams are split up and routed into **topics**. Think of a topic as a categories to hold related events. Topics can contain any type of messages, such as fraud alerts, customer orders, or temperature readings from IoT devices. It’s the producer’s responsibility to send messages to the appropriate topic. 

![[kafka_diagram.svg]]

Each topic is divided into one or more **partitions** (logs)—ordered immutable sequences of messages that continuously append new messages. More partitions allow for greater throughput, and each partition handles a subset of messages. This allows for more efficient traffic or message flow.

![[kafka_topic_diagram.svg|500]]

The producer decides which partition to send a message to, often using strategies like **round-robin** or by computing the destination partition based on a **message key**. In Kinesis, these concepts are similar, but instead of topics, you have **streams**, and instead of partitions, you have **shards**.

![[kenesis_kafka_diagram.svg]]
### Consumer Groups

On the consumption side, **consumer groups** subscribe to one or more topics. Consumers within a group work together to consume messages from all partitions of a topic. Each partition is assigned to a single consumer within the group, ensuring that each consumer handles a distinct subset of partitions. When a producer publishes a message to a topic partition, it is delivered to one consumer within each subscribing consumer group.

Once a message is published to a topic, Kafka Cluster retains that information for a configurable period, regardless of whether they’ve been consumed. This allows consumers to replay or reprocess messages as needed.

## Practical Solutions

In our conversation with the software engineer, we learned that user actions on the website are recorded as messages in the web server log. These messages will be routed to a Kinesis Data Stream. Alternatively, they could be routed to a Kafka topic, where you could consume them by subscribing to that topic under a different set of circumstances. 

![[kafka_pipeline_example.svg]]

You could also imagine a scenario where you have direct access to monitor the web server log for new messages. In this case, the web server log itself acts as the event producer, and events could be ingested into a Kafka topic or Kinesis stream as the first step in your ingestion pipeline.

Another common use case is monitoring database activity through **[[What is Change Data Capture (CDC)|continuous change data capture (CDC)]]**. By processing the database log, you can stream data changes into your pipeline, ensuring that your data remains synchronized with updates in the source database.

Next, we'll walk you through the details of **[[Kinesis Data Streams Details|Amazon Kinesis Data Streams]]**, which we’ll use as the streaming ingestion solution.