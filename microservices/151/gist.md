Say, we have 3 microservices - Order, Payments, and Logistics - and to get the order details we need data from all of them, merge it, and then respond to the client. A common pattern to achieve this is API Composition.

## API Composition

It is a high-level pattern to query microservices. It puts a composer right in the middle abstracting out the microservices.

With the composer sitting in between, the request from the client first hits the composer, and the composer then talks to the relevant services to get the response. It then merges the responses before sending them to the client.

## Implementing API Composition

Instead of building it from scratch, we can use tools that specialize in achieving this - ex: API Gateways like KrakenD, Kong, and AWS API Gateway.

## Improving user's experience using composer

An API Composer not only helps in making the backend simpler, but it also helps in gaining a good UX.

If we do not have an API composer, the client (browser/app) would have to make multiple API calls to microservices to get the information and render the interface. The multiple calls would require multiple round trips of the data increasing the latency and will also eat up the user's data.

By having an API composer sitting in between the client would only need to make one API call and the fan-out happening at composer will be within the infra. This would reduce the latency for clients and improve the UX.

## Branch Composition

For a complex usecase, it is quite possible that a downstream service may use another composer to reach out to another set of services to get things done. A dependency like this would create a multi-level API composition also called Branch composition.

This would create a hierarchical dependency between services solved through multiple API composers and it is a common pattern observed in complex e-commerce platforms.

## Advantages of using API Composition

- Simple to implement
- Client has a single point to interact
- Hides the implementation complexities
- Security and Limiting applied only to the composer
- Can cover the "bad" design decisions with a shiny new interface
- Hides legacy system allowing us to gradually move out of it

## Disadvantages of using API Composition

- If the dataset we fetch from microservices is large, it would make the composer in-efficient
- Overall availability is challenged as the number of services increase
- Having a transactional data consistency is difficult
- Composer needs to be managed and maintained
- Composer may become a bottleneck at scale