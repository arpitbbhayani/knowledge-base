Introduction to BitTorrent and the problem it beautifully solves
===


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
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Introduction to BitTorrent and the problem it beautifully solves](https://i.ytimg.com/vi/v7cR0ZolaUA/mqdefault.jpg)](https://www.youtube.com/watch?v=v7cR0ZolaUA)

BitTorrent is super popular when it comes to sharing and distributing large files over the network. But what is the engineering behind it? In this series, we will dive deep into BitTorrent, and understand various algorithms that power it. Along the way, we would also try to write our own torrent client to get a deeper understanding.

In this 1st video of this series, we take a look at what are peer-to-peer networks, what is bit torrent, the core idea behind it, and how it makes downloads super-fast, and conclude with some terminologies that would acquaint us to do a deep dive later.

Outline:

00:00 Agenda
02:43 Classic Download Flow
04:50 P2P Networks
07:19 Core Idea of BitTorrent
11:15 Nomenclature and Terminologies
16:03 BitTorrent is popular-friendly
16:56 Applications of BitTorrent

GitHub Repository: https://github.com/relogX/retorrent

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1hNOYmkFBb1ia0Myc6afrTB2kfwDyvQAE/view?usp=sharing)
 - Listen to this on the go on [Spotify](https://open.spotify.com/show/7qMoamm2iZQrsPVm6IQLoD)

# Arpit's System Design Masterclass

> A masterclass that helps you become great at designing _scalable_, _fault-tolerant_, and _highly available_ systems.

## The Program

This is a prime and intermediate-level cohort-based course aimed at providing an exclusive and crisp learning experience. The program will cover most of the topics under System Design and Software Architecture including but not limited to - _Architecting Social Networks_, _Building Storage Engines_ and, _Designing High Throughput Systems_.

The program will have a blend of Live Classes happening on Weekends, and 1:1 Mentorship sessions. The program is designed to be intense and crisp to accelerate the overall learning. We tackle every system from the [First Principles](https://en.wikipedia.org/wiki/First_principle) and build the solid foundation to architect any system in the future.


## Highlights

 - The course has been taken up by __500+__ people, spanning __9__ countries.
 - People from companies like Tesla, Amazon, Microsoft, Google, Yelp, Github, Flipkart, Practo, Grab, PayPal, and many more, have taken up this course.


## Hi, I'm Arpit Bhayani 👋

<img width="256px" src="https://arpitbhayani.me/static/img/arpit.jpg" />

In my last **~10** years of experience, I have worked at **D. E. Shaw**, **Practo**, **Amazon**, and **Unacademy**; and have built systems, services, and platforms that scaled to billions.

Post my masters in CSE from **IIIT Hyderabad** I joined D. E. Shaw for a short stint of 2 months, before moving to Practo and working there as a **Platform Engineer**, building and owning close to 8 different microservices. Post Practo I worked at Amazon on their primary mission-critical E-Commerce Database and built **Data Pipelines** that cold tiered the stale data.

After quitting Amazon in 2018, I joined Unacademy as their first **Technical Architect** and there I designed, built, managed, and scaled services like _Search_, _Notification_, _Logging_, _Deployment Engine_, and many more. I have now transitioned into the role of a Sr. Engineering Manager, leading the Site Reliability vertical.

I also run a YouTube channel [#AsliEngineering](https://www.youtube.com/c/ArpitBhayani) where I post 3 videos every week spanning topics like System Design, Distributed Systems, Microservices, and any interesting CS concept in general.

You can find details about upcoming cohort 👇‍ Hope to see you soon there.

<center>
<a target="_blank" href="https://arpitbhayani.me/masterclass">
<img src="https://user-images.githubusercontent.com/4745789/137859181-d4499cf4-ce65-4466-8b88-a078ece0f081.PNG" width="300px" />
</a>
</center>