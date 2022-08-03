Open Addressing is a common yet interesting way of handling collisions in Hash Tables and instead of using an auxiliary data structure, it leverages empty slots of the hash table to store the collided keys, making the entire approach space efficient.

While inserting a key in the hash table, we pass it through the hash function to get the slot, and if the slot is already occupied, we find the next available slot through probing.

## Probing

Probing is the process through which we deterministically find the next available slot in the hash table. The approach and algorithm could vary, but formally it is a function of the key to be placed and the attempt, that spits out a slot.

```
j = p(k, i)
```

The probing function uses the key `k` and an attempt `i` to spit out an index `j`. The attempt `i` and the index `j` are in the range `[0, m-1]`, where `m` is the size of the hash table.

### Good probing function

A good probing function would generate a deterministic permutation of numbers `[0, m - 1]` specific to the key `k`, so that we eventually check and cover the entire hash table for an available slot.

For example: for some key `k1`, on a hash table of size 8, the probing function might generate a sequence: 5, 7, 2, 1, 0, 6, 4, and 3. This means we first try to put the key in index `5`, if that is occupied we check `7`, then `2`, and so on.

## Hash Table Operations

### Adding a key

Until we find a free slot in the hash table, we keep invoking the probing function with attempts `0`, `1`, `2,`, etc. Once we find an empty slot, we stop and place the key in that slot.

### Key Lookups

For looking up a key, we invoke the probing function with attempt `0` and check the slot. If the slot holds the key we need, we stop and return the value. If not, we continue to probe with attempts `1`, `2`, etc., and continue to hunt.

We stop the iteration when

- we find the key,
- we stumble upon an empty slot during iteration
- we have checked the complete hash table

### Deleting a key

With open addressing, deleting a key from the table has to be a soft delete, because we need a way to differentiate between an empty slot and a deleted key.

If during deletion we empty the slot, then we would be unable to look and reach for a key that had a collision and was placed after the key we deleted.

## Limitation of Open addressing

Since we are not having any auxiliary data structure, a major limitation of Open Addressing is that the maximum number of keys we can hold are the same as the number of slots in the hash table.