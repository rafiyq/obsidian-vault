Data issues are inevitable and they could occur at any stage of your data pipeline. The earlier you are able to detect them, the less damage to the organization it will cause. To detect data issues, you need to first choose metrics that assess the data quality, similarly to how software teams monitor metrics that assess the health of their software's infrastructure.

In her book ([Data Quality Fundamentals](https://www.oreilly.com/library/view/data-quality-fundamentals/9781098112035/ch02.html#what_are_data_quality_metricsquestion_m)), Barr Moses suggests to start with the following questions:

- Is the data up-to-date?
- Is the data complete?
- Are fields within expected ranges?
- Is the null rate higher or lower than it should be?
- Has the schema changed?

She formulated these questions into 5 pillars for data observability, which aim to fully describe the state of the data.

## [Barr Moses 5 Pillars](https://www.montecarlodata.com/blog-what-is-data-observability/)

1. **Distribution/ Internal Quality**: The quality pillar refers to the internal characteristics of the data, and checks metrics such as the percentage of NULL elements, percentage of unique elements, summary statistics and if your data is within the expected range. It helps you ensure that your data is trusted based on your data expectation.
2. **Freshness**: Data freshness refers to how “fresh” or “up-to-date” the data is within the final asset (table, BI report), i.e., when the data was last updated, and how frequently it is updated. Stale data results in wasted time and money.
3. **Volume**: Data volume refers to checking the amount of data ingested and looking for unexpected spikes or drops. Sudden drops in data volume can indicate issues like lost data or system outages, and sudden increases may indicate unexpected surges in usage.
4. **Lineage**: According to [Barr](https://towardsdatascience.com/introducing-the-five-pillars-of-data-observability-e73734b263d5), “When data breaks, the first question is always “where?” Data lineage helps you trace the data journey from its source to its destination, visualizing how data was transformed and where it was stored. This way, you can identify the source of errors or anomalies.
5. **Schema**: Data schema refers to monitoring changes in data structure or types. This pillar helps avoid the failure of the data pipeline.

## Additional Resources

If you'd like to learn more about data observability, you can check the following additional resources.

- [Data quality fundamentals](https://learning.oreilly.com/library/view/data-quality-fundamentals/9781098112035/) , by Barr Moses, Lior Gavish, Molly Vorweck [book]
- [The rise of data downtime](https://towardsdatascience.com/the-rise-of-data-downtime-841650cedfd5), by Barr Moses [article]
- [What is data observability?](https://learning.oreilly.com/library/view/what-is-data/9781098120993/ch02.html#characteristics_of_a_data_incident) , by Andy Petrella [book]