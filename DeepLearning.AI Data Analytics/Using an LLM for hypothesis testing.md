## Step 1: Copy the dataset

1. Create a copy of [**the dataset file**](https://docs.google.com/spreadsheets/d/1TmskbkMzVO3IvRsUjKMhbshfn620zfBKZCJMYyQhgq0/copy) using this link.
2. Inspect the observations and features to familiarize yourself with the dataset.

> [!Note]
> If you are using a different LLM, you will need to download this file to upload to the LLM for context.

## Step 2: Upload your data to the LLM

The LLM interface you are working with supports file uploads. You will need to add the dataset to your prompt. Note that you don't actually need to use the entire dataset, since the LLM can learn the context of the problem just by using a few rows.

- Click on the Files button on the left of the text box:
    ![[files-button.png]]
- Select the **Fitbit_sleepdata.csv file** file. 
- Write the following prompt: 

| 👤💬 Prompt 1                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _I am providing you with a dataset with records of sleep parameters I am working with to help my friend understand whether they are experiencing stress while they sleep. Explain the dataset to me so I know you understand it._ |

## Step 3: Formulating Hypotheses

You can now work with the LLM to help you formulate hypotheses based on your business question.

Here is a good process for prompting:

1. Paste in your prompt and submit it.
2. Evaluate the response. Was it accurate to the data? Was it helpful?
3. Ask a follow up question or revise your prompt.
    1. If the LLM appears to be wrong: “Are you sure about that? Explain your answer”, or point out where it is wrong. Sometimes it will give you solutions using features for a tool you’re not working with (such as Microsoft Excel rather than Google Sheets), be on the lookout for those!
    2. If the LLM didn’t answer your question. “I was actually asking \[clearly stated request]. Does this change your answer?”

You are wondering if average sleep quality depends on the number of hours you sleep. Ask the LLM to create a good set of hypotheses for this task.

|👤💬 Prompt 1|
|---|
|_I want to know if the average sleep score is different for nights with less than 7.5 hours of sleep compared with nights with more than 7.5 hours of sleep. I plan to conduct a two sample hypothesis test for means. Help me formulate appropriate null and alternative hypotheses. Write your answer in correct statistical notation._|
|**Follow-up:** _Is that alternative hypothesis for a one tailed or two tailed test?_|

|👤💬 Prompt 2|
|---|
|_I have spoken with my client and reformulated my business question. I want to know if the average sleep score is greater for nights with 7.5 hours of sleep or more compared with nights with less than 7.5 hours of sleep. Can you reformulate the hypotheses accordingly?_|
|**Follow up**: _Is a right-tailed or a left-tailed test appropriate here?_|

## Step 4: Steps for testing

1. Try Prompt 1 to get step by step instructions
2. If something doesn’t work, iterate with the LLM until you get a working result. Depending on the problem, try prompts like:
    -  _There is an error in the formula. This is the message I am getting: \<copy error message>. Please help me fix it_
    - _The function \<function name> does not exist in Google Sheets. Please help me fix that._ 
    - _This is too elaborate. Can you suggest a simpler method?_
3. How does this solution compare with the one you learned in the demo?

|👤💬 Prompt 1|
|---|
|_Write a single formula to perform a two-sample unequal variance t-test in Google Sheets for this set of hypotheses. My sleep score column is Column B, and my Hours of sleep column is Column C. Double check your parameters to make sure they are correct for the revised hypotheses above. Only provide me with the formula; do not include any other information or commentary._|

## Step 5: Interpreting results

Now that you have performed the hypothesis test, use the LLM to help you communicate your results.

| 👤💬 Prompt 1                                                                                                                                                                                                                                                                                                                              |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| _The result of the hypothesis test is a p-value of 0.0027. Write a 100 word script for me to share with my client to explain the results of this test to them. Use appropriate statistical language while avoiding jargon. Make sure not to overstate your conclusions, and don't overwhelm with information. Keep it short and succinct._ |