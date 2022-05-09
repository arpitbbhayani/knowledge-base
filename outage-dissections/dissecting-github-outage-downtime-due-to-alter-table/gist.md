Can an ALTER TABLE command take down your production? 🤯

It happened to GitHub on 27th November 2021 when most of their services were down because of a large schema migration.

# Why did the outage happen?

GitHub ran a migration on a massive MySQL table and it made their replicas enter deadlock and crash. Here are the 5 insights about their architecture

## Insight 1: Schema migration can take weeks to complete

Schema migrations are intense operations as in most cases require you to copy the entire table with the new schema. Hence it might take a schema migration weeks to complete.

## Insight 2: The last step of migration is RENAME

To protect the database from not taking excessive locks during the migration, we create an empty ghost table from the main table, apply migration, copy the data, and then rename the table. This reduces the locks we need for the migration.

## Insight 3: Read Replicas can have deadlocks

The writes happening through the replication job and the production read load can create deadlocks on the read replicas.

## Insight 4: Have a separate fleet of replicas for internal traffic

Have a separate fleet of Read Replicas for internal workflows ex: analytics, etc. This way, any internal load will not affect the production load.

## Insight 5: Database failures cascade

When a replica fails, the load on healthy one's increases; which may them down and hence the cascading effect.

# Mitigation

The outage happened because there were not enough read replicas to handle the load, hence in order to mitigate it the way out was to add more read replicas. GitHub team very smartly promoted the replicas used for internal workloads to handle production.

Although the move was smart, it did not mitigate the outage because the incoming load was so high that the new replicas added also started crashing.

## Data Integrity over Availability

To ensure that the data integrity is not compromised because of repeated crashes, GitHub took a call and let the Read traffic fail. They took the replica out of the production fleet, gave it time to complete the migration, and then added it back.

This way all the replicas got the time they needed to complete the schema migration. It took some but the issue was completely mitigated.

# Long-term fix

Vertical Partitioning is a long-term fix for this problem. The idea is to create smaller databases that hold related tables; ex: all tables related to Repositories can go in one DB. This allows migration to quickly complete and during an outage, only the involved functionalities will be affected.