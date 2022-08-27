Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## LCR Algorithm

LCR Algorithm for leader election is the simplest and the easiest to understand and implement, and its variant can be seen in action in a bunch of distributed systems.

The LCR algorithm expects the network to have the following properties

### Unique ID

Every node in the network has a unique identification - UID - that can be compared with other UIDs.

### Virtual Circular Ring

LCR also assumes that the nodes in the network are virtually arranged in a circular ring, and each node knows the node to its right in the ring.

Although we want a circular ring, the nodes may be physically connected to other nodes through any topology. The ring mandate is purely virtual and can be maintained only for powering elections.

### The Algorithm

In the election, every node participates to be the new leader. To participate, it creates a message having its UID and sends it to its neighbor.

When a node receives a UID, it compares the incoming UID with its own, and

- if the incoming is greater than its own, it forwards it
- if the incoming is lesser than its own, it discards
- if the incoming UID == its own, it declares itself as the new leader

When a node receives its UID as an incoming message, it implies that the message survived the entire iteration leading to the assertion that the node has the highest UID in the network; and hence can become the new leader.

The new leader is then announced through another message passed across the ring.

### Halting the algorithm

Halting is one of the most important aspects of any distributed algorithm, as it can get tricky to know when to stop.

LCR algorithm stops when the new leader initiates the message and announces itself. To announce, it initiates the `HALT` message and sends it across.

The node receiving the `HALT` message understands that the new leader has been elected and needs to stop participating in the election. The node updates its local state with this information and forwards the message to the next node.

## Complexity

Each node participates in the election and sends messages across the entire ring. Every node could potentially receive the message from every other node; the communication complexity, the number of messages shared, is thus O(n^2).