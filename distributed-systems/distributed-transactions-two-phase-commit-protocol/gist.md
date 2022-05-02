Distributed Transactions are essential to have strong consistency in a distributed setup.

An example could be as simple as a 10-min food/grocery delivery- where to guarantee a 10-min delivery, you can only accept orders when there are goods available in the dark store, and a delivery agent is available to deliver the goods.

This is a classic case of Distributed Transaction where you need a guarantee of atomicity and consistency across two different services. In a distributed setup, we can achieve it using an algorithm called Two-phase Commit.

The core idea of 2PC is: Split the transaction into two phases: Reservation and Assignment.

# Phase 1: Reservation

The Order service will first talk to store service to reserve food items and delivery service to reserve a delivery partner. When the food or delivery partner is reserved, they are not notified. By reserving them, we are just making them unavailable for everyone else.

If the order service fails to reserve any of these, we roll back the reservation and abort the transaction informing the user that the order is not placed. Reservation comes with a timer, which means if we cannot assign a reserved food item to order in "n" minutes, we will be releasing the reservation, making them available for other transactions.

We move forward to the Commit phase only when the order service reserves both- a food item and a delivery agent.

# Phase 2: Commit

In the Commit phase, the order services reach out to the store service and the delivery service to assign the food and agent to the order. Because the food and the agent were reserved, no other transaction could see it, and hence with a simple assignment, we can get the reserved food and agent assigned to an order.

Upon this assignment, the store and the delivery agent are notified about the order and proceed with their respective duties.

We retry a few times if any of the assignments fail (which could happen only if the service goes down). If we still cannot get the assignment done, we inform the user that the order cannot be placed.

The order is placed only after the food item, and the delivery agent is assigned to the order.