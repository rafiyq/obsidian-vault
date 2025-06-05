Monitoring the health of your data systems ensures that all components are operating as expected. Effective monitoring allows you to detect and address issues as soon as they arise—or even anticipate and prevent them before they occur. When working with AWS resources, many services automatically send metrics to CloudWatch without requiring any setup.

## System Level Metrics

System level metrics provide a general understanding of how your resources are performing, these often include:

- CPU utilization
- Disk I/O 
- Network traffic
- Memory usage

These metrics can help you identify potential issues before they become critical. Identifying issues before your
end users do is important, and having robust monitoring in place can help you do that. 

While many AWS services automatically send metrics to CloudWatch, there are cases where you might want to send custom metrics. 

## Custom Metrics 

Custom metrics allow you to monitor specific aspects of your application that are not covered by default system metrics. For instance, you might want to track application specific data such as

- Number of transactions processed
- Response time of an API endpoint
- Number of active users

You can use CloudWatch dashboards to
visualize and monitor important metrics
from multiple components of your
system. These dashboards let you aggregate metrics from multiple system components into a single, unified view. This not only helps you diagnose issues as they arise but also allows you to analyze trends and anomalies over time.

## CloudWatch Alarms

However, you likely won’t be staring at dashboards all day. Instead, you want to be made aware when metrics reflect issues. You can set up **CloudWatch alarms** to notify you when specific metrics breach predefined thresholds. These alarms can even trigger automated actions to resolve issues proactively.

Before setting thresholds, it’s important to establish a **baseline** for your system’s performance. This involves measuring performance of your system under different loads and conditions over time. CloudWatch retains metric data for up to **15 months**. You can collect metrics for awhile before determining what the baseline is for your system.

In general, acceptable values for metrics depend on what your application is doing relative to your baseline. 

## Common Metrics for RDS

Let's explore some of the common metrics that you might be monitoring for RDS.

1. **CPU Utilization**
	- High value indicate your RDS instance might be under heavy load. 
	- Values over 80-90% can lead to performance bottlenecks.
   
2. **RAM Consumption**: High memory usage can slow down performance.

3. **Disk Space**: Value consistently exceeds 85%, you may need to archive or delete data to free up some space.

4. **Database Connections**
	- The number of active connections to your database.
	- Number of connections approaches the maximum limit can lead to connection errors and application failures.
	- Helps manage connection pooling and scale your database to handle more connections if needed. 

## Conclusion 

These are just a few examples of the metrics RDS sends to CloudWatch. Apart from CloudWatch, there are also third-party monitoring services like **Datadog** and **Splunk** that you might consider to monitor your systems. Keep in mind that each AWS service provides different metrics, and the ones you prioritize will depend on your specific use case.

Next, we'll be using Amazon CloudWatch to monitor database on AWS.