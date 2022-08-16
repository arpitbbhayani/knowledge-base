In a P2P network, every peer would want to download the file as fast as possible but this would lead to a skewed load on some peers. BitTorrent addresses this using a reciprocation algorithm called Choke.

The choke algorithm ensures

- maximum download speed to genuine peers
- minimal network abuse by free riders

## Free Riders

Free riders are the peers in the network that exist only to download the files but they never upload anything to any peer. Hence they are consuming the network bandwidth without contributing back.

The Choke algorithm is hence designed in a way that penalizes such free riders.

## Choking and Interested Peers

Choking a temporary refusal to upload. We say that peer A has choked peer B when A refuses to upload/send data to B, but it still allows A to get data from B.

When peer A wants to allow peer B to download the piece, we say that peer B is unchoked by peer A. We say that peer A is interested in peer B when it wants a piece of the file that peer B has.

## How to find peers to unchoke?

If a peer unchokes every other peer, then everyone would want to download the file from it, and hence the peer would be overwhelmed. Thus, a peer always prioritizes unchoking a peer that offers the best download speed.

This prioritization is based on the principle of reciprocity wherein a peer will send data to the peers from whom it gets the data faster. This encourages peers to let others download from it and prevent free riders, who never upload, from abusing the network.

## Choke algorithm for Leecher

Every 10 seconds, a leecher A orders the interested peers by their download rate to A, and the fastest 3 are unchoked. This is called regular unchoke. Unchoking is temporary, and after some time, an unchoked peer gets choked again by A.

### Optimistic unchoke

Every 30 seconds, one additional interested peer is optimistically unchoked at random without any reciprocation. This

- bootstraps new peers who do not have anything to share
- provides new peers with some pieces to participate in the network
- evaluates download capacity of newly joined peers

## Choke algorithm for Seeder

If a peer is a Seeder, it unchokes the peers that were more recently unchoked. This ensures that free riders are not unchoked by the seeders and they rely on optimistic unchoke by leechers.

If the two peers have the same last unchoke time, the one with the higher download rate is given priority.

For the first 20 seconds, seeder

- unchokes 3 peers as per the above sorting criteria
- unchokes one peer at random to promote randomness

For the next 10 seconds, it unchokes the first 4 peers ordered by the sorting criteria ensuring minimal abuse.