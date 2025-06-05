When writing DAGs, there are some best practices that help ensure your code is efficient, readable, idempotent and reproducible (like with any code). Let’s go through some of these basic practices.

## Keep tasks simple and atomic

When you prepare your pipeline for orchestration, you need to identify the tasks or steps of your pipeline. Keep your tasks simple such that each task represents one operation. You don’t want to end up with one task that does everything, otherwise you'll lose visibility into your data pipeline and reduce the readability of your code, which does not support idempotency.  

For example, in an ETL or ELT process, you would need to create at least three tasks: extract, transform, load, instead of creating just one task that handles the entire process.

## Avoid top-level code

In the following code,

```python
call_some_function()
perform_computation()

with DAG(dag_id="example_xcom", start_date=datetime(2024, 3, 13), schedule='@daily',catchup=False):
	task_1 = PythonOperator(task_id='extract',python_callable=extract_api)
	task_2 = PythonOperator(task_id='load_data',python_callable=load)
	
	task_1 >> task_2
```

`call_some_function()` and `perform_computation()` are both high-level codes. In general any code that isn’t part of your DAG or operator instantiations is considered to be top-level code. This type of code will be executed at the time when the DAG is parsed by the scheduler. On the other hand, any code that is part of an operator is executed when the task runs, not when the DAG is parsed. Top-level code can cause performance issues because the scheduler checks the DAG directory and parses the DAG files every 30 seconds. So it may not be efficient to execute the high-level code this frequently especially if the code makes some requests to an API or a database.

## Use variables (user-created variables, Airflow built-in variables and macros)

### User-created variables

Including hard-coded values directly in your code is generally not a good practice in software development. This is because they make your code less readable and more error-prone -- you may need to use the same value in multiple places and updating the same value in multiple places can be error-prone. The same principle also applies to when you write code to define your pipelines. Instead of including hard-coded values within your DAG or task definitions, you can store these values by creating variables in the Airflow UI or creating environmental variables and use these variables dynamically inside your code.

[Recommendations from Airflow documentation regarding using Variables](https://airflow.apache.org/docs/apache-airflow/stable/core-concepts/variables.html): “Variables are global, and should only be used for overall configuration that covers the entire installation; to pass data from one Task/Operator to another, you should use XComs instead. We also recommend that you try to keep most of your settings and configuration in your DAG files, so it can be versioned using source control; Variables are really only for values that are truly runtime-dependent."

### Airflow built-in Variables 

You learned that Airflow has a set of built-in variables that contain information about the currently running DAG and its tasks, such as the logical date of the DAG run and task instance (for a list of such variables, check [here](https://airflow.apache.org/docs/apache-airflow/stable/templates-ref.html)). You learned that you can access these variables within a task function by passing the context dictionary as an argument to the function. You can also pass these variables directly to the PythonOperator using a syntax known as Jinja templating, which looks like this : “{{ds}}”. You use double curly brackets and inside the brackets you specify the variable you’d like to access. In this example, ds represents the logical date of the DAG run.

Let’s see an example: Assume that your `python_callable` is a function that expects the name of a file. For example, this function loads some data to an s3 bucket and requires that you pass the file name.  And let’s say you want to include the logical date in the `file_name`.

```python
def load_to_s3(file_name):
	#code that loads data
	print(file_name)
```

So you can specify this information in the PythonOperator as follows:

```python
task_load_s3 = PythonOperator(task_id="load_to_d3",
        python_callable=load_to_s3,
        op_kwargs={'file_name': "data/created{{ds}}/file.csv"})
```

The parameter `op_kwargs` allows you to specify the arguments that you need to pass to the function `load_to_s3`. Note how the logical date was included in the file name using templating (“`{{ds}}`”).

### Task groups

In the Airflow UI, you can group tasks using Task Groups to organize your DAGs and make them more readable. Inside the task group, you can define tasks and their dependencies using the bit-shift operators `<<` and `>>`. You can create a Task Group using the `with` statement, as shown in the following example.

```python
from airflow.utils.task_group import TaskGroup

with DAG(...):
	start = DummyOperator(...)
	with TaskGroup('task_group')as task_group:
		task_a = PythonOperator(...)
		task_b = PythonOperator(...)
		task_a >> task_b
	
	end = DummyOperator(...)
	start >> task_group >> end
```

## Other practices (Airflow is an orchestrator not an executor)

- Heavy processing should be assumed by execution frameworks (e.g. Spark) not Airflow
- For large datasets, don’t use XComs (push dataframes). Use intermediary data storage instead.
- Including code that is not part of your DAG or operator makes your DAG hard to maintain and read: consider keeping any extra code that is needed for your tasks in a separate file.
## Additional References _(if you’d like to learn more)_

- [Airflow best practices](https://airflow.apache.org/docs/apache-airflow/stable/best-practices.html#communication)
- [Other best practices](https://docs.astronomer.io/learn/dag-best-practices)
- [Functional-data-engineering-a-modern-paradigm-for-batch-data-processing](https://maximebeauchemin.medium.com/functional-data-engineering-a-modern-paradigm-for-batch-data-processing-2327ec32c42a) by Maxime Beauchemin