## Step 1: Create a copy of the dataset

1. Create a copy of [**the dataset file**](https://docs.google.com/spreadsheets/d/1dpsMTqKoosEuEXAeOHsyTFK2Rrz1ctVE/copy) using this link.
2. Inspect the observations and features to familiarize yourself with the dataset.

> [!Note]
> If you are using a different LLM, you will need to download this file to upload to the LLM for context.

## Step 2: Attach context to the LLM

The LLM interface you are working with supports file attachments. You will need to add the dataset to your prompt. Note that you don't actually need to use the entire dataset, since the LLM can learn the context of the problem just by using a few rows.

- Click on the Files button on the left of the prompt box:
    ![[files-button.png]]
- Select the **Order_Details_small.csv** file. 
- Write the following prompt:    

| 👤💬 Prompt 1                                                                                                                                                           |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _I am providing you with a dataset of E-commerce sales that I am working with to better understand sales patterns for my client. Explain the structure of the dataset._ |

## Step 3: Comparing with a known distribution

### Background

You are particularly interested in the behavior of the Amount feature. This can help predict your upcoming revenues and better understand your customers. You are aiming to get some help in sampling and simulation, as well as how to communicate your findings.

Here is a good process for prompting:

1. Paste in your prompt and submit it.
2. Evaluate the response. Was it accurate to the data? Was it helpful?
3. Ask a follow up question or revise your prompt.
    1. If the LLM appears to be wrong: “Are you sure about that? Explain your answer”, or point out where it is wrong. Sometimes it will give you solutions using features for a tool you’re not working with (such as Microsoft Excel rather than Google Sheets), be on the lookout for those!
    2. If the LLM didn’t answer your question. “I was actually asking [clearly stated request]. Does this change your answer?”

### Instructions

1. In your spreadsheet, create a histogram chart for Amount, so you get a rough idea of how the feature behaves.
2. Try the prompts below to better characterize the distribution and evaluate whether the power law distribution would be a reasonable model for Amount.

| 👤💬 Prompt 1                                                                                                                                                                   |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _I am considering modeling e-commerce sales amounts using a power law distribution. Please rate the reasonableness of this assumption from 1 to 10 and explain your reasoning._ |
| **Follow-up:** _What about a normal or uniform distribution?_                                                                                                                   |

| 👤💬 Prompt 2                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------- |
| _I created a histogram for the Amount column. What characteristics in the histogram might lead me to suspect a power law distribution?_ |

## Step 4: Sampling

You want to simulate random samples from the product categories. This could help you understand the potential distribution of inventory stock to plan for the upcoming months. You can ask the LLM to help you generate 5 new samples from the Category feature. 

1. Try Prompt 1 below to identify the frequency of categories.
2. Implement the solution in the spreadsheet.
3. Try Prompt 2 to get the step by step instructions for sampling,
4. Try the solutions in the spreadsheet. If something doesn’t work, iterate with the LLM until you get a working result. Depending on the problem, try with prompts like:
    -  “_There is an error in the formula. This is the message I am getting: \<copy error message>. Please help me fix it_”
    - _“This is too elaborate. Can you suggest a simpler method?”_
5. How does the provided solution compare to the one you saw in the lectures?    

| 👤💬 Prompt 1                                                                                                                                                                                                                     |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Help me identify the unique values in the column Category, as well the frequency of occurrence. I’m working in Google Sheets. Don’t try to calculate these values. Instead, provide formulas so I can calculate them on my own._ |

| 👤💬 Prompt 2                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Write step by step instructions for creating 5 new samples from the feature Category. The samples should be drawn from the distribution of the original data. For example, if Category A occurs 80% of the time and Category B occurs 20% of the time, your samples should follow that probability mass function._ |

## Step 5: Interpretation

1. Use the prompt below to get help from the LLM with summarizing and communicating your findings.

| 👤💬 Prompt 1                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _After analyzing my samples I found the following results: 90% of the sales are below $745, which is about 13% of the range of values. Can you help me summarize and communicate these findings?_ |