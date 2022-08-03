The set data structure, when implemented with Hash Tables, is called a Hash Set; and just like a regular set, it supports operations like Union, Intersection, and Difference.

## Key Implementation Details

Hash sets are required to store the application keys that could be strings, integers, objects, etc., but the Hash Table understands only integers. We first pass the application keys through a hash function to map it to a 32-bit integer, and then the usual Hash Table operation takes over.

Given that the application key to hash key is a frequent operation, we would keep it handy by storing it alongside the application key. This helps us save repeated computations.

It is quite possible that multiple application keys would map to the same hash key, hence while looking up a key in the hash set, we first reach the slot, and then compare if the key present there is really the key we are looking for as we cannot just rely on the equality of the hash keys.
 
To achieve this, our Hash Set would need to accept a comparator function that can be used to compare two application keys for equality. Hash Set would use this comparator to check for the key equality, making our implementation agnostic.

## Hash Sets with Chained Hash Tables

Each node of the linked list in the chained hash table would have the following structure

```
struct node {
    int32 hash_key;
    void *key;
    struct node *next;
}
```

`void * key` would allow us to hold a key of any type, while `int32 hash_key` would enable us to hold a pre-computed hash, saving a lot of runtime computations.

At the Hash Table level, we would hold

- the array of linked list
- the size of the array
- number of keys
- key comparator function

## Hash Sets with Hash Tables having open addressing

Each slot of the hash table will have the following structure

```
struct node {
    int32 hash_key;
    void *key;
    bool is_empty;
    bool is_deleted;
}
```

`void * key` would allow us to hold a key of any type, while `int32 hash_key` would enable us to hold a pre-computed hash, saving a lot of runtime computations. `is_empty` would tell us if the slot is empty, while `is_deleted` would represent a soft deleted slot.

At the Hash Table level, we would hold

- the array of linked list
- the size of the array
- number of active keys
- number of used slots
- key comparator function

Note: here the load factor will be computed as the number of used slots/size of the array because the soft deleted keys also affect the performance of the hash table.

During insert, lookup, and delete when we find the matching hash, we need to explicitly compare the application key because multiple application keys can hash to the same location, and hence we cannot rely on just hash key equivalence.