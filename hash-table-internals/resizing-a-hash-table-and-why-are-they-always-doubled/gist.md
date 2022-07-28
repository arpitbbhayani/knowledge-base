To maintain a consistent performance, hash table has to be resized - be it growing or shrinking. The trigger to resize depends on the load factor which is defined as the the ratio of the number of keys that the hash table holds to the total number of slots.

## When should we resize?

Hash Table is resized when the load factor hits a certain threshold. If we get too aggressive or too lenient, we would not be able to get the optimal efficiency. Hence we have to find a sweet spot.

We typically grow the hash table when the load factor hits 0.5 and shrink when we hit 0.125.

## Why do we always double?

We have heard and seen so many times, that when a Hash Table is required to grow, we always double the underlying array; but why? can we not just increase it by 1 every time we are trying to insert?

### Resizing by 1 everytime

Let's take an example: say, we grow the array by 1 every time we insert an element in the Hash Table. Let's compute the time it requires to fill `n` elements.

Inserting the 1st element is: allocating array of size 1, and inserting 1 element; so in all O(1) operation.

Inserting the 2nd element is: allocating array of size 2, copying 1 element from old array, and then inserting the 2nd element; so in all O(2) operations.

Hence inserting the nth element is: allocating array of size n, copying n-1 elements from old array, and then inserting the nth element; so in all O(n) operations.

Total operations to to insert `n` elements = 1 + 2 + ... + n = (n(n-1))/2 which is O(n^2).

### Doubling Everytime

If we double every time, inserting `n` elements requires O(n) time, as are spacing out an expensive resize operation. We would be inserting n/2 elements before resizing the array to 2n.

Note: For a detailed amortized analysis, please refer to the video attached here where I have explained the reasoning in depth.

## Why is array always power of 2?

For a power of 2, the MOD and the bitwise AND spits out the same result and given that the bitwise AND is magnitude faster than the MOD, we get the best performance out of our Hash Tables when we use AND

```
(i % 2^k) == (i & (2^k) - 1)
```

This is why length of the underlying array is always a power of 2, making our most-frequent operation efficient.

## Shrinking the Hash Table

To ensure we are not wasting space, we trigger the shrink when we not utilizing the underlying array enough. While triggering a shrink we also need to ensure that we are not aggressive enough that we have to grow immediately after the shrink.

Hence, we shrink the hash table when the load factor hits 1/8 i.e. in a table of length 64, if we are only holding 8 keys, we trigger a shrink and that reduces the the length to 32.

Note: To understand why we do it at load factor = 1/8, please refer to the video.