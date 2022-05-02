## What is throttling?

Throttling is a technique that ensures that the flow of the data or the requests being sent at the target machine/service/sub-system can be consumed at an acceptable rate.

It is a defensive measure and 3 possible reactions could be

 - slowing down the incoming requests
 - rejecting the surplus requests
 - ignoring the surplus requests

## Why do we need throttling in the first place?

 - to prevent system abuse
 - to allow the amount of traffic we could handle
 - control the consumption cost
 - prevent cascading failures leading to a massive outage

# Real-world use-cases for throttling

## To prevent catastrophic DDoS attack

When your service is under a DDoS attack the rate limiter acts as your first line of defense that could prevent the surplus request from reaching your system. It would only allow the requests to go through at the configured rate.

## To gracefully handle a surge of users

It is possible that your product goes viral and now you are seeing a genuine surge in users. Upon getting a genuine surge in users, the stateful components like databases and caches crash which takes down the entire site.

Rate limiter in this case will help in preventing the entire site from going down; although some users would see some error, like 429- Too many requests- your product will continue to seamlessly work for the other set of users.

## Multi-tiered limits

Say, you are running a CICD company and offer 3 tiers of pricing- Tier 1 offers 200 minutes of build time, Tier 2 offers 1000 mins while Tier 3 offers unlimited build time. An internal rate limiter can keep track of the build times consumed by a customer and reject the requests once the limit is hit.

## Ensure you are not over-consuming

Say, we are consuming a super expensive third-party API and we want to ensure that we are not using it beyond a certain number otherwise the cost will shoot up. An internal rate limiter can keep a check on this to ensure the surplus request does not go through.

## Not overwhelming an unprotected system

Hard deleting from a database is an expensive operation. If we are deleting a huge number of rows from the DB it may severely affect the performance of the DB and hence it is best done in a staggered way. An internal rate limiter can help us streamline the writing by spreading them uniformly across time.