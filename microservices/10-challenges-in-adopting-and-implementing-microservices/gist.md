We always hear great things about Microservices. But today let's talk about the top 10 challenges that come with adopting Microservices.

## Managing Microservices

As the number of microservices increases, managing them becomes tough. If there is no plan or accountability then we might end up with a lot of tiny microservices or with a huge macro-service.

## Extensive Monitoring and Logging

Monitoring what happens across the entire infra is critical. Along with this, we would also need an ability to trace end user request path spanning services - also called Distributed Tracing.

## Service Discovery

It does not take much time for our services to grow beyond 100 and at that scale, discovering a service becomes a pain requiring us to put Service Discovery.

3 ways to do it are

- a central service registry
- load balancer-based discovery
- pure service mesh implementation

## Authentication and Authorization

Inter-service communication should be secure to ensure that a service does not abuse others; hence we need to put auth in place that allows authorized services to talk to each other.

## Config Management

Every microservice has a set of configs, like DB passwords, and API Keys. Committing them to the repository is an unacceptable practice, and we would not want every service to have its own config server.

Hence we need to have about a central config management system that is fault tolerant, robust, and scales well.

## No going back

It is extremely difficult to move back to monolith after the teams have tasted microservices. A few reasons would be

- services are written in various languages
- teams used to being autonomous
- teams have adopted new tools and processes

## Fault Tolerance

Outages are inevitable and as engineers, we always try to minimize them. A way to achieve this is to keep services loosely coupled that keep outages isolated ensuring no cascading failures.

## Internal and External Testing

End-to-end testing becomes complex as it is hard to spin up environments with all services running fine.

## Design with Failures in mind

Robust microservices require a counter-intuitive approach, and we need to assume everything would collapse after every line of code. Then we amend the code and architecture to handle it and re-iterate.

## Dependency Management is a nightmare

Managing dependencies across services is tough and it leads to a slowdown. The 3 kinds of dependency to be careful about

- sync dependency on other services
- services sharing a common library
- service depending on data coming from other services