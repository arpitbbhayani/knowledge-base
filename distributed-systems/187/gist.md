Breadth First Search is a critical algorithm in Distributed systems as it powers key features like

- Broadcast in minimum time
- Building topological understanding
- Topological stat like Diameter

In this gist, we discuss a synchronous approach which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

## Output of BFS

The output of this traversal is a Breadth-First Directed Spanning tree that covers all the nodes but a subset of edges. This output is important because we can use this spanning tree as a foundation for other applications and algorithms.

## The algorithm

The node `i0` initiates the BFS and it sends the `search` message to its neighbors. The nodes can either be marked or unmarked. If marked, they are part of the spanning tree already.

When an unmarked node receives the `search` message,

- it marks itself
- updates its parent to the node it received the `search` message from

In the next round, the nodes that received the message in the previous round participate, and send `search` messages to their neighbors, and the nodes receiving the messages do the needful.

Eventually, every node will be receiving the `search` message from some or the other node and will be part of the spanning tree.

## Complexity Analysis

Time taken to complete the BFS is proportional to the diameter of the network and the number of messages exchanged will be equal to the number of outgoing edges in the network.

## Conveying the children

With the current algorithm, every node knows its parent in the spanning tree but every node also needs to know which of its neighbors are its children in the spanning tree.

To achieve this, each node has to respond to the `search` message with a `parent/non-parent` message that tells the node if it was chosen to be the parent or not. This way, every node will know its parent and children in the spanning tree.

## Termination of BFS

The most important part of any distributed algorithm is its termination. How would the node know that BFS is done?

The approach we use is called Convergecast.

The idea is to respond to the search message only when it received responses from all its children. This ensures that the node initiating the BFS would receive the messages from its children only after all the nodes respond to their corresponding parents.

## Applications

After constructing the BFS Spanning Tree, we can use this constructed path to

- do an efficient broadcast on the network
- do distributed computation in the network