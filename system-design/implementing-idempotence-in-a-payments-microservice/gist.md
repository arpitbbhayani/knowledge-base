How can you implement idempotence in a Payments Microservice? [in a gist ]

Idempotence is executing the same action multiple times, but the result is as if the operation was applied just once.

Example: Double tapping a post multiple times on Instagram does not increase the like count. It just increases the first time and by 1.

Idempotence becomes extremely critical when money is involved. If A wants to transfer money to B, the transfer should happen just once. If due for any reason, the payment is implicitly retried, the funds will be deducted twice, which is unacceptable.

⚡ Why would a transaction repeat?

Before we talk about idempotence, it is important to understand why it would repeat in the first place.

Consider a situation where the payments service initiated a payment with a Payment Gateway, the money got deducted, but the payments service did not get the response. This would make the Payments service retry the API call, which would lead to a double deduction.

⚡ Implementing idempotence

Check and Update: Weave everything with a single ID.

The idea is to retry only after checking if the payment is processed or not. But how do we do this? The implementation is pretty simple- a global payment ID that weaves all the services and parties together.

The flow is:

 1. Payments service calls the PG and generates a unique Payment ID
 2. Payments service passes this ID to the end-user and all involved services
 3. Payments service initiates the payment with Payment Gateway with this ID specifying the transfer between A and B
 4. If there are any failures, the Payment service retries and in that request specifies the Payment ID
 5. Using the payment ID, the payment gateway checks if the transfer was indeed done or not and would transfer only when it was not done

Although we talked about the Payments service here, this approach of implementing idempotence is pretty common across all the use cases. The core idea is to have a single ID (acting as the Idempotence Key) weaving all the involved services and parties together.