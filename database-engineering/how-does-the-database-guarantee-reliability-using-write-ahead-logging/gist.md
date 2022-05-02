Any persistent database needs to guarantee the reliability, implying that any update/delete fired on the database is reliably stored on the disk. The alterations on the data should not be affected by power loss, OS failure, or hardware failure.

The changes to the data once committed should do to non-volatile storage like Disk making them outlive any outage or crash. Although the flows seem simple enough to say that- hey let's just flush the changes to the disk; it is a little more complicated than that.

## Disk writes are complicated

When we perform the disk write, the changes are not directly written to the disk sectors, instead, it goes through a variety of buffers like RAM, OS Cache, Disk Cache, and then finally to the Disk sectors. So, if the changes are in any of these intermediate caches and the process crashes, our changes are lost.

So, while guaranteeing reliability we have to skip all of these caches and flush our changes as quickly as possible on the disk sectors. But if we do that, we are impacting the throughput of the system given how expensive disk writes are.

# Write-ahead Logging

Write-ahead logging is a standard way to ensure data integrity and reliability. Any changes made on the database are first logged in an append-only file called write-ahead Log or Commit Log. Then the actual blocks having the data (row, document) on the disk are updated.

If we update any row or a document of a database, updating the data on disk is a much slower process because it would require on-disk data structures to rebalance, indexes to be updated, and so much more. So, if we skip the OS cache, and other buffers, and directly update the rows to the disk every time; it will hamper the overall throughput and performance of the database.

Hence, instead of synchronously flushing the row updates to the disk, we synchronously just flush the operation (PUT, DEL) in a write-ahead log file leading to just one extra disk write. The step will guarantee reliability and durability as although we do not have the row changes not flushed but at least the operation is flushed. This way if we need to replay the changes, in case of a crash, we can simply iterate through this simple file of operations and recover the database.

Once the operation is logged, the database can do its routine work and make the changes to the actual row or document data through the OS cache and other buffers. This way we guarantee reliability and durability in as minimal of a time as possible while not affecting the throughput much.

## Advantages of using WAL

The advantages of using WAL are

- we can skip flushing the data to the disk on every update
- significantly reduce the number of disk writes
- we can recover the data in case of a data loss
- we can have point-in-time snapshots

## Data integrity in WAL

WAL also needs to ensure that any operation flushed in the log is not corrupted and hence it maintains its integrity using a CRC-32 and flushes it on the disk with every entry. This CRC is checked during reading the entry from the disk, if it does not match the DB throws an error.