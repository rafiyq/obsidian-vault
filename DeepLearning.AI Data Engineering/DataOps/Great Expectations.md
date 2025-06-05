When working with Great Expectations, your workflow typically involves three key steps:

1. **Specifying the data** you want to test.
2. **Define your expectations** (or tests) to perform on the data.  
3. **Validate your data against the expectations**.

To implement this workflow, you’ll interact with the core components of Great Expectations: **Data Context**, **Data Sources**, **Expectations**, and **Checkpoints**. These components help you access, store, and manage the objects and processes required for your workflow.  

## Step 1: Instantiate a Data Context Object 

Your workflow begins by creating a **Data Context** object. This serves as *the entry point to the Great Expectations API*, providing classes and methods that allow you to connect data sources, create expectations, and validate your data. The Data Context also allows you to configure and access properties, objects, and metadata for your Great Expectations project.

## Step 2: Declare the Data Source

Next, you declare a **Data Source** object, which tells Great Expectations where to retrieve the data for validation. Data sources can include SQL databases, local file systems, S3 buckets, or Pandas DataFrames.

### Declare the data assets

Once connected to the data source, you specify the portion of the data to focus on by declaring **Data Assets**. A data asset is a *collection of records within a data source*, such as a table in SQL database, file in a file system, join query asset, or collection of files matching a pattern.  

You can further partition your data asset into **batches**. For example, if your asset represents yearly sales records, you could partition the data into monthly batches (by date) or by store IDs (by column values). Alternatively, you can work with the entire dataset as a single batch.

### Create a `batch_request`

To retrieve one or multiple batches, you create a `batch_request` object. It's the primary way to retrieve data from a data asset and is required for subsequent steps of Great Expectations components.  
## Step 3: Define Expectations  

An **Expectation** is a statement that you can use to verify if your data meets a certain condition. For example, you can define an expectation to check if
a column does not contain null values. You can create custom expectations or use prebuilt ones from the **Expectation Gallery**, such as:

- `expect_column_min_to_be_between`  
- `expect_column_values_to_be_unique`  
- `expect_column_values_to_be_null`  

### Create an **expectation suite**

You can define multiple expectations into an **Expectation Suite** object, which serves as a collection of tests for your data asset. 

To validate your data, you create a **Validator** object, which expect a `batch_request` and its corresponding expectation suite. You can manually validate data by interacting directly with the validator or automating the validation process using a **Checkpoint** object.

## Create a Checkpoints

A checkpoint automatically combines a `batch_request` and an **expectation suite**, passing them to a validator to generate *validation results*. This simplifies the validation process, especially for recurring tasks. 

Throughout this process, Great Expectations generates metadata about your project, which is stored in backend **stores**. The most common stores include:  
- **Expectation Store**: Stores your expectation suites.  
- **Validation Store**: Stores information about the objects generated when you validate data against the expectation suite (validation results).  
- **Checkpoint Store**: Stores checkpoint configurations.  
- **Data docs**: Stores reports on expectations, checkpoints, and validation results.  

You can access and manage these stores and their settings through the Data Context object.  

## Conclusion

Here are the steps of a typical Great Expectations workflow:

![[great_expectation_workflow.svg]]

Next, we'll use Great Expectations to apply data quality tests.