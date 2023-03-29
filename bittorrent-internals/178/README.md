Overview of the BitTorrent architecture
===


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
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Overview of the BitTorrent architecture](https://i.ytimg.com/vi/shVvFVFiZcs/mqdefault.jpg)](https://www.youtube.com/watch?v=shVvFVFiZcs)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

BitTorrent is superb, but what does its architecture look like?

In this 3rd video of the BitTorrent internals series, we take an in-depth look into its architecture and understand different components in it like - Tracker, Seeders, and Leechers, and learn how they work together to be this amazing file distribution network.

Outline:

00:00 Agenda
02:22 Pieces
04:50 Torrent File
06:53 Tracker
15:42 Architecture Overview
18:12 Seeders and Leechers

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/12NIH6eE6SlXSPkMdQP8jTKlu1Hz7-qMH/view?usp=sharing)
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