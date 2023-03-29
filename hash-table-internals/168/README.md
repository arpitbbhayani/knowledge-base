Linear Probing for Conflict Resolution in Hash Tables
===


Linear probing is the simplest and one of the most efficient ways to handle conflicts in Hash Tables, let's understand it in-depth.

## Conflicts

Conflicts are inevitable, and Open Addressing is a technique to handle them in a space-efficient way. Instead of using an auxiliary data structure to hold the collided keys, open addressing leverages the free slots of the Hash Table to accommodate the collided keys.

To find the next available slot, open addressing defines a probing function that uses the key and the attempt to deterministically iterate through the slots.

## Linear Probing

We first hash the key and find a primary slot. If that slot is free, we place the key there. If the slot is occupied, we check the slot to its right. We continue to process until we find an empty slot.

This way, we continue to hunt for the key linearly from the primary slot. Once we reach the end of the array, we circle back to index 0. Formally, the probing function for Linear Probing would be

```
p(k, i) = (h(k) + i) mod m
```

## Hash Table Operations

### Adding a key

We first find the primary slot of the key using the hash function. If the slot is empty, we place the key there. If not, we move to the right and find the first empty slot and place the key there.

### Key lookup

Lookup is an iterative process where we first find the primary slot of the key, if the key is present at that slot then well and good. If not, we move to the right hunting for the key. We continue to linearly iterate through the array until

- the key is found, or
- we encounter an empty slot
- we cover all `m` slots of the hash table

### Deleting a key

Deleting a key in Linear Probing is always a soft delete. We first look up the key in the hash table and once we find it, we mark that slot as deleted but never physically empty it. This allows us to go beyond the deleted slot and hunt for any other collided keys.

## Why is Linear Probing Fast?

Linear probing is fast because it beautifully exploits the locality of reference. To access a certain slot in the hash table, we fetch the page in the CPU cache. The page will not just contain the requested slot, but it also contains the neighboring slots as well.

Hence, upon collision when we iterate from that slot, we would not need to fetch the slots from RAM, instead, some slots would already be present in the cache making iterations superfast.

In an average case, Linear Probing gives constant time performance for adding, lookup, and deleting a key.

## Challenges with Linear Probing

1. Bad hash function would lead to many collisions
2. It suffers from non-uniform clustered collisions

Hence, it is important to pick a good hash function, like Murmur Hash, to ensure a near-uniform distribution of keys and fewer collisions.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Linear Probing for Conflict Resolution in Hash Tables](https://i.ytimg.com/vi/5QKAXG25hig/mqdefault.jpg)](https://www.youtube.com/watch?v=5QKAXG25hig)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Linear Probing is one of the simplest and the most intuitive ways to handle Hash Table collisions, and it is based on a technique called Open Addressing.

In the video, the fourth of this Hash Table Internals series, we take a detailed look into Linear Probing, understand what it is, how Hash Table operations happen with Linear Probing, learn why it is so simple yet so efficient, and conclude with looking at 2 challenges that come with adopting it.

Outline:

00:00 Agenda
02:28 Introduction
03:50 Linear Probing
05:56 Hash Table Operations with Linear Probing
09:34 Why is Linear Probing fast and efficient?
03:47 Challenges with Linear Probing

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1hqt-b4fQEXwFEgiEUVIUe5qoynpYXDb0/view?usp=sharing)
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