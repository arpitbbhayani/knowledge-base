It is always exciting to create new microservices as it gives us so many things to look forward to- a fresh codebase, a new tech stack, or even maybe a clean CICD setup. But does this mean we should create as many microservices as possible?

Whenever we decide to create a new microservice, it is very important to understand its scope of it. If you create a new service for every utility then you are effectively creating a mesh of network calls that is prone to a cascading failure. If your scope is too big, it would lead to the classic problem of a monolithic codebase.

There are a couple of guiding principles that would help us with scoping of microservice.

# Loose Coupling

Services are loosely coupled if changes made in one service do not require a change in other. This is the core ideology behind microservices as well, but while designing a system we tend to forget it.

Say, we have an Orders service and a Logistics service. These services are loosely coupled when they do not share anything in common and are communicating with each other via API contracts.

To achieve loose coupling, make your microservices expose as little information as possible. The other service should just know how to consume the data and that is it. No internals, no extra details.

# High Cohesion

The principle of High Cohesion says that the related behavior should sit together as part of one service while the unrelated ones should be separate. This would encourage services to be operating independently.

If the Orders service also owns the customer data then when the changes are deployed in one might affect the other module. So the scope of testing before taking things to production increases.

If there is a very strong coupling between the services then it may also happen that the changes in one lead to deploy a few other services- all at the same time. Deploying multiple services at the same time is very risky; because one glitch and the almost entire product is down.

Hence it is not favorable for heterogeneous components to be part of the same service. Keep it crisp and short; and while designing try to keep services loosely coupled and split it to a level where the unrelated components are split up.