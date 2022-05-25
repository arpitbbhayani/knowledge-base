Vertical sharding is fine, but how can we actually implement it? 🤔

## Vertical Sharding

Vertical sharding is splitting a database by the tables. Shards will hold a subset of tables. For example, all payments-related tables go to one shard, while all auth-related tables go to another.

So, how to implement it?

## Need for a configuration store

For our API servers to talk to the correct database we would need a configuration store that holds the information for all the tables mapped to the database server that holds it.

For example, the Users table is present on DB1 while Transactions on DB2

Whenever the request comes, the API servers first check the config to find which DB holds the table and then fire the SQL query to that specific database for the table.

### Reactive update

All API servers will cache the configuration to avoid an expensive network call to get the database ensuring we get a solid boost to the performance.

When a table is moved from one database server to another, the configuration will be updated and hence the changes would need to be reactively propagated to all the API servers. Hence our config store needs to support reactive communication.

This is where we choose Zookeeper which is resilient and battle-tested to achieve this.

## Moving tables

Say, we are moving table `T2` from database server DB1 to DB2. Moving the table from one server to another is done in 4 simple steps.

### Dump the table `T2`

We first dump the table `T2` from DB1 transactionally using the utility `mysqldump` that not only dumps the table data but also records the position in the `binlog`. This is like taking a point-in-time snapshot of the table.

### Restore the dump

We now restore the dump to database DB2. This way we will have a database server with the table `T2` containing data till a certain point in time.

### Sync table `T2` on DB1 and DB2

We now setup the replication from DB1 to DB2 specifically for sync changes happening on table `T2`. It is done through a custom job that will use the recorded `binlog` position and start syncing from it.

### Cutover

Once the table `T2` is synced with almost 0 replication lag on DB1 and DB2 we cutover. We first rename the table to `T2_bak` and update the config in Zookeeper.

As we rename the table any queries going to DB1 for table `T2` will start throwing "Table not found" errors, but as Zookeeper will propagate the changes to all API servers they would use DB2 to fire any query on table `T2`, thus completing the table movement.

This is how you can implement vertical sharding.