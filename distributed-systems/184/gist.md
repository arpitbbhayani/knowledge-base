Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## HS Algorithm

HS algorithm is synchronous which means every node proceeds with the algorithm in sync. A key highlight of this algorithm is that it has communication complexity i.e. number of messages exchanged, of O(n long).

The algorithm works with the following assumptions

- every node has a comparable unique ID
- the communication between nodes is bidirectional
- the nodes are virtually arranged in a circular ring
- the nodes know their immediate neighbors

### The flow

Every node participates in the election. To pitch itself, it creates a message with its UID and sends it to its immediate neighbors in both directions.

To reduce the number of messages required to elect the new leader, the nodes who knows their UID is smaller, they quickly drop out of the election.

The election proceeds in phases. In each phase `i`, the nodes participating in the election send their candidature to a hop distance of 2^i and wait for it to come back.

Every node along the path, upon receiving the message,

- if the incoming is greater than its own, it forwards it
- if the incoming is lesser than its own, it discards

If the node, receives its UID as an incoming message from both directions then it knows that it has the maximum UID in the 2^i neighborhood. With each phase, the hop distance increases exponentially.

With each phase, the nodes with smaller UIDs start to drop off from the election while still acting as the transmitter of the messages. After certain phases, there will be only one node remaining and that becomes the new leader.

### Halting

The leader election in the HS algorithm halts when the node receives its probe message and thus it knows that it is the only one left and hence declares itself as the new leader.

The new leader creates the announcement message and relays it across the ring announcing itself as the new leader all the nodes locally update it and the election is concluded.

### Key Implementation Detail

The message sent across during the election contains `<uid, hops, direction>`. It helps the node know

- the number of hops the message has taken
- stop forwarding when the hop count becomes 0
- in which direction to reply