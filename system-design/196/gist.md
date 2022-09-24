Swiggy has automated its customer support with Chatbots; so what's their architecture? Let's find out today.

Chatbots are essentially a Decision Tree where nodes are the states the conversation could be in and the edges are conditional statements. Depending on which statement (edge) meets the criteria, the conversation moves forward in that direction.

At each step, Swiggy shows the customer the options which are the child nodes of the current node until all the information is gathered; and the flow stops upon reaching the terminal state.

## Key components and architecture

The decision tree is stored in a relational database. It can be generated using historical customer support data and can be updated by product and business teams.

The core chatbot service needs to access data from other services/databases like Payments, Orders, and Notifications. Accessing peripheral information will provide a rich experience to the users.

The most important part chatbot is to interact with the Fraud Detection system. Given that the entire flow is automated and needs no manual intervention, the chances of Fraud shoot up.

Fraud Detection System, in real-time, would see if the customer is trying to commit fraud. This system would interact with historical information about the customer, past refunds, image processing, and much more.

There may be a possibility that the customer still needs to talk to an executive hence the customer support executive needs to get all of this information, including fraud probability, in an easy-to-use dashboard.

Hence, a real-time pipeline would be needed to ingest and move data across all of these systems. Apache Spark is an excellent candidate for building this.

## Business Continuity Plan

If the Chatbot is down, then Swiggy switches to a simple chat interface that connects directly to an executive, continuing to service the end users.

## Key Metric

A metric that Swiggy chases is Bot Efficacy which is nothing but the percentage of requests handled by the bot vs executive. Swiggy wants to handle as many requests as possible through the bots as it would help them remain efficient at scale.