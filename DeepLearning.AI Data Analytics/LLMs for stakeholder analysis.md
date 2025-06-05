## Step 1: Review the emails

1. Make a copy of the 🔗[**stakeholder emails linked in this document**](https://docs.google.com/document/d/1ZhDYJ6wE9aCwEo232eOdS0WiZsaUDRyaMGMTUaaMk3U/copy).
2. Skim the two emails so you understand their contents. The LLM won’t be useful to you if you aren’t sure if its responses are accurate

Once you’ve reviewed the emails, move on to the next step.

## Step 2: Compare the emails

Since Coursera’s LLM interface does not currently support document uploads, you will copy and paste the emails into the prompt. There is not a significant difference in responses between these two methods, as long as you’re using the same model; they effectively accomplish the same thing. Recall from the lectures that uploading a file essentially incorporates that file into your prompt, which is very similar to pasting it in.

1. Copy and paste this prompt in, but **do not send it yet**. This prompt explains some context about the business problem, the current situation, and the task the LLM should attempt. This prompt may seem long, but it follows the principle of being detailed & specific.

|👤**💬 Prompt 1**|
|---|
|_I’m currently working at a tech company whose flagship product is an app that allows users to track their hiking and biking trips. I’m looking into some analysis of a dataset of all hiking and biking trips users have taken in the past 5 years._<br><br>_Two stakeholders, the Engineering Lead and the Vice President of Sales, have sent me emails expressing their thoughts on the app's future direction. My goal is to synthesize their input and develop a proposed approach for how your analysis may contribute to business impact. Based on what you can read in these emails, you recognize that these two stakeholders have different goals._ <br><br>_Given the two emails from stakeholders below about their ideas for the business, identify the main business objectives each stakeholder is prioritizing. Highlight the common ground between their perspectives._|

2. Press shift + enter twice to start a new section of your prompt and paste in the two emails together from the document you copied earlier. Then hit enter to submit the prompt.
3. Read the LLM’s response. How good is it? How does it compare to the response you saw in the video?

Once you’ve evaluated the LLM’s response, move on to the next step.

## Step 3: Ask more about the emails

1. In the same chat, try the follow-up prompts below, the first of which you saw in the demo:

|👤💬 Prompt 1|
|---|
|Generate a single list of business decisions that need to be made based on the stakeholders’ objectives, prioritizing decisions that the two would likely agree on.|

|👤💬 Prompt 2|
|---|
|Generate 3 followup questions I can ask each stakeholder to better understand the types of analyses that would help them meet their business goals. My goal is to choose an analysis and inform business decisions using those insights, so design questions that help me get closer to this goal.|

2. Review the LLM’s responses. How good are they? Is there anything incorrect?
3. Try one of your own prompts! Consider ones about:
	- Stakeholder needs
	- The domain knowledge that each stakeholder might have
	- Reasons each stakeholder might not want to use your analysis
4. (Optional) Start a new conversation and try the first prompt again (the long one with the emails). What do you notice is different between the LLM's responses? Sometimes you can gain new insights just by starting fresh.

Great work! Move on to the next step.

## Step 4: Review the meetings notes

The stakeholders have decided to move forward with improving the user experience of the app as their next step. You have some meeting notes where they discuss their concerns, and you’d like to synthesize those concerns using a Rumsfeld matrix.

1. Make a copy of the 🔗[**meeting notes linked in this document**](https://docs.google.com/document/d/1blJNeUahG9D41xgEvBLN3fT0P7uEIz2J4Nqv_4aAbRE/copy). 
2. Skim the meeting notes. Make sure you understand their general contents before moving on.

Once you’ve reviewed the document, move on to the next instruction.

## Step 5: Synthesize the meetings notes

You can now send specific prompts about the meeting notes.

1. In a new chat, copy and paste in the meeting notes **without submitting** yet.
2. Press shift + enter twice then try the prompts below, the first of which you saw in the video. Press enter for each prompt.

|👤**💬 Prompt 1**|
|---|
|_Create a Rumsfeld matrix for our app’s initiative to improve the user experience using this document. Summarize and synthesize what was said in the meeting; don’t just repeat it. I want to better understand the knowns and unknowns surrounding this business problem so that, as a data analyst, I can perform the right analyses with the right data. I currently have access to a dataset of all hiking and biking trips users have taken in the past 5 years._|

|👤**💬 Prompt 2**|
|---|
|_Based on the data I have access to, what three analyses do you recommend performing first? For each analysis, explain how it relates to each stakeholder’s stated goals._|

3. Review the LLM’s responses. How good are they? Is there anything incorrect?
4. Try one of your own prompts! Consider ones about:
	-  The data that needs to be collected
	- A plan to check in with each stakeholder
	- Places where stakeholders may disagree

Great work! Move on to the next step.

## Step 6: Break the LLM

As you learned in earlier lectures, LLMs can make mistakes, so you should avoid assuming that every answer is correct. While an LLM is a good assistant for when you're first tackling a problem, you should be mindful of its strengths and weaknesses.

Below, you’ll find some prompts that this LLM may not be able to answer well. Note that responses may differ each time. 

Ask the LLM each prompt and evaluate its answer:

|👤**💬 Prompt 1**|
|---|
|_How many times is Kyra mentioned in these meeting notes?_|
|**Correct answer:** 7|

|👤**💬 Prompt 2**|
|---|
|_Based on the meeting notes, explain why Sanjana suggested not to segment by acquisition channel._|
|**Note:** Sanjana actually made the suggestion to segment by acquisition channel.|

|👤**💬 Prompt 3**|
|---|
|_List some of our competitor's stock prices right now._|
|**Note:** The LLM won’t be able to provide real-time stock data (though it can suggest competitors!)|

Great work finishing this lab! You’re almost done with this module. Move on to the module assessment and lab!