The BitTorrent Architecture BitTorrent architecture consists of the following entities

- Torrent File
- Tracker
- Leecher
- Seeders

Each torrent is independent and it holds information about one or many files that need to be distributed. To download a specific file, we need to hunt its torrent file from any torrent search engine.

## Pieces

The original file is split into equal size pieces and the SHA-1 of each piece is put into the `.torrent` file. The hash is then used by the peers to download the corresponding piece and once all the pieces are downloaded, they are merged to re-generate the file.

## Tracker

Tracker is the only central entity and it holds the information about all the peers participating in the torrent network. It is a simple HTTP server that responds to the queries of the peers and stores status information coming in from the peers.

Each torrent file holds a Tracker URL that helps the peers locate and talk to the tracker to participate in the torrent. The tracker keeps track of

- peers who hold the pieces of the file
- peers who are downloading
- peers who need help to find other peers

Although the tracker keeps track of a lot of information, it does not download or participate in the download of the actual content of the file; it simply holds the meta information.

## Leecher

Leecher is any peer in the network that is downloading the pieces and is awaiting the completion of the file. Leecher talks to the tracker to get the list of 50 peers and then talks to them to get the desired pieces.

The leechers also help other leechers by sharing the pieces they have, thus quickly distributing the file across the network.

## Seeder

Seeder is a peer in the network that has all the pieces of the file and does not need to download anything. So, if any leecher needs any piece that is not available with any other leecher, it can obtain from the seeder.

A leecher, after completing the download of the entire file, becomes the seeder and continues to participate in the network.