Linear probing is the simplest and one of the most efficient ways to handle conflicts in Hash Tables, let's understand it in-depth.

## Conflicts

Conflicts are inevitable, and Open Addressing is a technique to handle them in a space-efficient way. Instead of using an auxiliary data structure to hold the collided keys, open addressing leverages the free slots of the Hash Table to accommodate the collided keys.

To find the next available slot, open addressing defines a probing function that uses the key and the attempt to deterministically iterate through the slots.

## Linear Probing

We first hash the key and find a primary slot. If that slot is free, we place the key there. If the slot is occupied, we check the slot to its right. We continue to process until we find an empty slot.

This way, we continue to hunt for the key linearly from the primary slot. Once we reach the end of the array, we circle back to index 0. Formally, the probing function for Linear Probing would be

```
p(k, i) = (h(k) + i) mod m
```

## Hash Table Operations

### Adding a key

We first find the primary slot of the key using the hash function. If the slot is empty, we place the key there. If not, we move to the right and find the first empty slot and place the key there.

### Key lookup

Lookup is an iterative process where we first find the primary slot of the key, if the key is present at that slot then well and good. If not, we move to the right hunting for the key. We continue to linearly iterate through the array until

- the key is found, or
- we encounter an empty slot
- we cover all `m` slots of the hash table

### Deleting a key

Deleting a key in Linear Probing is always a soft delete. We first look up the key in the hash table and once we find it, we mark that slot as deleted but never physically empty it. This allows us to go beyond the deleted slot and hunt for any other collided keys.

## Why is Linear Probing Fast?

Linear probing is fast because it beautifully exploits the locality of reference. To access a certain slot in the hash table, we fetch the page in the CPU cache. The page will not just contain the requested slot, but it also contains the neighboring slots as well.

Hence, upon collision when we iterate from that slot, we would not need to fetch the slots from RAM, instead, some slots would already be present in the cache making iterations superfast.

In an average case, Linear Probing gives constant time performance for adding, lookup, and deleting a key.

## Challenges with Linear Probing

1. Bad hash function would lead to many collisions
2. It suffers from non-uniform clustered collisions

Hence, it is important to pick a good hash function, like Murmur Hash, to ensure a near-uniform distribution of keys and fewer collisions.