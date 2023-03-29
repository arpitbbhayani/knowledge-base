Double Hashing for Conflict Resolution in Hash Tables
===


Linear and Quadratic probing do a great job at handling collisions in a Hash Table, but they both suffer from Clustered Collision, which degrades performance. So, can we do better?

Double hashing is a technique that minimizes the problem of clustered collisions by using a secondary hash function to find the next available slot.

## Double Hashing

Double hashing is an Open Addressing technique to address collisions in a hash table; hence, instead of using an auxiliary data structure to hold the collided keys, it leverages the already available free slots.

The probing function for Double Hashing is defined as

```
p(k, i) = (h1(k) + i * h2(k)) mod m
```

Thus, with every attempt we make to find an empty slot, we can leap by any distance in any direction, making all slots equally likely. A sample sequence for a particular key `k1` could be

- primary slot: `h1(k1)`, if that is occupied then
- attempt 1: `h1(k1) + h2(k1)`, if that is occupied then
- attempt 2: `h1(k1) + 2 * h2(k1)`, if that is occupied then
- attempt 3: `h1(k1) + 3 * h2(k1)`, and so on

Linear probing and quadratic traversals take a predictable leap to hunt for an empty slot, while double hashing probing leaps depend on the key and hence reduce the chances of clustering. So, different keys will have different leaps.

## Choosing a second hash function

The second hash function is super-critical, as it is aimed at resolving collisions effectively while ensuring minimal clustering. The second hash function should

1. never return 0
2. cycle through the entire table (with no particular order)
3. be fast to compute and almost feel like a random number generator

## Advantages of Double Hashing

1. Uniform spread upon collision
2. follows no specific offset pattern, the key purely depends on
3. least prone to the clustering problem

## Disadvantage of Double Hashing

Double hashing is not cache-friendly, as it requires us to hop across the hash table to hunt an empty slot. We may be at one extreme of the table and then move to the other one.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Double Hashing for Conflict Resolution in Hash Tables](https://i.ytimg.com/vi/wV4K6fo0T58/mqdefault.jpg)](https://www.youtube.com/watch?v=wV4K6fo0T58)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

In previous videos, we talked about Linear Probing, and how good it is, but we learned that it suffers from clustered collisions; then we spoke about quadratic probing and saw how it addresses the issue of clustered collisions, but can we do better?

In this 6th video of the Hash Table Internals series, we talk about the final technique of conflict resolution called Double Hashing; understand how it addresses a big concern with clustered collisions, learn about a few things that would help us choose a good hash function, and conclude by looking at the advantages of using double hashing as a probing technique.

Outline:

00:00 Agenda
02:40 Introduction
06:23 Double Hashing
10:17 Choosing the second hash function
13:37 Advantages of Double Hashing

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1EbFM7ZleP4Gwsq14moI7kbQMXJSEdj5D/view?usp=sharing)
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