An edge case took down GitHub 🤯

GitHub experienced an outage where their MySQL database went into a degraded state. Upon investigation, it was found out that the outage happened because of an edge case. So, how can an edge case take down a database?

## What happened?

The outage happened because of an edge case which lead to the generation of an inefficient SQL query that was executed very frequently on the database. The database was thus put under a massive load which eventually made it crash leading to an outage.

### Could retry have helped?

Automatic retries always help in recovering from a transient issue. During this outage, retries made things worse. Automatic retries added the load on the database that was already under stress.

## Fictional Example

Now, we take a look at a fictional example where an edge case could potentially take down a DB.

Say, we have an API that returns the number of commits made by a user in the last `n` days. The way, this API could be implemented is to get the `start_date` as an integer through the query parameter, and the API server could then fire a SQL query like

```
SELECT count(id) FROM commits
WHERE user_id = 123 AND start_time > start_time
```

In order to fire the query, we convert the string `start_time` to an integer, create the query, and then fire it. In the regular case, we get the correct input and then compute the number of commits and respond.

But as an edge case, what if we do not get the query parameter or we get a non-integer value; then depending on the language at hand we may actually use the default integer value like `0` as our `start_time`.

There is a very high chance of this happening when we are using Golang which uses `0` as the default integer value. In such a case, the query that gets executed would be

```
SELECT count(id) FROM commits
WHERE user_id = 123 AND start_time > 0
```

  
The above query when executed iterates through all the rows of the table for a particular user, instead of the rows for the last 7 days; making it super inefficient and expensive. The above query would put a huge load on the database and a frequent invocation can actually take down the entire database.

### Ways to avoid such situations

1. Always sanitize the input before executing the query
2. Put guard rails that prevent you from iterating the entire table. For example: putting `LIMIT 1000` would have made you iterate over 1000 rows in the worst case.