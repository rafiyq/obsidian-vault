## What is CDC?

Suppose you extracted and loaded data from a database into your storage system. After some time, you might need to update the data stored in your storage system to ensure that it is in-sync with the data in the source system. There are two strategies for this:

- Full snapshots or full load:  in this approach, every time you want to update the data stored in your system, you ingest the entire data from your source system, replacing the old stored data with the new updated data. If your data is tabular, fully loading the data means that you delete all the old data from the stored table and extract all rows from the source table every time you need to update your stored data. This is a straight-forward approach that ensures the consistency between the data in the source system and the data stored in your data pipeline. However for high-volume data, it can take a long time to run and it can require lots of processing and memory resources. It is more suitable for cases where there’s no need for frequent data updates.
- Incremental (differential) load: in this approach, you only load updates and changes since the last read from the source systems. For example, when loading updates from a source database, you might utilize a _last_updated_at_ column to identify the rows of data that have been updated since you last read from this source database, and then only load the updated data from these identified rows. While this approach is faster than the full load approach, especially for high-volume data, it might require more complex logic to implement. When working with databases, this process is known as Change Data Capture or (CDC).  According to the book _Fundamentals of Data engineering_, “Change data capture (CDC) is a method for extracting each change event (insert, update, delete) that occurs in a database” and making it available for downstream systems.
## **Use Cases for CDC**

- CDC helps you synchronize data across different databases, supporting continuous database replication. For example, you might have a source PostgreSQL system that supports an application and you want to periodically or continuously ingest table changes into a data warehouse to enable analytics based on the most recent data. Or if you work in a hybrid company, you might need to use CDC to capture changes in on-premises databases and apply those changes to on-cloud databases.
- CDC helps you capture every historical change for auditing and other business purposes. For example, certain businesses are required to maintain complete historic information of their customer purchases for regulatory purposes, or to extract insights that allow businesses to improve.
- CDC enables microservices to track any change in the source database. For example, consider a microservice that manages purchase orders. When a new order is placed, you can use CDC to relay information to shipment service and customer service.

## **Two approaches to CDC**

- Push: This approach requires you to implement some sort of logic or process to capture changes in the source database. Then it relies on the source database to _push_ any data updates to the target system when something changes in the source system. This method allows the target systems to be updated with the latest data in near real-time, but if you don't set this up properly, you risk losing data updates if the target systems are unreachable when the source systems try to push the changes.
- Pull: This approach requires the target systems to continuously poll the source database to check for changes and then _pull_ in data updates when they happen. This method typically results in a lag before the target systems pull in any new data updates because the changes are usually batched between pull requests.

## **CDC Implementation Patterns**

There are several methods for how CDC can extract changes from databases.

- **Batch-oriented or query-based CDC (pull-based)**: In this approach, you query the database itself to identify if there has been a change in data. In the case of relational databases, this requires that the database has an additional column labeled as _updated_at_, _last_updated_ or _last_modified_ that helps you find all updated rows past a certain specified time. This process allows you to extract changes and incrementally update a target table. However, this approach can add computational overhead to the source system because target systems have to scan each row in the table to identify the last updated values. 
- **Continuous or log-based CDC (pull-based)**:  Instead of running periodic queries to get the table changes as a batch, you can treat each update to the database as an event using continuous CDC. This type of CDC relies on checking the database log. A database log records every change to the database sequentially  (e.g., every create, update, delete) and is used in case of a failure to restore the database state. You can read the events from this log (by writing your own code or using a CDC tool such as Debezium) and send them to a streaming platform, such as Apache Kafka. This way, you can capture data changes in real-time without incurring any computational overhead or requiring the need for an extra column in the source databases.
	![[CDC_diagram.png]]
- **Trigger-based CDC (push-based method)**:  A trigger is a stored function that you can configure to run when a specific column changes. The triggers inform the CDC of the changes in the source databases and in this way it relieves the CDC from detecting changes. However, too many triggers can negatively impact the write performance of the source database. 

## Tools for CDC

Feel free to read more about some of the common tools used to implement CDC

- [Debezium](https://debezium.io/)
- [AWS DMS](https://docs.aws.amazon.com/dms/latest/userguide/CHAP_Task.CDC.html)
- [Kafka connect API](https://limadelrey.medium.com/kafka-connect-how-to-create-a-real-time-data-pipeline-using-change-data-capture-cdc-c60e06e5306a) 
- [Airbyte log-based CDC](https://airbyte.com/solutions/database-replication)