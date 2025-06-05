Before diving into how orchestration tools can define and run data pipelines, let’s take a step back and explore how data pipelines were managed before these tools existed. In the pre-orchestration era, the simplest way to automate a data pipeline—or any set of software tasks—was to use **Cron job**.

## Cron Job

Cron is a command-line utility introduced in the 1970s that allows users to execute a particular commands at a specified date and time. To schedule a task with Cron, you create a **Cron Job**, which consists of five numbers (representing time intervals) separated by spaces and followed by the command you want to execute. Here’s the structure of a Cron Job:

![[cron_job_structure.svg]]

For example, this Cron Job Would print "Happy New Year" to the terminal every year at midnight on January 1st. 

![[cron_job_example.svg]]

## Scheduling Data Pipelines with Cron

Let’s apply Cron jobs to a data pipeline. Suppose you have a pipeline that:

1. Ingests data from a REST API every night at midnight.
2. Performs in-flight transformations on the API data at 1 AM.
3. Ingests data from a database at midnight.
4. Combines the transformed API data with the database data at 2 AM.

![[cron_job_data_pipeline.svg]]

Here’s how you might set this up with Cron jobs:

1. **Ingest API Data:**
    `0 0 * * * python ingest_from_rest_api.py`
    This runs the `ingest_from_rest_api.py` script at midnight every day.
2. **Transform API Data:**
    `0 1 * * * python transform_api_data.py`  
    This runs the `transform_api_data.py` script at 1 AM every day, assuming the ingestion step completes within an hour.
3. **Ingest Database Data:**
    `0 0 * * * python ingest_from_database.py`
    This runs the `ingest_from_database.py` script at midnight every day.
4. **Combine Data:**
    `0 2 * * * python combine_api_and_database.py`
    This runs the `combine_api_and_database.py` script at 2 AM every day, after the previous steps are complete.

You could have written all the necessary Cron jobs to implement your pipeline and carefully timed to execute in a sequential manner, also known as **pure scheduling**. This was a common way to automate data pipelines before orchestration tools became available. In fact, many simple pipelines still rely on Cron today.

## The Limitations of Cron

While Cron is intuitive and effective for basic tasks, it has significant limitations:

- **No Dependency Management:** If a task fails, runs longer than expected, or produces unexpected results, the entire pipeline can break. There’s no automatic way to handle dependencies or adjust downstream tasks.
- **No Error-handling by default**: Without additional testing and debugging, there’s no straightforward way to identify why a task failed or what went wrong.
- **No built-in monitoring or alerts**: The lack of built-in monitoring means you might only discover a failure when downstream stakeholders report issues with the data.

## When to use Cron Job

- To schedule simple and repetitive tasks
	Example: Regular data download that doesn't need any downstream dependencies
- In the prototyping phase
	Example: Testing aspects of your data pipeline

---
Next video, we'll discuss orchestration tools in general and how they have evolved in [[Evolution of Orchestration Tools]].