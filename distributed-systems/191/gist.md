Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

Reaching a consensus

- is impossible when the network is unreliable
- is simple when there are no network/process failures
- is tricky when we have to deal with process failures

## FloodSet Algorithm

The core idea of the FloodSet algorithm is to keep track of all the values seen so far and use some decision rule such that all nodes choose the same value.

Every node maintains a set `W` to hold all the values seen so far. If we assume at max `f` nodes would fail then the FloodSet algorithm runs for `f + 1` rounds, giving chances for processes to fail.

Every node starts with `W = {v}`, its own value. In each round, every node broadcasts `W` in the network. When a node receives the `W` from other nodes it updates its `W` by doing a set union.

After the `f + 1` rounds, every node will have the same `W` that holds all possible values of the network participating in the transaction.

### Decision Making

The decision-making is decentralized. If `W` contains just one value then the node converges to that value. If it contains more than one value, the node defaults to the last value.

This decision-making is use-case specific, so defaulting to the old value can mean that the transaction is aborted and the node is reverting to the old value.

### Alternative Decision Strategy

Depending on the usecase, we may choose another decision strategy like picking the smallest value or the largest value or the oldest value, or the newest value.

So long as we have a total ordering of the values, we can define our own decision strategy.