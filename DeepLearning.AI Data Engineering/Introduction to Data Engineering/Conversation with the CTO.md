The following is a conversation between a newly hired data engineer and the Chief Technology Officer (CTO) at an e-commerce company about the overall goals of the business and technology initiatives.

**Data Engineer:** 
Hi, thanks for taking the time to chat with me today. I’m really excited to join the team, and I’d love to get a better understanding of the company’s goals and how technology is driving them forward.  

**CTO:**
Great to have you on board! I always make it a point to connect with new hires in the tech team to ensure we’re all aligned on our objectives. Think of this as my way of “walking the shop floor” to stay in touch with what’s happening across the company.

Your role as a data engineer is going to be critical to our success in the coming year and beyond. Let me walk you through how your work ties into our broader initiatives.

**Data Engineer:**
Sounds good—I’m all ears!

**CTO:**
So far, our company has been successful as an e-commerce platform, but we’ve primarily focused on a limited number of product lines. Our early entry into the market gave us a first-mover advantage, and our marketing efforts have been strong. However, the landscape is changing. Smaller brands are emerging and capturing market share, which is a challenge for us.

On the technology side, we’re facing another major issue. While we’re an e-commerce platform now, we inherited some legacy systems that predate even the .com era. This outdated code poses a risk of outages, which could be costly and damaging to our brand reputation. You’ve probably seen news about similar outages at other companies—we want to avoid that at all costs.

Our big initiatives for the future include expanding market share, introducing new product offerings, and scaling internationally. To support this growth, we need to refactor our software. This means eliminating the legacy code that puts us at risk and building systems that are more scalable in the process.

From your perspective as a data engineer, how do you see this affecting your work?

**Data Engineer:**
It could have a significant impact. While working with legacy systems might not always be fun, I’m excited about the opportunity to help modernize the system.

**CTO:**
That’s exactly the attitude I’m looking for! One of the challenges I’ve seen in my experience as a CTO is what I call the “software-data divide.” Often, software teams write code kind of in a vacuum, and data engineers are left to deal with whatever output is generated. This has been a problem for us because the legacy code produces schemas that are difficult to use for analytics.

As part of the refactoring process, I’d like you to assist and consulting with the software teams to ensure the data they generate is analytics-ready with minimal post-processing. We won’t eliminate ETL entirely, but if we can produce cleaner, well-structured data from the start, it will make analytics much more efficient.

**Data Engineer:**
What tools can I expect to be working with?

**CTO:**
That's a good question. As part of our refactoring efforts, we’re shifting from a batch-based approach to a streaming-based architecture. On AWS, we’re exploring tools like Kinesis—Amazon’s native streaming service—and potentially Kafka for certain pipelines as we scale. Do you have experience with these? 

**Data Engineer:**
Not yet, but I’ve taken a data engineering course where I worked with Kinesis and Kafka in labs. I’m excited to apply that knowledge to real-world scenarios.  

**CTO:**
That's great. At this stage, you're going to work as a consultant with the software teams to understand the data they’re producing and helping them improve its quality. At the same time, you can spin up proof-of-concept projects using Kinesis and Kafka. Experiment with their scalability and build a strong foundation in these tools—they’ll be key to your responsibilities as we expand our streaming capabilities.

You’ll be working under the direction of the Head of Data, but we expect you to really take the skills and expand those to be strong in this area.

**Data Engineer:**
Got it. I know AI is a hot topic right now—does the company have any goals with respect to machine learning or AI?

**CTO:**
Absolutely. One of our major goals within our technology initiatives is improving customer retention. The software refactoring I mentioned will help by ensuring a more responsive website and minimizing downtime, which directly impacts customer satisfaction.

We’re also developing a recommendation engine. As part of the data engineering team, you’ll be building pipelines to support this system. This will involve analyzing product taxonomy data, customer behavior like clickstream and order history, and collaborating with data scientists to create pipelines that feed into the recommendation engine.

**Data Engineer:**
That sounds great. I’m excited to get started and can’t wait to connect again as we move forward.  

**CTO:**
Well, thanks. It's really great to have you on board.