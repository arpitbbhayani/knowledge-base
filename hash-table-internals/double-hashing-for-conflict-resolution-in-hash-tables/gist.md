Linear and Quadratic probing do a great job at handling collisions in a Hash Table, but they both suffer from Clustered Collision, which degrades performance. So, can we do better?

Double hashing is a technique that minimizes the problem of clustered collisions by using a secondary hash function to find the next available slot.

## Double Hashing

Double hashing is an Open Addressing technique to address collisions in a hash table; hence, instead of using an auxiliary data structure to hold the collided keys, it leverages the already available free slots.

The probing function for Double Hashing is defined as

```
p(k, i) = (h1(k) + i * h2(k)) mod m
```

Thus, with every attempt we make to find an empty slot, we can leap by any distance in any direction, making all slots equally likely. A sample sequence for a particular key `k1` could be

- primary slot: `h1(k1)`, if that is occupied then
- attempt 1: `h1(k1) + h2(k1)`, if that is occupied then
- attempt 2: `h1(k1) + 2 * h2(k1)`, if that is occupied then
- attempt 3: `h1(k1) + 3 * h2(k1)`, and so on

Linear probing and quadratic traversals take a predictable leap to hunt for an empty slot, while double hashing probing leaps depend on the key and hence reduce the chances of clustering. So, different keys will have different leaps.

## Choosing a second hash function

The second hash function is super-critical, as it is aimed at resolving collisions effectively while ensuring minimal clustering. The second hash function should

1. never return 0
2. cycle through the entire table (with no particular order)
3. be fast to compute and almost feel like a random number generator

## Advantages of Double Hashing

1. Uniform spread upon collision
2. follows no specific offset pattern, the key purely depends on
3. least prone to the clustering problem

## Disadvantage of Double Hashing

Double hashing is not cache-friendly, as it requires us to hop across the hash table to hunt an empty slot. We may be at one extreme of the table and then move to the other one.