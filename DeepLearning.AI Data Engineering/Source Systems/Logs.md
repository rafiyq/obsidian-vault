The simplest form of a streaming system I can think of is a log. In fact, a log isn’t even a system—it’s simply a record of information about events that tracks the activity of a system or application. Developers once viewed data generated by software applications as mere "exhaust" or a byproduct. This data wasn’t seen as inherently valuable but was useful for monitoring or debugging purposes. The most common type of data regarded as exhaust is the data contained in logs produced by software applications.

![[software_exhaust.svg]]

When developers deploy a product or platform, such as a website or mobile app, they configure it to record all activity in a log. This log might include user activity, like signing in or navigating to a particular page, as well as backend events, such as database updates or errors encountered during operations. Traditionally, logs have been used primarily to monitor system health, trigger alerts, or debug issues when errors occur. Because of this, logs might seem mundane, and the idea of them being "application exhaust" might feel fitting.

![[logs_sources.svg]]

> [!info] Log
> An append-only sequence of records ordered by time, capturing information about events that occur in systems. 

However, logs are far more than just monitoring tools—they are a rich source of data with significant value beyond system health checks. As a data engineer, you’ll often ingest data from logs for various purposes. 

For example, as a data engineer for an e-commerce company, you might use web server logs to capture detailed user activity data that could be used to support downstream analysis of user behavior patterns. Similarly, database system logs can track changes using a process called *change data capture* (CDC). This process can trigger ingestion pipelines to run automatically whenever new data arrives in the database. Logs can also feed into machine learning applications, such as anomaly detection in security systems.

In essence, logs play a critical role in tracking what happens in upstream software systems. This makes them a valuable resource for downstream use cases like data analysis, troubleshooting, performance monitoring, machine learning, and automation.

 A log typically records several key pieces of information for each event.

![[log_components.svg]]

- Identify the person, system, or service account associated with the event, such as a user ID or IP address.
- Describes the event, along with its metadata—for example, a user adding a specific product to their cart and the status of that action.
- Include a timestamp marking when the event occurred.

Log data can be stored in various formats, such as unstructured text, JSON, CSV, or even binary-encoded data.

![[log_format.svg]]
## Log Levels

Additionally, logs often include tags to categorize events by assigning *log levels* to each record. Common log levels include 

- “debug”
- “info”
- “warn”
- “error”
- “fatal”

These levels indicate the type of information a record contains. For instance, basic activity information might be tagged as ”info”, while an error message would be labeled ”error”. A ”fatal” tag might indicate a critical system failure requiring immediate attention. We’ll explore log levels in more detail later when you start integrating logs into your own data pipelines.

## Conclusion

As a data engineer, understanding how to work with logs—their types, formats, and applications—is essential. Logs are a vital data source that can help you troubleshoot issues, monitor performance, and support a wide range of downstream use cases. 

Next, we dive deeper into [[Streaming Systems|streaming systems]] and their role in data engineering.