This reading item contains additional notes about scheduling in Airflow, using Airflow Operators and defining dependencies between tasks.

## Scheduling Your DAG & Other DAG Parameters

When instantiating the DAG in the previous video, I specified the following parameters: `dag_id`, `tags`, `description`, `schedule`, `start_date` and `catchup`. You can also specify other DAG parameters. Check out the [Airflow documentation](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/models/dag/index.html#airflow.models.dag.DAG) to learn more.

In this reading item, we'll take a closer look at what the `start_date` parameter does. When you orchestrate your pipeline in Airflow, you may encounter the terms "_data interval_ " and "_logical date"_ in the Airflow UI or in the Airflow documentation. Each DAG run is associated with a data interval that represents the time range it operates in. Let’s say you instantiated a DAG to run daily using the cron preset `@daily` and the start date is March 1. As shown in the following figure, each DAG run operates in a data interval that starts each day at midnight (00:00) and ends at midnight (24:00).

![[airflow_data_interval.webp]]

The “logical date” is a term associated with a specific DAG run, and it denotes the start of the data interval.

![[airflow_logical_date.webp|256]]

The `start_date` argument for the DAG marks the "_logical date"_ or the start of the first "_data interval"_. 

Given a data interval, the DAG is executed at the end of the data interval, not the beginning. This is because Airflow was developed as a solution for ETL needs, where you typically need to aggregate data collected over a time interval. So if you want to analyze the data for March 1, you would need to wait till March 2 midnight after all data for March 1 becomes available. This is why a DAG is always executed at the end of the data interval, and the logical date of a DAG run (start of the data interval) represents the date _**for**_ which the DAG run is executed, not when the DAG is actually executed. So the first DAG run will only be scheduled one interval after start_date.

**Check out these links if you want to learn more about scheduling in Airflow:**

- [Data-interval](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/dag-run.html#data-interval)
- [What does execution date mean?](https://airflow.apache.org/docs/apache-airflow/stable/faq.html#what-does-execution-date-mean) 
- You can customize your DAG scheduling using  [timetables](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/timetable.html). In addition to scheduling DAGs, you can make your DAG data-aware, meaning that it is triggered when a data object is updated in another task. Here's an [example](https://airflow.apache.org/docs/apache-airflow/stable/authoring-and-scheduling/datasets.html) of this.

## Airflow Operators

You learned about some of the Airflow operators such as EmptyOperator, PythonOperator, BashOperator, EmailOperator. You can learn more about these operators by checking out the [Airflow documentation](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/index.html). In addition to those [core operators](https://airflow.apache.org/docs/apache-airflow/stable/operators-and-hooks-ref.html) provided by Airflow, there’s a [list of other operators](https://airflow.apache.org/docs/apache-airflow-providers/operators-and-hooks-ref/index.html) that are released independently of the Airflow core that allows you to connect to external systems. For example, [this link](https://airflow.apache.org/docs/apache-airflow-providers/operators-and-hooks-ref/index.html) shows all the possible operators that you can use to interact with each AWS service, and [this link](https://airflow.apache.org/docs/apache-airflow-providers/operators-and-hooks-ref/software.html#transfers) includes the operators you can use to copy data, for example, from a database to S3. It is generally recommended to use the available operators instead of writing your own code from scratch.

In the previous video, the two parameters that were specified in the PythonOperator were `task_id` and `python_callable`. You can always review the [Airflow documentation](https://airflow.apache.org/docs/apache-airflow/stable/_api/airflow/operators/python/index.html#airflow.operators.python.PythonOperator) to see what other parameters you can specify for PythonOperator. [Here](https://airflow.apache.org/docs/apache-airflow/1.10.13/_api/airflow/operators/index.html#package-contents) is another set of parameters that you can pass to any operators, it includes the following parameters:

- email (str or list[str]): the ‘to’ email address(es) used in email alerts. 
- email_on_retry (bool): indicates whether email alerts should be sent when a task is retried
- email_on_failure (bool): indicates whether email alerts should be sent when a task failed
- retries (int): the number of retries that should be performed before failing the task

Check out this [link](https://docs.astronomer.io/learn/what-is-a-sensor) if you'd like to learn more about Airflow sensors, another special kind of operator.

## Defining Dependencies

You learned that you can use the bit-shift operator (>>) to specify the dependencies between tasks. Here are some examples:

![[airflow_task_dependencies.webp]]

## Additional References

- [An introduction to the Airflow UI](https://www.astronomer.io/docs/learn/airflow-ui)
- [Airflow UI - screenshots](https://airflow.apache.org/docs/apache-airflow/stable/ui.html#)