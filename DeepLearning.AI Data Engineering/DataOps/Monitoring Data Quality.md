Data observability and monitoring begin with understanding what your stakeholders need. In practice, there’s a wide range of metrics and quality criteria you could monitor in your data pipeline. 

## Data Quality Metrics 

For instance:
- **Volume**: Total number of records adjusted in each batch or over some time interval.
- **Distribution**: Range of values in a particular column stays within some thresholds.
- **Null values**: Total number of null values in a table.
- **Freshness**: The *difference* in time between *now* and the *timestamp of the most recent* record in your data.

However, instead of monitoring every conceivable metric, it’s crucial to identify and focus on the most important metrics. Trying to track everything can lead to confusion, alert fatigue, and the risk of overlooking critical issues. The key is to prioritize the metrics that align with stakeholder needs for each specific use case.

> [!important]
> What do stakeholders care about most for this use case?

For example, if stakeholders require current data—no older than 24 hours—you’ll want to monitor data "freshness" by *measuring when the latest records were ingested* and ensuring they meet the project’s expectations. 

Similarly, while accuracy and completeness are universally important, not all data components carry equal weight. For example, if your stakeholders are interested in product sales revenue:

![[what_to_monitor_example.svg]]

What to monitor?
- The purchase amounts recorded are accurate.
- Verify that all sales records were successfully ingested.
- No null values in sales record.

What may be less important?
- Product SKU numbers match the product descriptions
- Each customer's postal code was recorded correctly

## Testing Ingested Data

The most important aspects of your data will vary from project to project. The importance of communicating with source system owners to anticipate and mitigate future changes remain the same.

While communication is irreplaceable, it’s also essential to Implement checks and tests in your monitoring process. These can verify that the schema, data types, and other structural elements remain consistent over time. These checks serve as both sanity tests and early warning systems, helping to catch issues before they propagate through your pipelines.

> [!important] Testing Ingested Data
> - Build in checks or tests to verify that the schema and data types stay consistent. 
> - Identify problems as early as possible before they are propagated further down your data pipelines

## Conclusion

When it comes to monitoring data quality, there are many approaches. You could start with manual checks or custom scripts to run tests and trigger alerts. These approaches might be suitable during the initial setup or prototyping phase. 

However, today there are numerous tools available to ensure data quality and monitoring, saving you from undifferentiated heavy lifting. One of the them is Great Expectations, an open-source tool designed for testing data quality.