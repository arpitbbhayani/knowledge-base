A map, when implemented with Hash Tables, is called a Hash Map; and just like a regular map it supports operations like put, get, and iterate.

## Key Implementation Details

Hash Maps are required to store the application keys of any type, but the Hash Table understands only integers. We first pass the application keys through a hash function to map it to a 32-bit integer, and then the usual Hash Table operation takes over.

Given that the application key to hash key is a frequent operation, we would keep it handy by storing it alongside the application key. This helps us save repeated computations.

While looking up a key in the hash map, we first reach the slot, and then compare if the key present there is really the key we are looking for, as we cannot just rely on the equality of the hash keys. The Hash Map, hence, accepts a key comparator function.

## With Chained Hash Tables

Each node of the linked list in the chained hash table has the following structure

```
struct node {
    int32 hash_key;
    void *key;
    void *value;
    struct node *next;
}
```

`void * key` and `void * value` allows us to hold a key and a value of any type, while `int32 hash_key` enables us to hold a pre-computed hash.

At the Hash Table level, we hold

- the array of linked list
- size of the array
- number of keys
- key comparator function

Instead of having a `contains` function, we have a `lookup` function that returns the value for the matching key, and `NULL` if the key does not exist. Thus, the `lookup` function doubles as a `contains` function.

When duplicate keys are inserted, we can do one of the following

- do not insert at all
- delete the old key and re-insert it again, bringing it to the head of the list, making it quicker to reach

## With Hash Tables having open addressing

Each slot of the hash table has the following structure

```
struct node {
    int32 hash_key;
    void *key;
    void *key;
    bool is_empty;
    bool is_deleted;
}
```

`void *key` and `void *value` allows us to hold a key and a value of any type, while `int32 hash_key` enables us to hold a pre-computed hash, saving a lot of runtime computations. `is_empty` tells us if the slot is empty, while `is_deleted` represents a soft deleted slot.

At the Hash Table level, we hold

- the array of linked list
- size of the array
- number of active keys
- number of used slots
- key comparator function

Here the load factor will be computed as number of used slots/size of the array because the soft deleted keys also affect the performance of the hash table.

During insert, lookup, and delete when we find the matching hash, and explicitly compare the application keys, as multiple keys can hash to the same location, and we cannot rely on just hash key equivalence.