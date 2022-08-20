Exploiting and stealing from the BitTorrent network
===


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
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Exploiting and stealing from the BitTorrent network](https://i.ytimg.com/vi/nYtAzzH-twM/mqdefault.jpg)](https://www.youtube.com/watch?v=nYtAzzH-twM)

Stealing is bad, but in a P2P network, it is a cakewalk.

In this 7th video of the BitTorrent Internals series, we take a detailed look into various challenges that comes with a P2P network and dive deep into engineering hacks that could help us download our torrent faster and cheaper.

Outline:

00:00 Agenda
02:21 Quick Overview
05:11 Pretend to be a new peer
08:45 Be greedy with piece selection
10:08 Open connections with a large number of peers
13:52 Pretend to upload

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1qG1mh2hu5P2V38wGilIr_Dyl5I0_tZD-/view?usp=sharing)
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