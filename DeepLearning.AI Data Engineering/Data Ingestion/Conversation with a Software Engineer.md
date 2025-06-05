Let’s dive deeper into streaming ingestion. We’ll have follow-up conversation with a software engineer to discuss the ingestion details for the recommender system.

---

> **Data Engineer**: *Thanks for joining me. I’m setting up a new product recommender system and would like to better understand how we can ingest real-time user activity data from the website. Can you walk me through how the data is currently being collected?*

> [!tips]
> Learn more about the **existing** data system 

> **Software Engineer**: *Absolutely. The system continuously records events in the web server log. These events include internal system performance metrics, errors, anomalies, and user activity—like button clicks, product views, and purchases.*

> **Data Engineer**: *Ideally, I’d like to ingest only the user activity data, excluding internal system metrics. Would it be possible to separate user activity events and push them into a separate log for ingestion?*

> **Software Engineer**: *Definitely. We can push user activity messages into a Kafka topic or Kinesis stream, which you can then ingest directly into your pipeline.*

 > **Data Engineer**: *That sounds good. A Kinesis data stream would work well for me since I’ve been exploring its use for other parts of the pipeline. Could you also share details about the format of data payload and the expected message rate?*
 
 > [!tips]
> Learn about the specific **data payload and message rate** of the existing data system

> **Software Engineer**: *Sure. The messages are in JSON format, containing a session ID, customer information (like location), and browsing activity (e.g., products viewed or added to cart). Each message is typically a few hundred bytes in size. As for the message rate, it varies based on user traffic. A single user might generate several events per minute, and during peak times, we could have around 10,000 users on the platform. That could translate to roughly 1,000 events per second.*

 > **Data Engineer**: *Got it. So, back-of-the-envelope math suggests around 1,000 events per second, each a few hundred bytes in size. That’s less than 1 MB per second, which is well within the capacity of a Kinesis data stream. They can handle hundreds of megabytes per second, depending on the configuration.*

> **Software Engineer**: *Exactly. Another thing to configure is how long messages are retained in the stream. The stream essentially append-only log, but we can set it up to remove messages after a certain period.* 

 > **Data Engineer**: *Right. Since we’ll be using the data in real-time to make recommendations and saving the model’s inputs and outputs of the recommender model for later analysis, we shouldn’t need to reread messages from the stream under normal circumstances. However, if something goes wrong, we might need to replay the stream. How about retaining messages for one day after they’re written?*

> **Software Engineer**: *Sure, let's see. On a busy day, we might write around 1 MB per second to the stream. With roughly 100,000 seconds in a day, the stream could grow to about 100 GB at peak. That seems reasonable.*

 > **Data Engineer**: *All right. Is there anything else we should discuss, or are we ready to start building?*

> **Software Engineer**: *I think we’re good to go.*

---

This conversation with the software engineer—an upstream stakeholder, highlights the importance of understanding the data source and ingestion mechanism. While there are other important topics to discuss with source system owners about potential
disruptions to the data pipeline—like schema changes and potential outages—we’ll focus for now on the data itself and the ingestion mechanism.

Let's unpack this conversation and explore [[Streaming Ingestion Details|streaming ingestion in more detail]].