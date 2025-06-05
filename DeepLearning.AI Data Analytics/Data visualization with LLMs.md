## Step 1: Create copy of a database

You will be working with a truncated version of the Hotel Reservations dataset which only contains the first 50 reservations from 2018. You will create a copy of the dataset so you can test the answers the LLM gives you. 

1. Make a copy of the [spreadsheet with the dataset](https://docs.google.com/spreadsheets/d/1j8Y1R-Ek_arOqFf5NNFKDVzh10c77W-_6p0DZu5_P1o/copy?usp=sharing). You will use this copy to create some data visualizations.
2. Briefly review the features to remind yourself of the structure of the dataset.

## Step 2: Upload the data to the LLM

The LLM interface you are working with supports file uploads. We have already uploaded the file into the environment, but you still need to import it to your prompt. This is why you are given a reduced version of the dataset, you don’t actually need all of it for the LLM to learn the context of the problem. 

- Click on the Files button on the left of the text box:
    ![[files-button.png]]
- Select the C1M3_Hotel reservations_LLM dataset. 
- Write the following prompt:
    _Here is a the structure of a dataset of hotel bookings. These are the first 50 rows, so you can get a sense of the structure of the data. Explain the dataset to me so I know you understand it._

## Step 3: Start asking question!

You can now prompt the LLM about the dataset to help you create some visualizations.

### Here is a good process for prompting:

1. Paste in your prompt and submit it.
2. Evaluate the response. Was it accurate to the data? Was it helpful?
3. Ask a follow up question or revise your prompt.
    1. If the LLM appears to be wrong: “Are you sure about that? Explain your answer”, or point out where it is wrong. Sometimes it will give you solutions using features not implemented in your working tool (in this case, Google Sheets), be on the lookout for those!
    2. If the LLM didn’t answer your question. “I was actually asking [clearly stated request]. Does this change your answer?”

Try each of the prompts below, and feel free to create your own based on the lectures you watched. Try out the suggested steps in Google Sheets to see if they work, and practice correcting the model if it needs guidance based on what you're trying to accomplish.

| 👤**💬 Prompt 1**                                                                                           |
| ----------------------------------------------------------------------------------------------------------- |
| _Which type of charts would you recommend for visualizing some interesting possible patterns in this data?_ |

| **👤💬 Prompt 2**                                                                                                                                                                            |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| _My colleague is considering creating a scatterplot to analyze booking cancellation rates across different room types. Rate this approach on a scale of 1 to 10 and explain your reasoning._ |

|**👤💬 Prompt 3**|
|---|
|_Which charts would you recommend to help my non-technical stakeholders best understand the different factors affecting cancellation rates?_|

|**👤💬 Prompt 4**|
|---|
|_Help me create a visualization for the average number of special requests by booking status using Google Sheets. I want named axes and a title. Provide succinct instructions for creating this visualization._|
|**Follow up:** Test this solution in Google Sheets. Was it correct?|

|👤💬 Prompt 5|
|---|
|Help me create a stacked bar chart of Cancellation Rate by Market Segment with axes names and a title using Google Sheets. I want canceled reservations to show in orange and not canceled reservations in blue.|
|**Follow up:** Try this solution on Google Sheets. Does it work? If not, try iterating your question until you get it right.|