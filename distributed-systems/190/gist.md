Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

But, reaching a consensus becomes impossible when we cannot guarantee message delivery.

## Two Generals' Problem

Say, there are two generals - A and B - and they want to attack the enemy from two different directions. The only way to conquer the enemy is when both generals attack simultaneously. If only one attacks, then the enemy wins.

The generals communicate via foot soldiers. These foot soldiers can be captured by the enemy and hence the message that generals wanted to send to each other can be lost. So, how would generals coordinate the attack?

### When no messages are lost?

If the communication channel is reliable, then the generals all send each other messages to agree to attack and everyone responds/ack to everyone else, thus coordinating the attack.


## Real World Analogy

Committing to a distributed database. The commit should succeed when all the nodes of the database agree to commit. If anyone cannot commit then the commit cannot go through.

## When messages are lost

When general A sent a message to general B, what if B's response got lost? then general A would not know if it should attack or not.

Also, since B did not receive an ack from A, then it cannot decide if it should attack or not either.

This is where we see both generals will keep on waiting for an acknowledgment of an acknowledgment, purely because the communication channel is unreliable.

This is the class Two Generals' Problem where it is impossible to reach a consensus when the underlying communication channel is unreliable.

## How should the generals decide?

Generals, instead of sending just a foot soldier, can send multiple foot soldiers increasing the probability that at least one of them would go through.

This is like we are flooding an unreliable network to get our message delivered.

## But how do we do this in the Real World?

In the real world, hence we do not assume a completely unreliable network. Instead, we assume a certain fraction of messages will be lost - eg: 1 in 2. Hence to overcompensate we send 2 messages instead of one.