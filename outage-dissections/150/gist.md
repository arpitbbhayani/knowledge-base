Imagine you created an index on a table and instead of boosting the performance, it lead to an outage 🤦‍♂️ GitHub ran a migration to reverse an index and it lead to a 60 mins outage.

Note: The example we have taken is pure speculation, the official incident report had minimal information about the outage. But the write-up will make you aware of possible challenges that might come during such situations.

## Reverse an index

Reversing the order of the index is done when we have a multi-column index and the query requires different sorting orders on them; for example, `DESC` on `date` and `ASC` on `user_id`.

For a query to be optimally executed on the database, we would need an index that physically stores the index ordered by the `date` in the descending order and `user_id` in the ascending order.

MySQL by default stores any index in `ASC` order and hence, GitHub had to run the migration to reverse the order of the index and gain a boost.

## What could go wrong?

A reverse index would require a Full Table Scan during the creation putting a load on the database. Also, upon changing the order of the index, it is possible we overlook another query that is more frequent but optimal with the old order.

The database does its best to create an optimal execution plan and it might not use the reverse index we just created. We can solve this by specifying Index Hints like `USE INDEX` and `FORCE INDEX`, ensuring that it uses our index to evaluate the query.

## Cascading Effect

Because one of the queries was doing a Full Table Scan, it put a load on the database which had a cascading effect on the service eventually propagating to the end user. All the intermediate services will timeout giving a degraded experience to the user.

## Key Takeaways

### Never blindly trust ORM

ORMs are designed to make our lives simpler but they might not generate the most optimal queries, and hence it is always better to periodically audit the queries and ensure they are optimal.

Poorly generated queries will put a load on the database choking the entire performance.

### Check the query execution plan

While updating a query or changing a schema always check the query execution plan. We can get the execution plan for any query using the `EXPLAIN` statement.

The diff in the plan would give tell us if any of our queries would perform a full table scan.

### Audit the queries and indexes

Keep an inventory of the queries we fire and the indexes it uses during execution. So, whenever we change any index, we can quickly run an audit and ensure zero regressions.