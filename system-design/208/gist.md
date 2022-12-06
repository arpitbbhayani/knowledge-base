The review system for Booking is one critical service as it drives business and hence making it highly available becomes extremely crucial.

Here's a thread about building a highly available system and the architecture of Booking's Review Service 👇‍

## Importance

Review shown on Booking.com are authentic and it helps people make a decision and thus bring in revenue.

The review system is also a high-throughput system as people can land on it from Search Engines or internal navigation.

## Review API Service

The core Review Service will be a simple REST-based API that exposes endpoints to create, read, update, and delete reviews.

Review Service of Booking handles 10,000 requests per second at peak with p99 of 50ms.

Given that the latncy requirement is too stringent, Booking serves most of the review from a centralized remote Cache and has done a bunch of optimizations on the Database through materialized views.

## Configuring storage

Booking.com has 250 million reviews and given the amount of info a review holds, they store these reviews in a shared datastore. 

Given Booking needs storage to be highly available, they configured each database to have multiple replicas and that too across regions to tolerate regional outages.

## Auto-scaling Storage

Given that the traffic for a travel business surges during the holiday season, the database needs to be scaled up to handle the load.

But keeping the database scaled up throughout the year without much load is very inefficient and hence Booking.com required some so of storage autoscaling.

Scaling up and down a sharded database requires us to add and remove nodes; but doing this naively requires the data to be re-partitioned.

To keep the movement to a bare minimum during scaling, Booking.com chose Consistent Hashing for determining data ownership.

## Architecture

1. Review Service is a simple REST service
2. Centralised cache and materialized views for quicker response
3. Database is sharded to handle larger loads
4. Data ownership is determined by Consistent Hashing
5. Database is replicated across within and across regions for HA