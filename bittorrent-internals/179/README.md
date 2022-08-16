The Choke Algorithm that powers BitTorrent
===


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
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![The Choke Algorithm that powers BitTorrent](https://i.ytimg.com/vi/iognYJRzCE8/mqdefault.jpg)](https://www.youtube.com/watch?v=iognYJRzCE8)

One of the most important algorithm that powers BitTorrent is The Choke Algorithm

In this 4th video of the BitTorrent Internals series, we go deep and understand what the choke algorithm is, how it works, and most importantly how, without having a central authority, it ensures that no one abuses the P2P network.

Outline:

00:00 Agenda
02:24 Core idea of peer selection
04:53 Choking and Interested
08:02 Finding peers to unchoke
13:15 Choke algorithm for Leecher
26:12 Choke algorithm for Seeder

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1VQXEeC8MBgKAzkEJ5HwOjBV5-H3br-Ey/view?usp=sharing)
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