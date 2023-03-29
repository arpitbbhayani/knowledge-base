The Piece Selection algorithm that makes BitTorrent fault tolerant
===


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
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![The Piece Selection algorithm that makes BitTorrent fault tolerant](https://i.ytimg.com/vi/QSeex0YxReY/mqdefault.jpg)](https://www.youtube.com/watch?v=QSeex0YxReY)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Performance of the BitTorrent network relies heavily on the order in which the pieces are requested by the peers.

In this 5th video of the BitTorrent Internals series, we take a look at the piece selection algorithm BitTorrent uses and learn how it makes the network fault-tolerant while ensuring a fast download rate across the network.

Outline:

00:00 Agenda
02:24 Why we need a Piece Selection algorithm
05:13 Goal of Piece Selection algorithm
05:53 Rarest-First Piece Selection Strategy
07:42 Advantages of Rarest-First Piece Selection Strategy
10:26 How does a peer compute the rarest piece
13:50 Random First Policy
16:25 Strict Priority Policy
18:37 End Game Mode

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1lAM5ohzk87b5tC22HRJ4-Eesyg99W_0z/view?usp=sharing)
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

<img width="256px" src="https://edge.arpitbhayani.me/img/arpit.jpg" />

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