Say we are building an e-commerce website and upon every purchase made we need to send a confirmation email to the user, notify the seller to keep the shipment ready and assign a logistic delivery partner to deliver the package to the user. So, how do we implement this?

Two high-level architecture patterns help us achieve this

- Orchestration
- Choreography

## Orchestration

Orchestration is the simplest way to model workflows. The core idea of the Orchestration pattern is to keep the decision logic centralized and have a single brain in the system.

In our example, the Orders service can be that brain, and when the order is placed the order service talks to Notification, Seller, and Logistics services and get the necessary things done. The communication between them is synchronous and the Orders service acts as the coordinator.

The workflow as part of our example is a one-level simple workflow but in the real world, these workflows could become extremely complex and the Orders service would be needing to handle the coordination.

## Choreography

The core idea of the Choreography pattern is to keep the decision logic distributed and let each service decide when needs to be done upon an event. It thus laid the foundation for Event Driven Architecture.

In our example, when the order is placed the Orders service will simply emit an event to which all the involved services subscribe. Upon receiving an event, the services will react accordingly and do what they are supposed to.

All the 4 involved services are thus totally decoupled and independent; making this a truly distributed and decentralized architecture

## Orchestration vs Choreography

Most model systems are inclined towards Choreography as it gives some amazing benefits

- loose coupling: services involved are decoupled
- extensibility: extending the functionality is simple and natural
- flexibility: search service owns its own decision on the next steps
- robustness: if one service is down, it does not affect others

Observability might become a challenge here; given that we need to track each service, action it took, and completion of it.

Although people prefer choreography, it does not make Orchestration bad. Orchestration has its advantages and can be used in modeling services that are involved transactionally.

For example, sending OTP during login is best modeled synchronous instead of doing it async. Another example is when we want to render recommended items the Recommendation service talks to relevant services to enrich the information before sending it to the user.