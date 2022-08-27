Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## TimeSlice Algorithm

TimeSlice algorithm for leader election is highly impractical, unbounded, yet an interesting algorithm to understand.

The algorithm assumes

- each node has a UID that is a positive integer
- the nodes are arranged in a virtual ring
- each node knows its immediate neighbor to the right
- each node knows the total number of nodes `n` in the network

### The flow

The election proceeds in phases 1, 2, 3, and so on. Each phase consists of `n` rounds. Because the algorithm is synchronous, each node knows when the algorithm is proceeding with rounds and phases.

In phase `i`, nodes can only forward the message having the candidature of UID `i`. Hence, in phase `3`, a node will forward the message to the next node, only when it is having the candidature of UID `3`.

## The flow

In phase 1, the node with UID 1 will send the message with its candidature across to the next node in the ring. If no such node exists, then no message is sent.

Thus, for `n` rounds within phase 1 there is void silence in the network. Then beings the phase 2.

Hence, we see that the messages will be sent across the ring only when the phase `i` beings where `i` is the smallest UID in the network. For all `(i - i) * n` rounds, there will be void silence in the network.

When phase `i` begins the node with UID `i` will know that it is the new leader and it initiates the message and sends it to the next neighbor. For `n` successive rounds, the message is sent across the network and thus all `n` nodes know about the new leader `i`.

## Complexity Analysis

The algorithm thus elects the node with the minimum UID as the new leader in just `O(n)` messages but takes time proportional to the `O(n*i)`.

If the minimum UID is a large integer, then the algorithm will take a longer time to elect the leader, and hence it is unbounded on the number of nodes in the network.