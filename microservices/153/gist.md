Everyone's talking about Microservices, but what exactly are they? Are they just a set of functions hosted over a network or something more?

Microservices in simple terms are like the regular functions from our programming language but just a more extensive set of responsibilities and served via a network.

So, you may have a microservice that handles everything related to Payments, a service that handles Notifications, and a service that deals with analytics. We see each service having focussed responsibility.

Microservices are no silver bullet, and they would not magically solve all the problems you have. It has its own fair share of drawbacks.

## Monolith

Almost all products start monolith where every feature is put into a single codebase which is deployed as one artifact across all the servers. For example, the code handling payments, notifications, and analytics are all part of the same codebase deployed within the same binary.

Monoliths are always simple to build, develop, test, and scale. Given their simplicity, they are the go-to option for anyone starting up. With a lean team working on monolith would ensure very quick feature delivery.

### Disadvantages of Monolith

- monolith is tightly coupled
- the deployment artifact - binary/JAR is bulky
- the tech stack is homogeneous
- bug in one module affects other modules
- scaling one module requires scaling everything
- large monolithic codebase is intimidating and it slows down delivery

### Monolith to Microservices

Migrating from monolith to microservices is a slow process and to start you would club a related set of functions and fork out a service out of it. The process would be repeated for other sets of functions, eventually breaking the entire monolith.

## Characteristics of Microservices

- microservices are autonomous
- microservices are focused and specialized
- microservices are built around a business usecase/need

## Advantages of Microservices

- agility: small independent teams can move much faster
- scaling: you can precisely scale one service as per the load
- freedom: you can pick the best-suited tech stack for the service
- given the scope is focused, a microservice is simple to understand
- microservices can be reused across the platform
- if a service goes down, it is easy to isolate it using a circuit breaker

## Anti-patterns

- do not start with microservices; start with a monolith
- do not make services too small; they should a larger responsibility
- don't reinvent the wheel, use existing tooling as much as possible