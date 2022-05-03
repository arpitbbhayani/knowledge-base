Distributed Transactions are not theoretical; they are very well used in many systems. An example of it is 10-min food/grocery delivery.

Previously we went through the theoretical foundation for the Two-phase commit protocol; in this one let's spend some time going through the implementation detail and a few things to remember while implementing a distributed transaction.

> The UX we want is: Users should see orders placed only when we have one food item and a delivery agent available to deliver.

A key feature we want from our databases (storage layer) is atomicity. Our storage layer can choose to provide it through atomic operations or full-fledged transactions.

We will have 3 microservices: Order, Store, and Delivery.

An important design decision: The store services have food, and every food has packets that can be purchased and assigned. Hence, instead of just playing with the count, we will play with the granular food packets while ordering.

# Phase 1: Reservation

Order service calls the reservation API exposed on the store and the delivery services. The individual services reserve the food packet (of the ordered food) and a delivery agent atomically (exclusive lock or atomic operation).

Upon reservation, the food packet and the agent become unavailable for any other transaction.

# Phase 2: Assignment

Order service then calls the store and delivery services to atomically assign the reserved food packet and the delivery agent to the order. Upon success assigning both to the order, the order is marked as successful, and the order service returns a 200 OK to the user.

The end-user will only see "Order Placed" when the food packet is assigned, and the delivery agent is assigned to the order. So, all 4 API calls should succeed for the order to be successfully placed.

Negative cases:

- If any reservation fails, the user will see "Order Not Placed"
- If the reservation is made but assigning fails, the user will see "Order Not Placed"
- If there is any transient issue in any service during the assignment phase, APIs will be retried by the order service to complete the order.
- To not have a perpetual reservation, every reserved packet and delivery agent will have an expiration timer that will be large enough to cover transient outages.

Thus, in any case, an end-user will never experience a moment where we say that the order is placed, but it cannot be fulfilled in the backend.