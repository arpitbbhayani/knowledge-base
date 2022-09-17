Say, we have a distributed database with three nodes, and we want our "commit" to succeed when it is successful in all three nodes otherwise we "abort".

This is a classic Distributed Transaction.

Assumptions:

- no messages are lost
- processes can fail in the middle of the transaction
- every node knows about every other node in the network

## Two-Phase Commit

Say have the transaction, and N processes are participating. One of the `N` processes becomes the coordinator and it coordinates until the end of the protocol.

### Phase 1

All the nodes send if they can `commit` or `abort` to the coordinator process. If a process does not send any information, the coordinator will mark it as `abort`.

At the end of phase 1, the coordinator will have the local decisions of all the nodes. The coordinator decides `commit` if all the nodes can `commit`, otherwise the decision is `abort`.

### Phase 2

Process A broadcasts its decision to all the nodes in the network, and thus the entire network either commits or aborts; thus completing the transaction.

## Failure Scenarios

If the coordinator fails before the start of phase 1, then since the consensus did not even start, all the nodes can safely abort.

If the coordinator fails after initiating phase 1, some of the nodes might have sent their local decision and would be waiting to hear back the final decision. These nodes would remain blocked.

If a participant crashes before sending its local decision to the coordinator, then the coordinator keeps on waiting for the local decision.

If the coordinator and one participant crash in phase 2 without other participants knowing anything about the decision then the new coordinator that comes up would have no idea about the decision.

No one could proceed, because the new coordinator does not know if the crashed node was committed or aborted.

The Two-Phase Commit looks super-simple but it has a major flaw in the failure scenarios, and hence distributed systems take even finer steps to remediate and reach a consensus more robustly.