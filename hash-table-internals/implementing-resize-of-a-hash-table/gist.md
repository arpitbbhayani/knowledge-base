Resizing a Hash Table is important to maintain consistent performance and efficiency, but how do we actually implement it?

Resize is all about

- allocating a new array of the desired size
- insert existing keys in this new array
- delete the old array

but a few granular details are specific to the type of hash table.

## Resizing a Chained Hash Table

Resizing a table happens when the load factor hits a threshold. To implement an efficient resize a Hash Table that uses chaining needs to keep track of

- number of keys
- total number of slots

This would help us avoid reevaluation and we can instantly compute the load factor.

### Resize during insert

While we are inserting a key in the Hash Table, we keep on checking the load factor. If it breaches the threshold we trigger the resize.

```
insert_key(k, table) {
    ------
    LF = count_keys / total_slots;
    if (LF >= 0.5) {
        resize(table, total_slots * 2)
    }
}
```

### Shrinking during delete

While we delete a key from the Hash Table, we check the load factor. If it breaches the threshold we trigger the shrink. The pseudocode is fairly similar to the above one.

### Two ways to implement resize

Chained Hashing is implemented using Linked List and there are two ways to resize

1. we iterate through the keys and re-insert them into the new array
2. we iterate through the keys and just adjust the pointers of the nodes, instead of re-allocating the new set of nodes.

## Resizing a Hash Table with Open Addressing

In open addressing, we always soft delete so that we can reach the elements placed further in the collision chain. To handle this gracefully, we need two counters at the hash table

1. Key Counter: number of active keys in the table
2. Used Counter: number of used slots in the table

For open addressing, the load factor will be counted as the used counter divided by the total slots. The deleted keys also affect the performance as we have to go past them looking for the keys.

Hence, the Key Counter will increase and decrease upon every insert and delete while the used counter would increase upon insert but would reduce only when we do a resize.

### Resize during insert

While we are inserting a key in the Hash Table, we check the load factor. If it breaches the threshold we trigger the resize. Resize operation would skip the deleted keys and re-insert only the active keys.

### Shrinking during delete

The shrinking of the hash table will be triggered when the number of active keys falls beyond the threshold and hence here our load factor for this operation would be active keys / total_slots.

Similar to the insert phase, we would skip the deleted keys and re-insert only the active keys in the new array. The key counter and the user counters are adjected accordingly.