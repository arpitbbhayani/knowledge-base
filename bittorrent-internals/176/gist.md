BitTorrent is a peer-to-peer protocol that makes the distribution of large files easier, faster, and more efficient.

## Need for BitTorrent

To download a file client makes a request to the server, and the server after processing the request responds with the file.

Although the download is simple, it suffers from

1. server's bandwidth is limited and more clients will overwhelm
2. speed of transfer is limited by the upload capacity of the sender

Is there a way where we can download the file faster? without overwhelming the server? P2P networks like BitTorrent solve this problem beautifully.

## P2P Network

A P2P network is a network of nodes called peers where each peer is equal and can initiate communication with any other peer. Such a network has no SPoF and hence even if we remove a node, the network continues to function.

There may be a central entity in the network to hold meta information but the core work is still done by the peers. Such a network is called a Hybrid P2P network.

## Core Idea of BitTorrent

BitTorrent is built on the principle of not downloading files from just one machine, instead, it encourages us to download pieces of the file concurrently from multiple machines.

### Advantages

- faster download
- upload load gets distributed across
- better utilization of download capacity of a machine
- even when a large number of nodes join the network, the load is increased only by a small margin

### Simplified Idea

Split the file into small pieces and distribute it across the network. Instead of downloading the complete file from one server, download the pieces of the files from different machines, concurrently.

## Nomenclature

### Pieces and Blocks

The film is split into equal-sized pieces, and each piece is further split into blocks. In one transfer a block is transferred but a node can only serve after it has the entire piece.

### Peer Set

Each peer maintains a list of peers to whom it can reach and download the pieces. Out of all the peers in the peer set, a node can only send data to a subset and this subset of peers is called Active Peer Set.

### Seeders and Leechers

A node having the complete file is a seeder while a node currently downloading the file is a leecher. A leecher can download the pieces from seeders or other leechers.

## Popular friendly

The new and popular files will have a lot of seeders and hence a new node joining the cluster will be able to download them much faster. If the file is old and unpopular, there will be few seeders and hence we would see a slower download.

## Applications of BitTorrent

- distributing OS images across the network is faster
- sending patches to machines quickly
- powering deployments across a massive cluster of machines