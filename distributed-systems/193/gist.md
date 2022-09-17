Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

## Byzantine Agreement

The byzantine agreement is a problem of reaching a consensus even when one or many nodes or processes are malicious/corrupt.

## EIG Algorithm for Byzantine Agreement

The core idea of the Exponential Information Gathering Algorithm is to gather a large amount of information from the network and then apply some decision rules to reach a consensus.

## EIG Data Structure

EIG algorithms require an EIG Tree that is like a Trie and is constructed level by level. If there are `n` nodes in the network and the level of the tree is `k` then the leaf of the tree contains all k-length permutations of `n` nodes.

If a node `a` received a message from a path `b, c, d` then the incoming message (value) is stored along the path `b`, `c`, `d` at the node `a`.

Thus, at each level of the tree, the number of children of each node reduces by 1. The root of the tree is labeled EMPTY, and it has `n` children, say A, B, and C.

Each node in the next level will have 2 children. A will contain `AB` and `AC` while `B` will contain `BA` and `BC`, and `C` will contain `CA` and `CB`. Thus we see at level 2 the leaves contain all 6 2-length permutations of A, B, and C.

## The algorithm

The construction of the EIG Tree remains the same as it was in the Distributed Consensus and we assume that each node has constructed the EIG tree independently.

The algorithm is tolerant to `f` faulty process. When a process sends an ill-formed value the nodes participating in the consensus discard the value.

Ex: expected int, got string, discard.

### Decision Making

The processes propagate their values for `f + 1` rounds and each node builds its own EIG Tree. Once the EIG Tree is constructed, to make the decision, a node traverses the entire tree level by level starting from the leaves towards the root.

While traversing, the parent's value is the majority of its children's values. If there is no clear majority, then the parent sets to the default value.

The final consensus is the value that the root node of the EIG Tree decides. If any of the fault nodes send ill-formed values, the value will get absorbed along the tree because most of the nodes are honest and correct values outnumber the fault ones.

Hence, gathering exponential information is the key to resolving Byzantine agreements.