Collisions are inevitable in Hash Tables, and a common way of handling them is through Chaining using Linked List. But can we use some other data structure?

Collisions are inevitable in Hash Tables as we are mapping a large range of application keys on a smaller range of array slots. So, there are chances that the hash function spits out the same value for two different application keys.

Because Hash Tables cannot be lossy, we need a way to handle these collisions and allow storing of multiple keys that are hashed to the same slot. A way to achieve this is Chaining and it is very commonly implemented through a Linked List.

## Data Structures

To accommodate this, the Hash Tables are now implemented as an array of Linked List where all the keys that collide are placed.

### Adding a Key

While adding a key to the hash table, we first pass it through the hash function and get the slot index. We then create a node holding the key and add it to the linked list.

We can add the new node at one of the 3 places

- always at the head of the list - O(1)
- always at the tail of the list - O(1)
- in the middle of the list while maintaining a sort order - O(p)

### Deleting a Key

To delete a key, we first pass it through the hash function and get the slot index. We then iterate through the linked list present at the slot, element by element, and locate our key of interest.

While iterating, we keep track of the pointer to the previous node so that once we reach the node to be deleted, we adjust the pointers and free up the node.

### Key Lookup

Key lookups are similar to delete operations. We first pass the key through the hash function to get the slot index. We then iterate through the list present at the slot and locate our key. The operation requires us to iterate the list iteratively.

## Other Data structures for chaining

Linked List is not the only data structure that we have to use to chain the collided keys. Depending on the use case, access pattern, and constraint we can pick a data structure that suits us.

For example, if our array is small and we cannot resize it then we may end up having a large number of collisions. If we are trying to read, then iterating over this list will reduce the throughput as it is a linear scan.

To optimally perform a key lookup, when the collisions are high, we can use a self-balancing search tree, like BST or Red-Black. This way, we get an optimal lookup performance on keys hashed to the same slot.