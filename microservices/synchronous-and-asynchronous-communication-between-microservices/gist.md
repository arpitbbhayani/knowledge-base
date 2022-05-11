Say, we are building a Social Network and anytime someone reacts to your post, you need to be notified. So, how should the Reaction service talk to the Notification service to send out a notification?

The communication would be much simpler and reliable, just a function call if it was a monolith; but things become tricky as we go distributed.

Microservices need to talk to each other to exchange information and get things done; and there are two categories of communication patterns - Synchronous and Asynchronous.

# Synchronous Communication

Communication is synchronous when one service sends a request to another service and waits for the response before proceeding further.

The most common implementation of Sync communication is over HTTP using protocols like REST, GraphQL, and gRPC.

## Advantages of Synchronous Communication

- It is simple and intuitive
- Communication happens in realtime

## Disadvantages of Synchronous Communication

- Caller is blocked until the response is received
- Servers need to be pro-actively provisioned for peaks
- There is a risk of cascading failures
- The participating services are strongly coupled

## When to use Synchronous Communication

- When you cannot proceed without a response from the other service
- When you want real-time responses
- When it takes less time to compute and respond

# Asynchronous Communication

The communication is asynchronous when the one service sends a request to another service and does NOT wait for the response; instead, it continues with its own execution.

Async communication is most commonly implemented using a message broker like RabbitMQ, SQS, Kafka, Kinesis, etc.

## Advantages of Asynchronous Communication

- Services do not need to wait for the response and can move on
- Services can handle surges and spikes better
- Servers do not need to be proactively provisioned
- No extra network hop due to Load Balancer
- No request drop due to target service being overwhelmed
- Better control over failures and retires is possible
- Services are truly decoupled

## Disadvantages of Asynchronous Communication

- Eventual consistency
- Broker could become a SPoF
- It is harder to track the flow of the message between services

## When to use Asynchronous Communication

- When delay in processing is okay
- When the job at hand is long-running and takes time to execute
- When multiple services need to react to the same event
- When it is okay for the processing to fail and you are allowed to retry