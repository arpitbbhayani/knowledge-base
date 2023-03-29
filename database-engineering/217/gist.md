Relational Databases and some non-relational databases use B+ trees to hold the data but why?

One of the main reasons why SQL databases use B+ trees to hold the data is because of their efficiency in performing operations such as insert, update, find, and delete.

## Limitations of Sequential Files

Before we delve into the details of why SQL databases use B+ trees, let's first understand the limitations of storing data in a sequential file.

When records of a table are stored in one file sequentially, performing operations such as insert, update, and delete becomes complicated, with a complexity of O(n). The linear scan in the middle of the file for insertion or overriding can take up a lot of time and resources, making it inefficient.

## Where B+ Trees thrive

In B+ trees, rows or documents of a table are clubbed in B+ tree nodes, and each node holds a maximum of some `n` rows. For example, if one B+ tree node is 4KB big (same as a disk block size) and the row size is 40B, then each node will hold a maximum of 100 rows. This makes disk reads efficient since reading one node from a disk means reading 100 rows at once.

Non-leaf nodes in a B+ tree hold routing information, while leaf nodes hold the actual rows. The leaf nodes are linked so that linear traversal of the actual rows is possible. The B+ tree structure thus ensures that the table is always logically and physically arranged by its primary key

## CRUD Operations with B+ Trees

### Finding row by ID

Finding a row by ID involves

1. traversing from the root node,
2. reaching the leaf node that holds the row,
3. reading the node and disk blocks in the main memory, and
4. extracting the row from the node and returning

### Inserting a new row

Inserting a new row involves

1. finding the leaf node where the row should be placed
2. reading the node in the main memory
3. inserting the node
4. rebalancing the tree, if needed
5. flushing a leaf node where the value is updated

### Updating a row

Updating a row involves

1. finding the leaf node that holds the row
2. reading the node (disk blocks) in the main memory
3. updating the row in memory, and
4. flushing the blocks to the disk.

### Deleting a row

Deleting a row involves

1. finding the leaf node that holds the row,
2. reading the node (disk blocks) in main memory,
3. removing the row from the node, and
4. flushing the blocks to the disk
5. re-balance the tree, if required

## Range Queries with B+ Trees

Range queries such as finding rows with IDs in the range of 100 to 600 involve finding the leaf node that holds the first row, traversing linearly to reach the row with ID 600, and extracting the data until then.

The B+ tree structure ensures that the time complexity of these operations is O(log n), which is much more efficient than the O(n) complexity of sequential file storage.

## Conclusion

In conclusion, SQL databases use B+ trees to store data efficiently and perform operations such as insert, update, find, and delete with a time complexity of O(log n). This makes managing and storing large volumes of data more manageable and efficient.