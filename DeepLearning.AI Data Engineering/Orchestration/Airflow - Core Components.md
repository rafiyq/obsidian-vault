In this lesson, we’ll explore the **core architecture of Airflow** and how its components work together to automate and manage your workflows.

When you create DAGs in Airflow, several components operate behind the scenes to ensure your workflows run smoothly. These components handle task dependencies, execution, and status updates, which are then reflected in the **Airflow user interface (UI)**.

The main components of Airflow include: a web server where the Airflow user interface runs, a scheduler, workers, a metadata database, and finally a DAG directory.

![[airflow_main_component_diagram.svg]]

When setting up your Airflow environment—whether through a direct installation or a managed service—all of these components will be included in your setup. As a user, your primary interactions will be with the **DAG directory** and the **user interface (UI)**. The other components operate seamlessly in the background.

![[airflow_user_interaction.svg]]

The **DAG directory** is a folder where you store the Python scripts that define your DAGs. This directory is connected to the web server hosting the Airflow UI, meaning any DAG you create and add to the directory will automatically appear in the UI. The UI allows you to **visualize**,  **monitor**, **trigger**, and **troubleshoot** behavior of your DAGs and their individual tasks.

![[airflow_DAG_server_component.svg]]

You don’t always need to manually trigger your DAGs from the UI. Instead, you can *trigger DAGs based on a schedule or with an events*, or rather you can do so with the help of the scheduler component of Airflow. 

The **scheduler** constantly monitors all DAGs and their corresponding tasks in the DAG directory. By default, it checks every minute to determine if any tasks should be triggered—either based on their schedule or by checking if their dependencies are complete.

Once the scheduler identifies a task ready to be triggered, it pushes the task to a **queue**. The **executor**, a component of the scheduler, then extracts tasks from the queue and assigns them to **workers**, which carry out the actual execution.

![[airflow_task_sceduler.svg]]

When the scheduler triggers a given task, its status changes from **scheduled** to **queued**. Once the workers begin executing the task, the status updates to **running**, and finally to either **success** or **failed**, depending on the outcome.

![[airflow_execution_status.svg|100]]

The **scheduler** and **workers** store the status of tasks and the state of DAGs in the **metadata database**. The **web server** then extracts those states and displays them in the **UI**.

![[airflow_store_state.svg]]

## Amazon Managed Workflows for Apache Airflow (MWAA)

If you’re using a managed service like **Amazon MWAA**, all of these core components are automatically provisioned and managed for you. 

![[amazon_mwaa.svg]]

In the architectural diagram, you’ll see how Amazon MWAA organizes the core components of Airflow on the cloud. For example:
- The **DAG directory** is stored in an **Amazon S3 bucket**.
- The **metadata database** uses **Amazon Aurora PostgreSQL**.
- Additional AWS networking components and services handle **security**, **logging**, and **monitoring**, ensuring a robust and scalable environment.


The other components are AWS networking components and additional AWS services that support securing your data as well as logging and monitoring your environment. 

In the lab exercises, you will:
1. Set up the Airflow environment
2. Define your DAGs as Python scripts
3. Upload your DAG scripts to the S3 bucket
4. Open the Airflow UI

## Conclusion 

Understanding how these components interact will help you troubleshoot issues effectively and make the most of Airflow’s capabilities. 

Next, we’ll explore the **[[Airflow - The Airflow UI|Airflow UI]]** and its key features in more detail!