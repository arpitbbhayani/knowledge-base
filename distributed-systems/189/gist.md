Minimum Spanning Trees are super-critical in distributed systems, and they form the crux of building efficient broadcasting systems.

## Spanning Tree

A tree that covers all the nodes through selective edges. MST is the Spanning Tree such that the summation of the weights of the covered edges is minimum.

The weights on the edges can quantify communication latency, congestion, cost of the communication, or even distance.

## Distributed Setup

In a distributed setup, every node does not have information about the entire topology, instead, it holds the information about just itself, the nodes connected to it, and the incident edges.

## GHS Algorithm

The algorithm operates on a "level" and each level is a collection of a bunch of spanning trees. The core idea of this algorithm is to continue grouping spanning trees into a bigger ones until we are left with one huge spanning tree.

Level 0 consists of all the nodes and no edges and if we have `n` nodes, there will be `n` spanning trees (components) in the forest.

Every spanning tree would know

- total number of nodes n
- incident edges to it
- its UID of the leader of its component

Each node within the component sends a search message to the component to get MWOE (Minimum Weight Outgoing Edge).

Each node upon receiving the message searches for an outgoing edge that is connecting to the node that is not part of the component. Of all such edges, the node picks the edge with the min weight and sends it across to the leader of the component.

### How to test if another node is in another component?

Every node knows its leader UID and hence a node sends a `test` message to its immediate neighbors and they revert back with their leader UIDs. Comparing this UID with its own, the node knows if the other node is part of the same component or not.

### Merging the components

Now that the leader has the all minimum outgoing edges from the peripheral nodes, it can find a global minimum outgoing edge that is going out of its component.

The leader of the component now talks to the nodes connected over MWOE and tells them to mark itself in under this component. The new leader of the merged component is one of the two nodes with a higher UID connected over the MWOE.

### Level by Level

The spanning tree is constructed level by level. It starts with all nodes being their own Spanning Tree. Then Two Level 0 nodes merge to form Level 1 nodes, and then Level 2 and so on.

### Termination of the algorithm

The algorithm will terminate when the leader of the component is trying to find MWOE but none of the nodes sends it any information given they are all part of the same tree.