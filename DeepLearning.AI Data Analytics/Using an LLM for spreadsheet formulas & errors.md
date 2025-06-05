## Step 1: Create a copy of the data set

You will be working with a dataset that includes just the first 70 songs of the Spotify dataset you've been working with, since the size of the prompt is limited.

You will use a spreadsheet to test responses and formulas from the LLM.

1. [**Use this link to create a copy of the dataset**](https://docs.google.com/spreadsheets/d/1o5Py0NhQZUNc0F7GGBnZEPU-QrJTCrtk-Ho789oEYiU/copy)

## Step 2: Attach your data to your prompt

Attach the smaller dataset to your prompt by including the file in your chat. The purpose of the dataset is for the LLM to learn the context of the problem, not to directly perform calculations on all the data.

- Click on the Files button on the left of the text box:
	![[files-button.png]]
- Select the **Spotify_Top3000small.csv** file. 
- Write and send the following prompt to learn more about the data.    

| 👤💬 Prompt 1                           |
| --------------------------------------- |
| Describe the structure of this dataset. |

## Step 3: Central tendency of track_genre

Your goal is to calculate descriptive statistics for this dataset. You want the LLM to help you write your formulas and troubleshoot errors, but you will carry out the actual calculations separately.

The following steps include some suggestions to get you going, but feel free to create your own prompts based on the lectures you watched!

Here is a good process for prompting:

1. Paste in your prompt and submit it.
2. Evaluate the response. Was it accurate to the data? Was it helpful?
3. Ask a follow up question or revise your prompt.
    1. If the LLM appears to be wrong: “Are you sure about that? Explain your answer”, or point out where it is wrong. Sometimes it will give you solutions using features for a tool you’re not working with (such as Microsoft Excel rather than Google Sheets), be on the lookout for those!
    2. If the LLM didn’t answer your question. “I was actually asking [clearly stated request]. Does this change your answer?”

One idea you’re considering is finding the central tendency of track_genre, but it’s a categorical variable, so you’re not sure how that would work. Ask the LLM to suggest multiple approaches and explain its reasoning.

| 👤💬 Prompt 1                                                                                                                                                                                                                          |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _I would like to calculate the central tendency of track_genre, but since it’s a categorical variable, I’m not sure how. Give me 3 possible approaches, rate the effectiveness of each approach from 1-10 and explain your reasoning._ |

## Step 4: Troubleshooting

Your coworker is asking for you to help calculate the mean of the track durations for the 'hip-hop' genre. They tried this formula first: 

_**=AVERAGEIF(Data!S:S, ="hip-hop",Data!E:E)**_

However, this formula gave them an error. Let’s see if you can use the LLM can help fix it.

|👤💬 Prompt 1|
|---|
|_I'm trying to calculate the mean of track durations for the hip-hop genre. I entered the following formula, but I got a formula parse error, can you help me fix it? Here is my formula: =AVERAGEIF(Data!S:S, ="hip-hop",Data!E:E)_|

Let’s see if the LLM can expand on this error for a new use case. You now want the mean track duration for tracks in the 'hip-hop' genre that also have an acousticness of less than 0.25. You can use this prompt:

|👤💬 Prompt 2|
|---|
|_Please help me find a formula to get the mean of column duration_ms for tracks that have genre=hip-hop and acousticness < 0.25_|
|**Follow up:** Try creating your own prompt so that the acousticness threshold is the median of the feature, rather than a fixed value. You can use the previous one as a guide.|

## Step 5: Following up

You want to know which features have a positive skew. Ask the LLM to help you write a formula for that.

|👤💬 🚨 Prompt 1|
|---|
|_Can you help me write a formula that returns all the numerical columns that have positive skew? The dataset is loaded on sheet Data, and I want the formula on Sheet 1._|
|**Follow-up:** Did that work on the first try? If not use the following prompt below.|

| 👤💬 Prompt 2                                                                       |
| ----------------------------------------------------------------------------------- |
| _That is not correct. I got the following error: \<copy the error you are getting>_ |
