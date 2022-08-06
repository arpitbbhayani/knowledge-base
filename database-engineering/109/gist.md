The database is just a collection of records. These records are serialized and stored on the disk. The way the records are serialized and stored on the disk depends on the database engine.  
  
## How does the database read from the disk?  
A disk is always read in Blocks, and a block is typically 8kb big. When any disk IO happens, even requesting one byte, the entire block is read in memory, and the byte is returned from it.  
  
Say we have a "users" table with 100 rows, with each row being 200B long. If the block size is 600B, we can read 600/200 = 3 rows in one disk read.  
  
To find all users with age = 23, we will have to read the entire table row by row and filter out the relevant documents; we will have to read the entire table. In one shot, we read 3 rows so that it would take 100/3 = 34 disk/block reads to answer the query.  
  
## Let's see how indexes make this faster.  
  
An index is a small referential table with two columns: the indexed value and the row ID. So an index on the age column will have two columns age (4 bytes) and row ID (4 bytes).  
  
Each entry in the index is 8 bytes long, and the total size of the index will be 100 * 8 = 800 bytes. When stored on the disk, the index will require 2 disk blocks.  
  
When we want to get users with age == 23, we will first read the entire index, taking 2 disk IOs and filtering out relevant row IDs. Then make disk reads for the relevant rows from the main table. Thus we read 2 blocks to load the index and only relevant blocks have the actual data.  
  
In our example, it comes out to be 2 + 2 = 4 block reads. So, we get an 8x boost in performance using indexes.  
  
Note: This is a very crude example of how fetch happens with indexes; there are a lot of optimizations that I have not talked about.  