The split-brain problem in Distributed Systems is not theoretical. GitHub had an outage because their Zookeeper cluster ended up having two leaders, leading to writes to Kafka failing.

Zookeeper is an essential component for Kafka as the clients connect to get information about the brokers and cluster internally using it to manage its state.

## What happened?

During scheduled maintenance the Zookeeper nodes were getting upgraded/patched and during this time, many new nodes were added "too quickly" to the zookeeper cluster.

With a lot of new nodes added "too quickly", they were unable to self-discover or understand the topology and the way the bootstrap code of Zookeeper is written, they thought the cluster was leaderless. This made them trigger a Leader Election.

Given that a lot of new nodes were added, they formed the majority and elected a new leader. These nodes formed a logical second cluster operating independently. Thus the cluster is now having a split-leadership problem.

## Broker Connected

One of the Kafka broker (node) connected to the second cluster and found that no other nodes are present (because second zookeeper cluster had no entries) and hence elected itself as the controller.

When the Kafka clients (producers) were trying to connect to the Kafka cluster they got conflicting information which led to the 10% of writes failing.

If the number of brokers connecting to the new cluster were more, then it could have led to even data consistency issues. But because only one node connected, the impact was minimal.

## Recovery

The zookeeper cluster would have auto-healed but it would have taken a long time to converge, and hence a quick way to fix this is to manually update the zookeeper entries and configure it to have a single leader.

To keep things clean, the nodes that were part of second zookeeper cluster could have been deleted as well.

## Ensuring zero data loss

Even though 10% of write requests failed, why did it not lead to a data loss? the secret is Dead Letter Queue.

It is a very standard architectural pattern that ensures zero data loss even when the message broker (queue) crashes. The idea is to have a secondary queuing system that you can push messages to if the write on the primary fails.

All the messages that client tried to write to Kafka failed, but they were persisted in DLQ which they processed later.

## Key Learnings

- Make consumers idempotent
- Automate cluster provisioning
- Have a DLQ for all critical queueing systems
- Have retries with exponential back-offs on clients