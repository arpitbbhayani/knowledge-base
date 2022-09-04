Determining the shortest path in a distributed system is an important problem to address and it finds its application across multiple use cases like

- delivering messages to a node efficiently
- efficient routing of messages

A key point to consider here is the fact that "shortest" is not only about the distance, but it can also be about the congestion, time, cost of communication lines, cable infra, and much more.

## Problem statement

In a distributed network, where nodes are connected via paths/edges having some weight assigned, find the shortest path from a specific source to all the nodes

## Bellman-Ford Algorithm in Distributed System

In this gist, we discuss a synchronous approach which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

Because it is a distributed network no node knows the entire topology and weights. They just know

- total number of nodes
- their immediate neighbors, and
- the weights of the edges incident on it.

Every node keeps track of `dist` which holds the shortest distance to it from the source `i0`. Initially, `dist` at `i0` will be `0` and `dist` at all other nodes will be `inf`.

At every round, all the nodes will send their `dist` across all of their outgoing edges to their neighboring nodes. Every node `i` upon receiving an incoming `dist` from its immediate neighbor `j` compares

- its own `dist`
- incoming `dist` + `weight(i, j)`

after comparing, if the incoming distance plus the weight of the connecting edge is smaller than its own `dist` it means that the distance from `i0` to the current node could be shorter and hence, the node updates the `parent` suggesting that the shortest path from `i0` to `i` goes through `j`.

After `n - 1` rounds, the `dist` at every node will contain the shortest distance to it from source `i0`, and the `parent` will contain one of its immediate neighbors that lies in the shortest path.

## Complexity Analysis

We require `n - 1` rounds to complete the algorithm, the time complexity of Bellman-Ford Shortest Path in Distributed System is `O(n)`. At every round, every node sends `dist` message across all of its edges to its immediate neighbors, the communication complexity becomes `O(n x |E|)`.