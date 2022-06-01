Should every microservice have its own database?

Microservices need some persistence to store the state of the application. They also need to be loosely coupled with others so as to be autonomous and having a separate database for itself really helps, and this is the Database Per Service pattern.

## Modeling a social network

The importance of having a database per service can be seen when we model a social network. For every usecase, we would need a specialized database to keep our latencies to a bare minimum.

- Chat: a partitioned non-relational database like Cassandra
- Auth: a simple relational database with replicas like MySQL
- Profile: a nonrelational schemaless database like MongoDB
- Analytics: a massively scalable columnar storage like Redshift
- Videos: blob storage like S3

## Advantages of Database Per Service Pattern

### Loosely coupled components

Because the databases are separate, the services could not connect to other databases and would have to directly talk to each other making them loosely coupled.

### Specific DB for specific usecase

Services can pick the best database for their usecase making them super performant and efficient. For example, picking a Graph database to model relations in social networks instead of relational.

### Granular control and scaling

Services can choose their scaling strategies as per the load it is getting; be it vertical, horizontal, replicas, partitioned, or decentralized.

### Smaller blast radius

When any database is experiencing an outage only the services that are directly or indirectly dependent on it get affected and everything else continues to operate normally. For example, we can continue to accept the payments even when the profile service is down.

### Compliance

Compliance requires us to make changes in how our data is stored and moved across. Separate databases would help us in implementing changes on a fraction of data instead of the whole.

## Downsides of Database Per Service Pattern

### Transactions are distributed and expensive

If we need strong consistency across, we would need distributed transactions and those are expensive and complex to implement.

### Conveying updates requires brokers

Conveying updates from one service to another would require us to have message brokers, thus adding more things to manage and maintain.

### More infra to manage

Having a database per service bloats up our infra and we would need to build expertise in maintaining and managing them.