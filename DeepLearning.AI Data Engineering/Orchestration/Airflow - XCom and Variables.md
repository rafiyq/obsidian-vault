Let's dive deeper into Airflow’s advanced features and explore best practices for implementing orchestration. In this lesson, we’ll learn how to pass data between tasks using Airflow’s XCom feature and how to create global variables in the Airflow UI. 

In the first lab, you got some
experience building DAGs, interacting with the Airflow UI, and troubleshooting
issues in your DAG. Now you're ready to explore additional airflow
features and look at some best practices for implementing orchestration
with airflow. In this video, you'll learn
how to pass data from one task to another
using airflow XCom, and how to create global
variables in the airflow UI. Let's get started. Here's a DAG implemented in the previous lab. In the task get_random_book, you requested the data of a randomly chosen
book from a book API and then store that data in an S3 bucket to be used
in subsequent tasks. You essentially passed
data from one task to another using an
intermediate storage, in this case, the S3 bucket. This method is appropriate
when you want to pass large datasets
between tasks. But for small amounts of data, there's another method called
XCom that you can use. 

## What is XCom?

XCom (**cross-communication**), is a key airflow feature for sharing data among tasks. It’s designed to pass small amounts of data: metadata, dates, single value metrics, or simple computations
between tasks. Here’s how it works:

- **Storing Data**: In a task, you can store a value in an XCom variable using the `xcom_push` method. This pushes the data to Airflow’s metadata database.
- **Retrieving Data**: In another task, you can retrieve the value using the `xcom_pull` method.

In a given task, if there's a value that you'd like
to use in another task, you can sort in an
XCom variable by calling the xcom_push method. The XCom variable is then
pushed to a metadata database. Each XCom contains the
following information. A key, which is the name of the XCom variable,
the stored value, the timestamp at which
the variable was created, as well as a DAG ID and the task ID from which the
XCom variable originated. To extract the value stored in an XCom variable
in any given task, you can call the
method xcom_pull. Let's go over an example. The DAG you see here
consists of two tasks. The extract metric task
connects to an API, sends a request for
a certain data and then computes a metric
based on the return data. The second task prints the metric computed
by the first task. Since you need to pass some data between the first
and second task, you can use the
XCom feature here. The first task uses the
function extract_from_api. This is where you need
to call xcom_push. The second task uses the
function print_data. This is where you need
to call xcom_pull. Let's take a closer
look at each function. This is the code for the
extract_from_api function. Here I called the REST
API of a job site to get the latest 40
remote job postings for data engineering in the US. Then I computed the ratio of those jobs and asked for
a senior data engineer. Now, you want to pass this
value to the second task. You need to first store the obtained value
in an XCom variable by calling the method xcom_push. This method expects
two parameters, the key of the variable
and the computed value. XCom_push is a method associated
with a task instance. This means that you
need a task instance here on the left in order
to call the method. By task instance, I mean the object that represents
the currently running task. Airflow has a set of
built-in variables that contain information about the task that is
currently running, including the task instance. This information is
stored in a dictionary called airflow
context that you need to pass to the
extract_from_api function as an argument,
like you see here. To get the task instance object from a
context dictionary, you can use context
and in brackets, you'll see TI or TI
stands for task instance. Then you can call xcom_push. On the tasking so
the object you got. Then to access a computed ratio of the XCom variable
in the second task, you need to call xcom_pull
like this and pass in the key of the variable in the task ID where the XCom
variable was created. Similar to what you did in the
extract_from_api function. We also need a task instance
in order to call xcom_pull. Let's pass the
context dictionary, as an argument to the
print_data function, and then use context
and then brackets TI again to get
the task instance, and finally, call the method
xcom_pull on this object. When you run your DAG, you can check your XComs
in the Airflow UI by clicking on Admin and
then navigating to XComs. Here's the XCom
variable that we just created along with this
corresponding value. I want to offer you a word of
caution about using XComs. They are not designed to pass large datasets like
DataFrames between tasks as they degrade the performance of your DAGs
and the metadata database. If you need to share large
datasets between tasks, you should follow what you
did in the previous lab and use an intermediate
storage like S3. Now let's discuss
another airflow feature using the same DAG
as an example. If you examine the API
requests of the first task, you see that the value
of certain parameters, such as count and
geo are hard-coded, which means they are directly
included in the code. But what if you don't
want those values to be fixed because you may need to change them in future DAG runs, or maybe you want to experiment
with more than one value? You can update the
values in the code, but this approach might be error prone and not the
most efficient, especially if the values are repeated many times
in your code. Instead of including
hard-coded values within your DAG or
task definitions, you can create
global variables in the Airflow UI or create environmental variables in
your development environment and use these variables
inside your code. Let's create two variables
in the Airflow UI, one for the number of posts
and another for location. If you click on
the Admin tab and then select the
Variables option, you'll see your
list of variables. Prior to a new variable,
you can click on this plus sign and then specify the key and
value of the variable. For the locations variable, I specify the list of countries. I'm interested in gathering
job posts as a JSON objects. For the number of post variable, I'll assign it the value of 20. To use those variables
inside your code, you need to import
the variable module, and then inside your code, you use the
variable.get method to retrieve the total number of posts and the list of locations. Here you set the parameter deserialize_json=True
if you want this method to return
the JSON object as a dictionary
instead of a string. In the next lab, you'll practice creating variables
in the Airflow UI, as well as using airflow
built-in variables. You'll also use XCom variables to pass data between tasks. Before you go to the next lab, make sure you check out
the reading materials after this video that lists
some of the best practices for writing DAGs to
ensure that your code is efficient, readable,
and reproducible.