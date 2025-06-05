One of the main features you'll interact with when using Apache Airflow is the **User Interface (UI)**. The UI is where you can 

- Monitor the status of your DAGs (Directed Acyclic Graphs) and their individual tasks
- Gain insights into historical DAG runs
- Troubleshoot issues within your pipelines

Let’s explore some of the basic features of the Airflow UI.

## The DAG view

When you first open the UI, you’ll land on the **DAG View**. This page displays a list of all the DAGs you’ve created in your DAG directory. For each DAG, you’ll see basic metadata such as the **DAG ID**, **tags**, **owner**, and **schedule**. 

![[airflow_ui_DAG_view.webp]]

You can also view when the DAG was last run, its current status, and how many runs are queued, running, completed successfully, or failed. There's also a more granular view for each dag where you can check the status of all tasks. This includes information on how many tasks are queued, running, successfully executed or failed, skipped, up_for_retry, up_for_reschedule, etc.

![[airflow_ui_DAG_status.webp]]

### Interacting with DAGs

On the left side of the DAG View, you’ll find a toggle to **pause or unpause** a DAG. On the right, you can manually **trigger** a DAG or **delete** it from the view. Additionally, you can filter the DAGs displayed on this page by status or custom tags you assign them.

![[airflow_ui_DAG_control_filter.webp]]

You can click on the **DAG ID** to get more detailed information about the dag.

## The Grid view

This new view is called the **Grid View**, and it provides detailed insights into each DAG run and its corresponding task instances.

![[airflow_ui_DAG_grid_view.webp]]

On the left side of the Grid View, you’ll see a bar chart representing all previous runs of the DAG. For example, if the DAG has been run twice, you’ll see two bars. The height of each bar indicates the **duration** of the run, and the color represents its **status**—red for failed and green for successful.

For each run, you can also examine the outcome of individual task instances. A color legend at the top of the page helps you interpret the status of each task.

### Tabs in the Grid View

On the right side of the Grid View, you’ll find four tabs: **Details**, **Graph**, **Gantt**, and **Code**.

1. **Details Tab** provides detailed information about historical DAG runs, including the total number of runs, successful runs, failed runs, and metrics like minimum, mean, and maximum run durations. These metrics serve as indicators of your pipeline’s health. You can also select a specific DAG run (e.g., a failed one) to view its detailed information.
	![[airflow_ui_DAG_grid_details.webp]]
2. **Graph Tab**: Here, you’ll see a visualization of your DAG, which helps you explore its structure and verify the dependencies between tasks are correctly configured. To visualize the status of a specific DAG run, click on it in the bar chart. Each task will be color-coded based on its status for that run.
	![[airflow_ui_DAG_grid_graph.webp]]
	For example, if a task like “Extract from API” failed, you can click on it to show its logs tab and find all the error messages in this tab. After fixing the issue, you can use the Clear option to rerun the task. If it succeeds, the remaining tasks in the pipeline will proceed as expected.
	![[airflow_ui_DAG_grid_logs.webp]]
3. **Gantt Tab** displays the **queued duration** (in gray) and **run duration** for each task in a specific DAG run. It’s particularly useful for identifying bottlenecks in your pipeline.
	![[airflow_ui_DAG_grid_gantt.webp]]
4. **Code Tab**: This tab shows the code corresponding to the selected DAG. While you will not edit the code here, it’s a helpful reference to ensure the code in the UI matches the code in your DAG directory.
	![[airflow_ui_DAG_grid_code.webp]]

## Conclusion

The Airflow UI offers many features to interact with your DAGs effectively. In this overview, we’ve covered the essential UI features you’ll use most frequently. Next, we’ll walk through the steps to [[Airflow - Creating a DAG|build a simple DAG]].