Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

Leader Election should work with any topology and hence we take a look into an algorithm called FloodMax.

## FloodMax Algorithm

The Flood Max Algorithm Flood Max works with a network that is arbitrarily connected. It assumes that every node is given a comparable UID that may be randomly allotted and every node knows the network's diameter.

### The algorithm

The Flood Max algorithm is designed to elect the node with the maximum UID as the new leader and the core idea is to flood the network with the Max UID until the value converges.

The election process happens synchronously, which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

The algorithm stops after completing rounds equal to the diameter of the network. In each round, every node

- sends the max UID it has seen to the connected nodes
- updates the max UID it has seen so far after receiving messages from its neighbors

After completing the `diameter` number of rounds, each node will have the max UID it has seen so far which will also be the global maximum; thus every node will know who is the leader of the network.

### Complexity Analysis

It takes O(diameter) number of rounds to elect the leader and in each round the number of messages exchanged is equal to the number of edges, hence O(|E|); hence communication complexity is O(diameter x |E|).

## Reducing Communication Complexity

To decrease the number of messages exchanged during the election, nodes can send the Max UID only when it changes. This would significantly reduce the messages exchanged across the network during leader elections.

Another optimization to reduce the communication is to NOT send the Max UID in the direction of the neighbor from which it was received.