Grab stores and processes millions of orders every day, here is the design of the systems that powers it ⚡

The architecture of Grab's order platform is divided into two main databases, one for transactional queries and the other for analytical queries.

The transactional database holds transactional data about the orders that serve as the single source of truth for ongoing orders. In contrast, the analytical database holds historical and statistical data and stores it for longer periods. This database is defined to be more efficient for read-heavy analytical queries.

## Design Goals

Given the critical role that databases play in any system, the most important criteria for a good design are stability, availability, and consistency.

Stability is critical as the database must handle high volumes of queries per second. Availability is important because the database stores orders and any downtime could lead to revenue loss. Consistency ensures that users receive updated information when performing transactional queries. Therefore, strong consistency is necessary for transactional queries, while eventual consistency is sufficient for analytical queries.

## Architecture

### DynamoDB as Transactional Database

Grab uses DynamoDB as its primary data store. DynamoDB offers strong consistency, scalability, and high availability, making it an ideal choice for transactional queries.

Grab uses key-value queries such as get, create, and update orders, and DynamoDB's internal partition balancing feature to handle spikey traffic loads and hotkeys.

The orders table in DynamoDB contains several key attributes, including order ID, the state of the order (ongoing, completed, or canceled), the time the order was created, and the user ID.

To optimize performance, a global secondary index was created on the user ID, which allows for quick retrieval of ongoing orders for a particular user. When an order is completed, it is automatically removed from the index to keep it lean.

Grab has also designed its schema to keep its global secondary index (GSI) lean and performant by removing entries from the index after three months of inactivity.

### MySQL as Analytical Database

For analytical queries, Grab uses MySQL as its Analytical database. It is partitioned by the created_at, ensuring minimal cross-partition queries, and it drops old partitions to keep the database lean and consistent.

### Sync between databases

Grab uses Kafka to handle asynchronous batch ingestion from DynamoDB to MySQL. All events from the order service are sent to Kafka, which then updates the analytics database.

## Conclusion

In conclusion, Grab's order platform is an example of a complex system that balances consistency, availability, and cost-effectiveness to process millions of orders every day. By separating transactional and analytical queries into two separate databases, using specialized processing units, and leveraging modern data storage technologies, Grab has built a system that is highly scalable, available, and cost-effective.