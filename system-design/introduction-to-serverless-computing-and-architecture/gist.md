Serverless is a cost-efficient way to host your APIs and it forms the crux of systems like Chatbots and Online Judge.

Serverless does not mean that your code will not run on the server; it means that you do not manage, maintain, access, or scale the server your code is running on.

The traditional way to host APIs is by spinning up a server with some RAM, and CPU. Say the resources make your server handle 1000 RPS, but you are getting 1000 RPS only 1% of the time which means for the other 99% you are overprovisioned.

So, what if there was an Infrastructure that

- scales up and down as per the traffic
- is billed per execution
- is self-managed maintained and fault-tolerant

These requirements gave rise to Serverless Computing.

# Real-world applications

## Chatbot

Say, we build a Slack chatbot that responds with the Holiday list when someone messages `holidays` . The traffic for this utility is going to be insignificant, and keeping a server running the whole time is a waste. This is best modeled on Serverless which is invoked on receiving a message.

## Online Judge

Every submission can be evaluated on a serverless function and results can be updated in a database. Serverless gives you isolation out of the box and keeps the cost to a bare minimum. It would also seamlessly handle the surge in submissions.

## Vending Machine

Upon purchase, the Vending machine would need to update the main database, and the APIs for that could be hosted on Serverless. Given the traffic is low and bursty, Serverless would help us keep the cost down.

## Scheduled DB Backups

Schedule daily DB backups on the Serverless function instead of running a separate crontab server just to trigger the backup.

## Batch and Stream Processing

Use serverless and invoke the function every time a message is pushed on the broker making the system reactive instead of poll-based.

# Advantages

 - No need to manage and scale the infra
 - The cost is 0 when you do not get any traffic
 - Scale is out of the box; so no capacity planning is needed

# Disadvantages

 - Takes time to serve the first request as the underlying infra might boot up
 - The execution has a max timeout, so your job should complete within the limit
 - Debugging is a challenge
 - You are locked in on the vendor you chose

# When NOT to use Serverless

 - Load, usage, and traffic pattern is consistent
 - Execution will go beyond the max timeout
 - You need multi-tenancy

# When to use Serverless

 - Quick build, prototype, and deploy the changes
 - Usecase is lightweight
 - Traffic is bursty