In a BitTorrent network, the file is split into pieces and then distributed across the network. A piece is a unit of transmission and when a peer has all the pieces it concatenates them and re-creates the entire file.

## Importance of Piece Selection strategy

Having a piece selection strategy is important because what if every single peer starts with the first piece first, this would increase the load on the peers/seeders that have them; thus reducing the speed of distribution.

What if before anyone could download the last few pieces, the seeder (having all the pieces) leave the network? none of the lechers would be able to complete their download.

## Rarest-first Piece Selection

Core idea: prioritize the download of the piece that is the rarest in the network.

### Advantages

### Spreading the seed

Rarest-first piece selection strategy ensures only "new" pieces (that are with no other leechers) are downloaded from the seeder. We get a quick distribution of pieces in the network and a reduced load on the seeder.

### Increases download speed

Since more peers have a variety of pieces, they can quickly trade among themselves and complete downloads faster.

### Enabling upload

When a peer has a rare piece, every other peer would be interested in downloading it. Because of reciprocation, it would be frequently unchoked from others, getting a better download speed.

### Preventing rarer missing piece

By prioritizing the download of the rarest pieces, we ensure that rare pieces do not go missing from the network even when the seeder leaves.

## How to compute the rarest piece?

There are two ways to know which pieces the peers have

1. `Have` messages: a peer in the network broadcasts the pieces it has
2. `Bitfield` message: during the initial handshake, a peer sends a Bitfield message that contains the pieces that it holds.

Every peer maintains the piece availability across its peer set and uses it to compute the rarest piece.

## Random First Policy

When a peer joins a network, to proactively participate, it would need to get the first piece as soon as possible, and hence instead of picking the rarest first, it goes for random pieces.

## Strict Priority Policy

A file is split into pieces and a piece is split into blocks. Blocks are what get transferred. Hence, when a block of a piece is fetched, we prioritize downloading all the blocks of the same piece before moving on to the new one.

## End Game Mode

Downloading the last few pieces may take time and hence a peer. In the end game mode, a peer sends a request to all the peers for every block that is remaining.

The peers respond with the block and this completes the download faster.