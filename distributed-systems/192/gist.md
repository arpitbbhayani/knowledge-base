Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

Reaching a consensus

- is impossible when the network is unreliable
- is simple when there are no network/process failures
- is tricky when we have to deal with process failures

## EIG Algorithm

The core idea of the Exponential Information Gathering Algorithm is to gather a large amount of information from the network and then apply some decision rules to reach a consensus.

## EIG Data Structure

EIG algorithms require an EIG Tree that is like a Trie and is constructed level by level. If there are `n` nodes in the network and the level of the tree is `k` then the leaf of the tree contains all k-length permutations of `n` nodes.

If a node `a` received a message from a path `b, c, d` then the incoming message (value) is stored along the path `b`, `c`, `d` at the node `a`.

Thus, at each level of the tree, the number of children of each node reduces by 1. The root of the tree is labeled EMPTY, and it has `n` children, say A, B, and C.

Each node in the next level will have 2 children. A will contain `AB` and `AC` while `B` will contain `BA` and `BC`, and `C` will contain `CA` and `CB`. Thus we see at level 2 the leaves contain all 6 2-length permutations of A, B, and C.

## Algorithm

We assume at max `f` nodes would fail and hence the algorithm runs for `f + 1` rounds. In each round, a new level of EIG Tree is constructed. Each node independently constructs the level but every single node will have formed the exact same EIG Tree.

### Round 1

Every process `i`, sends its value to the entire network including itself. Upon receiving the value `v` from `j`, the nodes update their own trees and add nodes `tree[j] = v`.

At the end of round 1, every node will have an EIG tree of depth 1.

### Round > 2

Every process `i`, sends all pairs `(x, v)` from the `k - 1` level in the network where `i` is not in `x`. This would lead to the construction of the permutation tree.

After the `f + 1` rounds, each node will have the exact same copy of the EIG Tree of depth `f + 2`.

### Decision Rule

The algorithm stops after the `f + 1` rounds, and each node simply traverses through the entire EIG Tree to find all distinct values it holds.

If the number of values is 1, the node decides that as the final value. If the distinct values are many, then the node may choose the default value.

This decision-making is use-case specific, so defaulting to the old value can mean that the transaction is aborted and the node is reverting to the old value.

### Alternative Decision Strategy

Depending on the usecase, we may choose another decision strategy like picking the smallest value or the largest value or the oldest value, or the newest value.

So long as we have a total ordering of the values, we can define our own decision strategy.