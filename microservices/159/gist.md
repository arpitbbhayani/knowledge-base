Running Microservices in isolation does not make any sense; it is natural for them to work together and solve a bigger problem. This would require each microservice to expose a well-defined API interface simplifying others to talk to it.

The following are the best practices that we should follow that would make interfacing and integration easy.

## Forward and Backward Compatability

While rolling out any changes in a microservice, we need to ensure they are both forward and backward compatible. If not, it would break the consumers or interfacing microservices.

Three key places where we need to be extra careful are

- while changing the database schema
- while changing the API response body
- while changing the message format in async communication

We can ensure forward and backward compatibility if we

- never abruptly delete any column/attribute
- never abruptly change the type of the column/attribute

We should always roll out breaking changes in phases ensuring the dependent services remain unaffected.

## Make APIs tech-agnostic

Tech evolves quickly in the world of software engineering, and hence we would always feel like using the new shiny thing available. While having that urge, we should always ensure we are not picking the technology that would induce tight coupling.

For example, we should not pick a framework that would require the interfacing services to be written in a particular language or require them to use a specific tech stack. This would take away autonomity from the interfacing services as we are dictating which stack to use.

## Dead simple consumption

Microservices are built to interact with other services and get things done. So, the core focus should be to make things super simple for anyone to integrate.

It does not matter how good your LLD is if the API interface is hard to integrate. Be consumer-centric while desinging the interface of a microservice and ensure you have

- simple API
- simple data format
- use common protocols

## Hide internal implementation details

Never let other microservice learn about the internal implementation detail of your service. If they interact using internal details this would create a tight coupling between the two services.

Internal details could be

- broker for internal communication
- building dependency on transitive dependencies
- allowing directly connecting to the private database

It is always safe to hide the internal implementation details and expose a strict interface to interact with the service. The interface could be REST, gRPC, or anything that your org uses.