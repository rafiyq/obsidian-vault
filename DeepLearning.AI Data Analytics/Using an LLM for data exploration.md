## Step 1: Provide data to the LLM

In the upcoming graded lab, you will work with a dataset of video game sales. In this practice lab, you will explore that dataset using an LLM!

While this LLM currently supports file attachments, it cannot write and run code. For that reason, you will use Approach 2: providing metadata or a few rows. Follow the instructions below.

1. Click the files button on the left side of the prompt input to open the file explorer. Select the video game sales file and add it to your prompt.

![[files-button.png]]

2. Now that you've given the LLM access to a few rows of the data, you can prompt it with some additional information about you, your task, and the LLM's role.

| 👤**💬 Prompt 1**                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _I am conducting some data analytics work for a company that creates video games with the goal of conducting market research to identify the most in demand video games. Your task is to help me explore a dataset I have identified to help with this market research. I am working with a dataset of cumulative video game sales based on a game’s year of release. You have access to the first rows of this dataset. You will help me better understand this dataset. Please summarize your task so I know you understand._ |

> [!Tip]
> Use “Shift + Enter” to add a new line to your prompt without submitting it.

## Step 2: Include the metadata

In addition to sharing a few rows of the dataset, you can also add metadata: data about the data.

Navigate to [this Kaggle page](https://www.kaggle.com/datasets/thedevastator/global-video-game-sales) and expand the “About this Dataset” section. Paste it into the chat interface and include the prompt below. You can include as much or as little information from the Kaggle site as you like in the prompt.

| 👤**💬 Prompt 1**                                                         |
| ------------------------------------------------------------------------- |
| _Here is some more information about this data set. Please summarize it._ |

## Step 3: Start asking questions!

You can now send more specific prompts about the dataset.

### Prompting process

1. Paste in your prompt and submit it.
2. Evaluate the response. Was it accurate to the data? Was it helpful?
3. Ask a follow up question or revise your prompt.
    1. If the LLM appears to be wrong: “Are you sure about that? Explain your answer”
    2. If the LLM didn’t answer your question. “I was actually asking [clearly stated request]. Does this change your answer?”

### Instructions

Try at least 3 of the prompts below, and feel free to create your own based on the lectures you watched!

| 👤**💬 Prompt 1**             |
| ----------------------------- |
| _How is this data generated?_ |

|👤**💬 Prompt 2**|
|---|
|_Summarize the mix of numeric and categorical features._|

|👤**💬 Prompt 3**|
|---|
|_What are some relationships you can infer between the features based on how they are defined?_|

|👤**💬 Prompt 4**|
|---|
|_What do you suspect is the general quality of this data and why?_|

|👤**💬 Prompt 5**|
|---|
|_What summary statistics should I calculate about this dataset in order to better understand it?_|

|👤**💬 Prompt 6**|
|---|
|_What data processing steps do you recommend from this list: categorical grouping, text processing, binning?_|

| 👤**💬 Prompt 7**                                                                                                                                                                                                 |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _Considering the goals of this project, if you were to collect more data, what information would be most valuable to add to this dataset? You can also suggest an additional dataset that would be more helpful._ |

## Step 4: Break the LLM

As you learned in earlier lectures, LLMs can hallucinate, so don't take every answer as fact. While an LLM is a good assistant for when you're first tackling a problem, you should be mindful of its strengths and weaknesses.

Below, you’ll find some prompts that some LLMs may not be able to answer well. See if the one you're using can handle them. Note that responses may differ each time. 

Ask the LLM each prompt and evaluate its answer.

|👤**💬** Prompt 1|
|---|
|_What is the sum of all the global sales for the first 10 games?_|
|**Correct answer: 160.67**|

|👤💬 Prompt 2|
|---|
|_How old was the president of Nintendo in 2023?_|
|**Correct answer:** 51|

|👤💬 Prompt 3|
|---|
|_How many years is there between the earliest and latest game published, considering only the first 10 games?_|
|**Correct answer:** 25|