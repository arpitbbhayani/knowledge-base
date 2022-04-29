On the 5th of May, 2020, GitHub experienced an outage because of this very reason. One of their shared table having an auto-incrementing ID column hits its max limit. Let's see what could have been done in such a situation.

# What's the next value after MAX int?

GitHub used 4 bytes signed integer as their ID column, which means the value can go from `-2147483648` to `2147483647`. So, now when the ID column hits `2147483647` and tries to get the next value, it gets the same value again, i.e., `2147483647`.

For MySQL, `2147483647` + `1` = `2147483647`

So, when it tries to insert the row with ID `2147483647`, it gets the *Duplicate Key Error* given that a row already exists with the same ID.

# How to mitigate the issue?

A situation like this is extremely critical given that the database is not allowing us to insert any row in the table. This typically results in a major downtime of a few hours, and it depends on the amount of data in the table. There are a couple of ways to mitigate the issue.

## Approach 1: Alter the table and increase the width of the column

Quickly fire the `ALTER` table and change the data type of the ID column to `UNSIGNED INT` or `BIGINT`. Depending on the data size, an ALTER query like this will take a few hours to a few days to execute. Hence this approach is suitable only when the table size is small.

## Approach 2: Swap the table

The idea here is to create an empty table with the same schema but a larger ID range that starts from `2147483648`. Then rename this new table to the old one and start accepting writes. Then slowly migrate the data from the old table to this new one. This approach can be used when you can live without the data for a few days.

## Get warned before the storm

Although mitigation is great, it is better to place a monitoring system that raises an alert when the ID reaches 70% of its range. So, write a simple DB monitoring service that periodically checks this by firing a query on the database.