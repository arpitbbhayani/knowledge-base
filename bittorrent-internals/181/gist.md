Kademlia is a P2P Distributed Hash Table implementation that distributes the KV stores across nodes in a network and retrieves them without any central authority/database.

## Representation

Every node in the Kademlia network is identified by a unique 20-byte SHA-1 hash. The hash function is also used in reducing the key to be distributed to 20 byte unique id.

## Ownership

The node closest to the key is the one that owns the key and is responsible for holding it. But to define which is the closest one, we need to define a distance metric that could quantify the distance between two entities.

## Requirements from a distance metric

1. distance between the node to itself should be 0
2. distance between two nodes should be a positive number
3. d(a, b) + d(b, c) >= d(a, c)

any function that satisfies the above 3 can be used as a distance function.

## XOR as a Distance Metric

Kademlia uses XOR as a distance metric and defines it as a simple XOR between the ID of the entities

```
d(a, b) = a XOR b
```

XOR can be used as a distance metric because

1. a XOR a = 0
2. a XOR b > 0
3. d(a, b) + d(b, c) = a XOR b XOR b XOR c = a XOR c = d(a, c)

### Visualizing distance

XOR is not a usual distance we can measure, and hence it requires a special way to visualize. XOR tends to turn like bits to 0, so when we XOR two 160 bits numbers, the like bits will turn to 0.

Hence, the more common the prefix between the two 160-bit IDs, the smaller the resultant value, hence the shorter the distance. Thus we can visualize the distance between nodes by placing them in a complete binary tree.

In this complete binary tree, the nodes having shorter distances will be placed closer to each other. Instead of creating a tree with a depth of 160, the tree is constructed only to the point it minimally disambiguates the entity.

## Routing

Because there is no central entity, nodes must know how to route requests among themselves such that they always converge to the right node.

To ensure this, every node in the network keeps track of a few nodes in its routing table. These are not random, but very strategic.

Every node knows at least one node in each subtree that it is not part of. This means that the routing table may not have the address of the desired node, but it can lead us to one of the nodes present in its subtree.

By following a greedy approach, the nodes can route us, step-by-step, to the desired node. This is a classic Overlay network with its own routing.

### Updating routes

When a node receives a message from any other node, it makes an entry in its routing table thus ensuring the table is auto-updated without any explicit intervention.