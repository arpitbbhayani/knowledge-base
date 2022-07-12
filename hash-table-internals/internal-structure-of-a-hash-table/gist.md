Hash Tables are implemented through simple arrays, but how?

Hash Tables are so powerful, that OOP based languages internally uses it to power Classes and sites members. Symbol tables that holds the variables mapped to memory location are also powered though hash tables.

They are designed to provide constant-time key-based insertion, updation, and lookups while being space efficient at all times.

## Core Ideas to construct Hash Tables

- convert application keys to wide-ranged (`INT32`) hash keys
- onovert hash keys to a smaller range

## Application Keys to Hash Keys

Hash Tables should support storing any object as key and to power that the keys are first hashed to a big integer range (provided by user) typically `INT32`. This hash key is then further used to decide how and where the KV pair would be stored in the data structure.

## Naive Implementation

A naive implementation of Hash Table would be to create an array of length INT32. To store the KV in it, we pass the key through the hash function spitting out an integer. We use this key and store the KV pair at this index in the array.

Although this would give us constant time insertion, updation, and lookups, but it is highly space in-efficient, as we would need to allocate at least `4` * `INT32` = `16GB` of ram to just hold this array, with most of the slots left empty.

### Hash Keys to Smaller Range

This step is designed and introduced to make our Hash Table space efficient. Instead of having a huge array of length `INT32`, we keep it proportional the the number of keys inserted. For example, if we inserted 4 keys then our holding array could be around 8 slots big.

To achieve this, we map the hash key into a small range (same as the length of the array) and place our key at that very index. This allows us to remain space-efficient while sporting fast and efficient insertions, updations, and lookups.

## Adding more keys

The small limited sized array will not be able to hold large number of keys and hence after a certain stage we would need a larger array to hold the data. This is done by resizing the holding array and is typically made 2x every time it is full enough.

Thus, this two step implementation allows to power near constant time insertions, updations, and lookups while remaining space efficient.