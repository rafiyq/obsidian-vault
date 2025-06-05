The principles and practices of observability and monitoring are foundational pillars of DataOps, originating from software development practices. 

Over the past decade, the rise of cloud computing and distributed systems has driven software engineers to develop advanced observability tools. These tools provide teams with critical insights into system health, enabling them to monitor metrics like CPU and RAM usage, response times, and more. This visibility helps:

- Quickly detect anomalies
- Identity problems 
- Prevent downtime
- Ensure reliable software products

![[observability_tools_history.svg]]


Similarly, data engineers can leverage these observability tools to monitor the health of their data systems. While software teams focus on system performance metrics like CPU usage or response times, data engineers must also prioritize **data quality**. 

## What is High Quality Data?

High-quality data is accurate, complete, discoverable, and delivered in a timely manner. It aligns with stakeholder expectations, adhering to well-defined schemas and data definitions. Conversely, low-quality data—inaccurate, incomplete, or unusable—can be more harmful than providing no data at all. Decisions based on poor-quality data can lead to significant financial losses and erode trust in the data team.

| High quality data            | Low quality data |
| ---------------------------- | ---------------- |
| Accurate                     | Inaccurate       |
| Complete                     | Incomplete       |
| Discoverable                 | Hard to find     |
| Available in a timely manner | Late             |

For instance, if a software application crashes or a webpage returns a 404 error, the issue is immediately apparent, triggering alerts for engineers to resolve. If the system stops functioning entirely and the issue is immediately apparent, this is actually the **best-case scenario** for a failure. Because you can quickly identify the problem, debug it, and restore the system to full operation.

In contrast, data systems can fail in more subtle ways. The challenge lies in the fact that data systems producing low-quality data may appear healthy on the surface.  A system might continue functioning but no longer providing high quality output, which can have far-reaching consequences.

Consider this hypothetical scenario: Imagine you’re a data engineer at a U.S.-based company selling products in Europe. You’re responsible for ingesting sales data and serving it for downstream analytics. Suppose the team managing the transactional database suddenly starts recording sales prices in euros instead of dollars. Your system continues running, and the analytics dashboards still display data—but now, revenue appears to drop by 10-20% due to the currency conversion. This discrepancy triggers an emergency meeting, leading to a frantic effort to identify and resolve the issue.

![[dollar_to_euro_conversion.svg]]

While this example may seem exaggerated, similar scenarios—often more severe—have occurred in organizations worldwide. In this case, the system transitioned from delivering high-quality data to providing inaccurate or unexpected results in an instant. You might argue that the source system owners should have communicated the change, but disruptions and upstream changes are inevitable and should be expected and mitigated. Once data is in your hands, ensuring its quality becomes your responsibility.

## Conclusion

So, how can you detect and address disruptions to your data system as quickly as possible? This is where **data observability and monitoring** come into play. In the next section, you’ll hear from an expert in this field, Barr Moses. The following video is optional, so feel free to skip ahead if you prefer. Otherwise, join me for an insightful conversation with Barr on the critical role of data observability and monitoring.