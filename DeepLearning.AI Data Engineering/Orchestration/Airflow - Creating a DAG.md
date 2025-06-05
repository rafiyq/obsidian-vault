In this video, we’ll walk through the process of building a simple Directed Acyclic Graph (DAG) using core Apache Airflow concepts such as **DAG** and **Operator** classes. To illustrate this, we’ll use an example of an **ETL (Extract, Transform, Load)** process. The following diagram shows a DAG representation of this process, which consists of three tasks: **extract**, **transform**, and **load**. 

Rather than diving into the specific details of each task, we’ll focus on how to set up a DAG with this structure. Let’s get started!

## Setting Up the Environment

Let’s begin by creating an empty Python script and import some essential packages:
- The **DAG class** from Airflow.
- The **datetime module** to handle scheduling.

```python
from airflow import DA
from datetime import datetime
```

These packages will be used to create the DAG instance.

### Creating the DAG Instance

To create the DAG instance, you’ll use the **`with` statement**, also known as a **context manager**. This helps group and define all the tasks that belong to this DAG. Then, you’ll specify the parameters of the DAG:

```python
with DAG(
	dag_id = "example_dag",
	description = "ETL pipeline",
	tags = ["data_engineering_team"],
	schedule = "@daily",
	start_date = datetime(2024, 12, 1),
	catchup = false):
```


-  **`dag_id`**: The unique name used to identify the DAG in the Airflow UI.
- **`description`** (Optional): A description of the DAG, which will appear when you hover over the DAG name in the Airflow UI.
- **`tags`** (Optional): You can assign tags (e.g., `data_engineering_team`) to filter DAGs in the UI.
- **`schedule`**: This defines when the DAG will run. You can use:
	- **cron expression**: `0 8 * * *` for daily at 8 am.
	- **cron preset**: `@daily`, `@hourly`, or `@weekly`.
	- A **timedelta object**: `timedelta(days=3)` for every three days.
- **`start_date`**: This specifies the first date the DAG will execute.
- **`catchup`**: Boolean parameter. If set to `True`, the scheduler will kick off a DAG Run for any missed interval when the DAG was paused. (Default: `True`)

Next, let's define the tasks for the DAG. We need to use Airflow operators to define each task.

## Airflow Operator

- Operators are Python classes used to encapsulate the logic of the tasks or how data should be processed in your pipeline.
- Operators are provided by Airflow and you can import to your code.
- Each task is an instance of an Airflow Operators.

There are several operators that you can choose from. 

- `PythonOperator`: execute Python script that contains the logic of your task. 
- `BashOperator`: execute bash commands. 
- `EmptyOperator`: organize your DAGs, such as marking the start and end of the pipeline.
- `EmailOperator`: send a notification via email.
- `Sensors`: special type of Operator used to make your DAGs event-driven.

For this example, We'll use the **PythonOperator** to define each of the three tasks: **extract**, **transform**, and **load**.

### Step 1: Import the Operator

First, import the **PythonOperator** class.

```python
from airflow.operators.python import PythonOperator
```

### Step 2: The extraction step

Inside the context manager, define each task as an instance of the **PythonOperator**. Each task requires two parameters:
1. **`task_id`**: A unique name for the task (e.g., `extract`). This name will be used to reference the task in the Airflow UI.
2. **`python_callable`**: The Python function containing the task’s logic.

```python 
# ...
with DAG(//...):
	task1 = PythonOperator(task_id='extract', python_callable=extract_data)
	task2 = PythonOperator(task_id='transform', python_callable=transform_data)
	task3 = PythonOperator(task_id='load', python_callable=load_data)
```

For now, let’s assume the following functions exist:

- `extract_data()`
- `transform_data()`
- `load_data()`

We’ll define these functions later in the script.

### Step 3: Creating Task Functions

You can define the task functions either:

- Before the DAG definition.
- Next to the corresponding task within the DAG.
- In another file and import it into the code.

For simplicity, each function in this example will contain a **`print` statement**.

```python
def extract_data():
	#code for extracting data
	print("Done with the extracting task")

def transform_data():
	#code for transforming data
	print("Done with the transforming task")

def load_data():
	#code for loading data
	print("Done with the loading task")
```

### Defining Task Dependencies

Once the tasks are defined, you’ll specify the order of execution using the **bit shift operator (`>>`)**. For example:

```python
task1 >> task2 >> task3
```

This means:
- **Task 1** must complete before **Task 2** starts.
- **Task 2** must complete before **Task 3** starts.

Here, `task1`, `task2`, and `task3` are variables representing the task instances.

## Conclusion

```python
from airflow import DA
from datetime import datetime
from airflow.operators.python import PythonOperator

def extract_data():
	#code for extracting data
	print("Done with the extracting task")

def transform_data():
	#code for transforming data
	print("Done with the transforming task")

def load_data():
	#code for loading data
	print("Done with the loading task")

# context manager
with DAG(
	dag_id = "example_dag",
	description = "ETL pipeline",
	tags = ["data_engineering_team"],
	schedule = "@daily",
	start_date = datetime(2024, 12, 1),
	catchup = false):
		# define task here
		task1 = PythonOperator(task_id='extract', python_callable=extract_data)
		task2 = PythonOperator(task_id='transform', python_callable=transform_data)
		task3 = PythonOperator(task_id='load', python_callable=load_data)
		
		task1 >> task2 >> task3
```

That’s it! You’ve now learned how to build a simple DAG in Airflow. In the lab, you’ll have the opportunity to create another DAG on your own. Once completed, you’ll:
1. Upload your Python script to the **Airflow S3 toolkit** (which acts as the DAG directory).
2. Open the **Airflow UI** to check and monitor your DAG.

Next, we’ll explore additional Airflow concepts like **XComs** and **Variables**.