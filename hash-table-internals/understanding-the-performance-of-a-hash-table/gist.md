Hash Tables are designed to give a constant time performance and to do this, it needs to have a large number of slots available. Since we cannot allocate a huge chunk of memory at first, we need Hash Tables are great because they are performant.

Which factors make them performant?

## Load Factor

Load Factor is a quantification that makes it simple for us to tell how loaded the Hash Table is and it is just a simple division of the number of keys and the number of slots in the hash table.

As the load factor increases, the performance of the Hash Table decreases. It happens purely because it takes longer for us to do a slot lookup and find an empty slot to place the key.

## The Best Strategy

Every probing strategy or collision resolution strategy has its merit and de-merit and they all perform the best in a certain condition and the worse in others. Let's take a detailed look.

### Chained Hashing

Chained Hashing is costly as it requires us to do a linear traversal of the linked list to find the key we are looking for. As the collisions increase, the lookup time shoots up, degrading the performance.

Chained Hashing is not cache-friendly as it requires us to do random lookups in the memory while hopping from one linked list node to another.

### Double Hashing

Evaluating two hash functions requires extra CPU cycles that could get taxing. Double Hashing is also not cache-friendly as it requires us to chump across the Hash Table to hunt an empty slot.

The optimal strategy is contextual. If the performance of the Hash Table is critical then we need to experiment, tune, and evaluate the best that fits us.

## Lookup Time vs Load Factor

Lookup Time is the most critical metric in evaluating the performance of the Hash Table; when we benchmark Lookup Time vs Load Factor we would see

- perf of Open Addressing degrades as the load factor increases
- perf of Chained Hashing degrades gracefully with load factor
- Linear Probing would be slower than Double Hashing
- Probes required for Double Hashing would be shorter

## Making Chained Hashing cache efficient

Chained Hashing is known for being cache-inefficient as it requires us to traverse through linked list nodes that may be present across the heap. Can we somehow make it cache efficient?

To make Chained Hashing cache-friendly, we have to ensure that the nodes of the linked list are allocated contiguously instead of randomly. Hence, instead of allocating one node at a time, we allocate the space for 5 nodes (like an array) at a time and then form the linked list out of them.

This would make the linked list leverage the CPU cache well and ensure our iterations are efficient as the next nodes will be available in the CPU cache not requiring us to fetch them from the main memory.