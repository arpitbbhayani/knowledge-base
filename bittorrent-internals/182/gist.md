P2P networks are prone to exploitation as there is no central authority to keep track of the activity. BitTorrent is not different, and it is easy for Free Riders to exploit it.

## Overview

The file is broken into pieces and peers download them piece-by-piece. Seeders are the peers that have the entire file and is uploading the pieces. Leechers are the nodes downloading the file and they talk to seeders and other leechers to complete the download.

## Pretend to be a new peer

When a peer joins the network, it talks to the tracker and the tracker sends a list of 50 peers it can talk to. Hence, by pretending to be the new peer, we may collect information about thousands of peers participating in the network.

Having information about a large number of peers in the network enables us to download the pieces faster as we can establish connections with many of them and initiate the download.

## Being greedy with piece selection


Peers in a BitTorrent network are supposed to follow the rarest-first policy through it prioritizes the download of the piece that is rarest in the work, but we choose to ignore that.

We can be greedy with the piece selection and download the pieces without any strategy and we grab whichever piece we get from our peers.

## Pretend to upload

Periodically, peers in a BitTorrent network inform the tracker about their download and upload statistics. There is no way for the tracker to check if the peer has indeed done the mentioned work.

Hence, we share false bloated numbers with the tracker, making the tracker think we are a "good" peer that is uploading a lot in the network. With this, the tracker will give us a boost and share our IP with a new peer.

### Uploading dummy data

Instead of uploading the actual piece, we can also choose to upload dummy data. Although this is not free riding as we are uploading some information because it is not genuine, it is counted as free riding.

The clients upon receiving any piece do an MD5 verification and our dummy data will be caught in that. Peers may choose to block us if they see repetitive failures. Hence, this is risky but we can get a boost in the download speed due to reciprocation.