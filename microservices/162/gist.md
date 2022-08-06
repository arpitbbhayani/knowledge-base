Say, we are launching an e-commerce website that people can use from their desktop and place orders. We want to render the product details that include - name, description, sellers, variants, reviews, and faqs. The site did well and now we decide to launch a mobile app.

Given that the mobile has limited real estate, it is very hard to render the same information that we do on the Web. Hence, we choose not to render Reviews and FAQs. Thus even if we receive the reviews and faqs in the response, while rendering we choose not to render them.

This is a waste of user bandwidth, data, and processing power. Ideally, we should not be sending unnecessary fields from the backend. So, how do we implement this?

## Backend for Frontend

BFF is a layer that sits between the clients and the backend. Every type of client has a dedicated BFF; for exampDesktop Web has its own BFF while Mobile has its own.

Depending on the request, the BFF then talks to the backend, grabs the data, filters out the unnecessary fields, and responds. It can also optionally transform the data in a client-specific format.

This way, we keep the backend simple and apply all presentation-level hacks and tweaks on BFF.

## BFF and Microservices

BFF acts as a perfect abstraction for underlying microservices. For an API, it can connect to necessary microservices, gather the responses, and respond. This ensures that we are not fetching data that we don't need.

For example, Given compatibility and constraints, a Desktop BFF can talk to Orders, Sellers, and Reviews Services, while a Mobile BFF can talk to Orders, Sellers, and AR services to respond to the same API endpoint.

## Advantages

- we can add client-specific tweaks and hacks on BFF
- we can hide sensitive information from specific clients
- we can patch client-specific vulnerabilities on respective BFF
- we can pick the best communication stack for the client and BFFs
- we can have a general-purpose backend supporting all kinds of clients

## Disadvantages

- a large chunk of code would be duplicated
- needs to support high fan-out, hence pick a stack that suits
- there is a slight increase in latency with the new network hop
- by adding BFFs we are adding more moving parts that need to be managed, maintained, monitored, and deployed

## Adopting BFF

We should adopt BFF when

- the interface between different clients varies significantly
- the communication format/protocol is different from what your backend supports (eg: legacy integration might need XML while your backend serves JSON)