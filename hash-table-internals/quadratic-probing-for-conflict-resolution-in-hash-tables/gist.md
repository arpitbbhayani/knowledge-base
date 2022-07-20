Linear probing is a popular way to handle Hash Table collisions, but is that the only way? Definitely not.

## Challenges with linear Probing

Linear Probing suffers from one significant challenge and that is clustered collision. With poor hash function, it is very much possible that some slots are preferred more over others, and upon collision, they are placed next to each other.

Hence, we would see clusters of collided keys forming across the entire hash table, and this is called Clustered Collision. Linear Probing suffers from this the most.

## Quadratic Probing

Quadratic Probing determines the next slots as per an arbitrary probing function

```
p(k, i) = h(k) + c1 * i + c2 * i^2
```

For attempt 0, we get the primary slot `h(k)` and post that for each attempt we move quadratically through the hash table to hunt for the next available slot.

Because of the quadratic jump, we do not form clustered collisions, instead, we cover a good chunk of the hash table. A simple quadratic sequence would be

```
h(k) + 1
h(k) + 4
h(k) + 9
h(k) + 16
.
.
```

where `h(k)` is the primary slot we got by passing the key through the hash function and 1, 4, 9, and 16 are the quadratic offsets.

## Properties of Quadratic Probing

### Reducing clustered collisions

Quadratic Probing reduces the clustered collisions by distributing collided slots quadratically across the hash table and utilizing the entire hash table space.

### Good Locality of Reference

Quadratic Probing has a good locality of reference. When we access a particular slot of the hash table we are also bringing in neighboring slots to the CPU cache. Upon collisions when we access a few next quadratic slots we need not fetch it from the RAM.

The locality of reference is not as high as Linear Probing but it is decent enough when we observe fewer collisions per slot.