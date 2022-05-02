Traditional databases like MySQL, Postgres, MongoDB run on their server on a specific port. Anyone who wants to talk to the database can directly connect and talk.

Embedded Databases are different from these traditional databases, and they operate in their own confined space within a process. There is no separate process for the database.

No one can directly connect to this database, unlike how we do it with MySQL and other databases. The role and the use of the embedded database are limited to the process it is confined to.

## Popular embedded databases are

- SQLite: an embedded SQL-like database
- LevelDB: on disk KV store by Google
- RocksDB: on disk KV store optimized for performance
- Berkeley DB: KV store with ACID, Replication, and Locking

An embedded database is always designed to solve one niche really well.

## Application of Embedded Databases

Every modern browser uses an embedded database called IndexedDB to store browsing history and other configuration settings locally. The browser is confined to a machine, and the IndexedDB is contained in the browser; there is no separate process to connect to.

Every Android phone has support for SQLite database that we can use to store any information like game scores, stats, and information locally on the phone.

The core idea: When we need to store and query data that could be confined within a space and does not need to be centralized, we choose to use an Embedded Database.