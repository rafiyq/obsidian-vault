Previously, we looked at the difference between [batch](Batch%20Architectures%20186c79dde35380c9b0a8c7c607299ef3.md) and [stream processing](Streaming%20Architectures%20186c79dde35380c7a0dcd1c27384abf6.md) across different stages of the data engineering life cycle. Then, you worked with an example of a data architecture where batch and streaming collaborated in the context of a recommendation system in [Building End-to-End Batch and Streaming Pipelines Based on Stakeholder Requirements](Building%20End-to-End%20Batch%20and%20Streaming%20Pipelines%20%20195c79dde35380e0ab10d96fcb0bb683.md). In this lesson, we'll take a closer look at the details of event-driven architectures and how message queues and streaming platforms work as source systems for your data pipelines.

## Terminology

First, let's define some key terms. We’ve discussed streaming data in terms of **events**, **messages**, and **streams**. Broadly speaking, an event is something that happened in the world or a change to the state of the system—for example, a user clicking a link or a sensor measuring a temperature change. In a sense, all data can be considered streaming data at its source because it consists of a record of events that occur or within a system. 

![[source_system_example.svg|256]]

A **message** is a record of information about an event. It includes details details about the event such as which button a user clicked or the temperature a sensor recorded, along with metadata and a timestamp. When messages are generated continuously, they form a **stream**—a sequence of messages such as sensor readings or website clicks over a period of time. Collectively, messages and streams make up streaming data.

![[stream_of_events.svg]]

If you process chunks of this data over a specific time interval, you’re performing **batch processing** on a stream of messages. If you process each message as it arrives, you’re working with a **streaming system**, where actions are taken based on incoming messages. In such systems, messages record event information, and actions are triggered as messages are received.

![[batch_vs_streaming_system.svg]]

## Components of Streaming System

There are three components of a streaming system: **event producer**,
**event consumer**, and **event router—**also known as **streaming broker** that sits between the producer and the consumer. 

![C2_W1-112.svg](Streaming%20Systems%20199c79dde35380f58512defb75505e72/C2_W1-112.svg)

1. **Event Producer** is what generates messages in a stream. This could be an IoT device, mobile app, API, or website.
	   ![[streaming_systems_component_producers.svg|256]] 
    
2. **Event Consumer (Subscriber)** is what processes each individual message. There can be multiple consumers in a streaming system. For example, in an e-commerce scenario, placing an order might trigger events for both a payment service and an inventory service. In this case, both payment and inventory service would be the event consumers. 
	![[streaming_systems_component_customers.svg]]

3. **Event Router (Streaming Broker)** acts as a buffer to filter and distribute the messages from producer to consumer. It helps decouples producer from consumer, enabling asynchronous communication between them. This means the producer doesn't have to wait for the message to be delivered to the consumer before sending another one. It also prevents message from being lost even if the consumer is not immediately available. Examples include Apache Kafka.

## Your Data System

When working with event systems as source systems, your upstream source might be a simple event producer (like an IoT device), with your system acting as both the event router and consumer. Alternatively, your upstream source could involve multiple producers, routers, and consumers, with your system serving as a downstream consumer.

![[single_event_producer.svg]]
Simple event producer

![[multiple_event_producer.svg]]
Multiple event producer

## Type of Streaming Systems

In data engineering, you’ll encounter two main types of streaming systems: **message queues** and **streaming platforms**. While they share similarities, the key difference lies in how the event router operates.

### Message Queues

In a message queue, the event router acts as **a queue/buffer that accumulates messages** sent by the producer. The event consumers read messages in a first-in-first-out (FIFO) order, and once a message is acknowledged, it’s deleted from the queue. 

![C2_W1-119a.svg](Streaming%20Systems%20199c79dde35380f58512defb75505e72/C2_W1-119a.svg)

> [!info] Message Queue
> A queue/buffer that accumulates messages and delivers those messages to consumers asynchronously.

With a message queue, the event producer can push new messages at any time, and the event consumer can read them at any time. The queue acts as a *temporary storage* solution, decoupling event producers from consumers. An example is Amazon Simple Queue Service (SQS), commonly used in microservices, distributed systems, and serverless applications.

![C2_W1-119b.svg](Streaming%20Systems%20199c79dde35380f58512defb75505e72/C2_W1-119b.svg)

### Event Streaming Platforms

Here, the event producer streams events to a log—append-only record of events (as discussed in [Logs](Logs%20199c79dde3538015a669c0c06f59eaab.md)). The event router distributes messages to appropriate event consumers, who process them sequentially as a read-only operation. Unlike message queues, messages are not deleted from the log, making the data persistent. This allows for replaying or reprocessing past events—log from a past point in time. Examples include Apache Kafka and Amazon Kinesis Data Streams.

![C2_W1-121a.svg](Streaming%20Systems%20199c79dde35380f58512defb75505e72/C2_W1-121a.svg)

<aside>
<img src="https://www.notion.so/icons/info-alternate_blue.svg" alt="https://www.notion.so/icons/info-alternate_blue.svg" width="40px" />

**Event Streaming Platform**
Log: Append-only record of events

</aside>

![C2_W1-121b.svg](Streaming%20Systems%20199c79dde35380f58512defb75505e72/C2_W1-121b.svg)

## Conclusion

Streaming systems are critical source systems for data engineers. They can also be integrated into your data pipelines as part of the ingestion, transformation, and serving stages.

That’s an overview of common source systems in data engineering. Next, we’ll discuss how to [connect to these source systems](Connecting%20to%20Source%20Systems%2019ac79dde353809d9c8aef20f58124e9.md).