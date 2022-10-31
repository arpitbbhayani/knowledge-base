Phone numbers can be misused if gone into the wrong hands. But sometimes delivery agents need to reach out to us for directions.

So, do delivery agents get our phone numbers?

Here's how Gojek ensures seamless communication without sharing actual phone numbers.

## Problem Statement

Say, customer A ordered something from Gojek and a delivery agent D gets assigned to this order.

We want to

- enable A to contact D
- enable D to contact A

but neither should have the other's phone numbers.

and we achieve this using...

## Virtual Phone Numbers

Instead of sharing the actual phone numbers of the users, we create virtual phone numbers which are

- temporary but functional
- can be assigned to any user at will

Telecom operators and providers like Twilio and Exotel provide these services.

### Is it for everyone?

If we assign a fixed VN to every user in the system

- does not improve the security posture
- we would need millions of virtual numbers

If VN remains the same for a user, then abusers can keep track, and attack the user; breaching their privacy.

## Constraints

Hence, the virtual numbers we assign to the users should be

- assigned on demand
- bound to a transaction/order

Once the transaction is over, or the order is delivered, we assign the VN to some other user.

so, how do we assign?

## Fetching Virtual Numbers

Instead of trying to get Virtual Numbers on the fly from the telecom operators and providers, we fetch them periodically and keep them handy in our database.

Say, we call this service VN service.

### Assigning Numbers

When a delivery agent is assigned to an order,

- we hit the VN database,
- fetch a couple of unused VN,
- and make an entry into the orders DB.

we show the assigned numbers on the app to the customer and the delivery agent.

If a user (customer/delivery agent) has multiple active orders, he/she will be assigned one VN for each active transaction.

Hence, if a delivery agent is delivering two orders at the same time, he/she will be assigned two VNs, ensuring privacy.

## Flow

A user places an order and the event is sent to Kafka, to be consumed by the consumers which ensure we have enough VNs available.

If not, more VNs are fetched from the telecom operators and providers.

Once the delivery agent is assigned to the order, the Kafka consumers fetch the VNs from the database and update the mapping in Orders DB.

This entry is used to render the phone number of the other party on the app.

so, what happens when a user calls the delivery agent's VN?

### Calling a VN

Say customer A wants to call the delivery agent D. Say, DDD is the virtual number of D that A has.

When A makes a call on the number DDD, the telecom provider gets the call and it needs the actual number to connect to.

Hence, it makes a call to the VN service. The VN service then checks

- who is calling
- to whom the call is made
- the existence of a valid transaction between A and D

once everything is validated, the VN service responds with A's VN and actual number against DDD.

The telecom provider then bridges the call that was initiated from A to the actual phone number of D but it sets the source phone number to VN of A.

This way, when the D receives the call, it does not see A's actual number, instead, it sees the VN of A.

This is how the customer and the delivery agent can connect over the phone call, while neither gets the actual phone number of the other.

This is exactly what Gojek does. The link to their blog is in the description of the attached video.