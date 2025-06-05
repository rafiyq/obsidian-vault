In [[Stakeholder Management & Gathering Requirements]], we conducted requirements gathering based on conversations with various stakeholders at an e-commerce company. These stakeholders included [[Follow-up Conversation with the Data Scientist|a data scientist]], [[Conversation with the CTO|the chief data officer]], [[Conversation with Marketing|a product marketing manager]], and [[Conversation with the Software Engineer|a software engineer]]. From these discussions, we learned from the chief data officer that the company’s goals are to *expand into new markets* and *increase retention* among existing customers. Together with these stakeholders, we established a data pipeline for a recommender system.

Now, we’re building on those conversations by speaking with a marketing analyst tasked with uncovering insights and identifying product sales trends.

---

> **Data Engineer**: *Hi, nice to meet you!*

> **Marketing Analyst**: *Nice to meet you too!*

> **Data Engineer**: *Hi, I'm the new data engineer. I'm looking forward to hearing more about what you're working on.*

> **Marketing Analyst**: *Absolutely! I’m thrilled to collaborate with you. My current focus is understanding how external factors might influence customer purchasing behavior. On the marketing team, we’ve been brainstorming potential signals and have a few ideas we’d like to explore further.*

> **Data Engineer**: *That sounds interesting. Can you tell me more?*

> **Marketing Analyst**: *Sure! We’re considering how emotions—like happiness, sadness, excitement, or relaxation—might impact online shopping behavior. While we can’t know exactly how our customers feel on any given day, we’re exploring ways to gather insights. Specifically, we’d like to analyze what kind of music people are listening to in various regions where we sell our products and compare that data with product sales.*

> [!tips]
> Learn what **actions** your stakeholder plan to take with the data

> **Data Engineer**: *I see. So you’re thinking of pulling public data from external sources to get information on the music people are listening to?*

> **Marketing Analyst**: *Exactly. I’ve been researching this, and it looks like Spotify offers a public API where we can access data on trending artists across different regions and people's listening trends over time. Does that sound like something you could help us with?*

> **Data Engineer**: *Definitely! I’ll take a closer look at the Spotify API. Once I understand the details, we can discuss exactly what data you’d like to pull and how you’d like it delivered.* 

> [!tips]
> A **follow-up conversation** may be required

> **Marketing Analyst**: *That sounds great. Let me know if there’s anything I can assist with in the meantime, and I look forward to continuing the conversation once we’ve the details sorted out.* 

---

This conversation with the marketing analyst highlights their data needs for a project focused on integrating public API data with product sales data. While analyzing regional music trends might not particularly a brilliant approach to marketing strategy, stakeholders often propose unconventional ideas when it comes to different kind of data they want to explore. 

The key takeaway here isn’t to debate the merit of the idea but to identify the system requirements needed to build it. In this case, more information is required to determine the best approach for building the entire data pipeline for the project. 

## Conclusion

For the moment, we’ll need to ingest data from a third-party API. While there are additional considerations—like how to store and serve the data to the analyst—we’ll focus for now on the ingestion process. Typically, ingesting data from an API involves a batch ingestion process, but the specifics will depend on what you aim to do with the data. 

Next, we’ll explore the trade-offs between two popular batch data processing paradigms: [[ETL vs. ELT|ETL (Extract, Transform, Load) vs. ELT (Extract, Load, Transform)]]. After that, we’ll dive into connecting to and ingesting data from a [[REST API]].