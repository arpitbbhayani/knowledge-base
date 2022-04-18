How does the database guarantee reliability using write-ahead logging?

Any persistence database needs to guarantee the reliability, implying that any update/delete fired on the database is reliably stored on the disk. The alterations on the data should not be affected by power loss, OS failure, or hardware failure.

To update a certain row of the database, the database engine first reads the block in the memory, performs the update, and flushes the block to the disk. The database engine writes the updates on the blocks that represent the table data and the indexes during the flush.

What if, just before the flush, the database process crashed? The changes that remained in the memory are lost. How do databases prevent this? The answer is super-simple

✨ Write-ahead Logging ✨

Write-ahead logging is a standard way to ensure data integrity and reliability. Any changes made on the database are first logged in an append-only file called write-ahead Log or Commit Log. Then the blocks on the disk are updated.

An operation like Update Query, Delete Query is logged in the commit log and not the actual changes making the write lightning-fast.

✨ Advantages of using WAL

 - we can skip flushing the data to the disk on every update
 - significantly reduce the number of disk writes
 - we can recover the data in case of a data loss
 - we can have point-in-time snapshots

✨ Data integrity in WAL

WAL also takes care of its data integrity by writing a CRC-32 before logging the operation. This CRC is checked during reading and replicating.