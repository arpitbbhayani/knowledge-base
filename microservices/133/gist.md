Microservices need to communicate with each other, and one such way of doing it is through a shared database.

For example: While building a multi-user blogging application, say we have a Blogs service that manages all the blogs-related information and we have an Analytics service that takes care of all the analytics like Likes, Shares, Views, etc.

Analytics service updates the information asynchronously directly in the blog's database; eg: total_views that happened on the blog. This can be easily achieved by sharing the database between Blogs and Analytics, and this pattern is the Shared Database pattern.

### Advantages of sharing the database

- the simplest way of integration
- no middleman involved
- no latency overhead
- quick development time

## Challenges with Shared Database

There are 4 challenges to using this pattern

### External parties know internal details

By sharing the database across services, an external party (Analytics) would get to know the internal details of the Blogs service; eg: deletion practice, schema, etc.

This leads to a very tight coupling between the services; which then restrains the maintainability and performance of the system. For example, whenever the Blogs service changes the schema, the Analytics Service would have to be informed about the change.

### Sharing the database is sharing the logic

To compute some information we need to query a set of tables; and say, this information is required by the Blogs, Analytics, and Recommendation service.

The business logic to compute the information has to be replicated across all the 3 services. Any change in the logic needs to be made across all the services.

### Risk of data corruption and deletion

There is a risk that one of the services might corrupt or delete some data given that the database is shared between the services.

### Abusing the shared database

One service firing expensive queries on the database will affect the performance of other services sharing the same database.

## When to share a database?

A shared database pattern is helpful when you are seeking quick development time. Although it is not the best practice, sharing the database does reduce the development effort by a massive margin.

Sharing the database is also seen where it is inconvenient to have a middleman for the communication; for example: sending a notification to a million followers of a person is simple when the Relationship database is shared with the notification fan-out service; instead of iterating the millions of followers through some middleman API.