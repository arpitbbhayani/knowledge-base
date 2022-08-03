Conflict Resolution in Hash Tables with Open Addressing
===


Open Addressing is a common yet interesting way of handling collisions in Hash Tables and instead of using an auxiliary data structure, it leverages empty slots of the hash table to store the collided keys, making the entire approach space efficient.

While inserting a key in the hash table, we pass it through the hash function to get the slot, and if the slot is already occupied, we find the next available slot through probing.

## Probing

Probing is the process through which we deterministically find the next available slot in the hash table. The approach and algorithm could vary, but formally it is a function of the key to be placed and the attempt, that spits out a slot.

```
j = p(k, i)
```

The probing function uses the key `k` and an attempt `i` to spit out an index `j`. The attempt `i` and the index `j` are in the range `[0, m-1]`, where `m` is the size of the hash table.

### Good probing function

A good probing function would generate a deterministic permutation of numbers `[0, m - 1]` specific to the key `k`, so that we eventually check and cover the entire hash table for an available slot.

For example: for some key `k1`, on a hash table of size 8, the probing function might generate a sequence: 5, 7, 2, 1, 0, 6, 4, and 3. This means we first try to put the key in index `5`, if that is occupied we check `7`, then `2`, and so on.

## Hash Table Operations

### Adding a key

Until we find a free slot in the hash table, we keep invoking the probing function with attempts `0`, `1`, `2,`, etc. Once we find an empty slot, we stop and place the key in that slot.

### Key Lookups

For looking up a key, we invoke the probing function with attempt `0` and check the slot. If the slot holds the key we need, we stop and return the value. If not, we continue to probe with attempts `1`, `2`, etc., and continue to hunt.

We stop the iteration when

- we find the key,
- we stumble upon an empty slot during iteration
- we have checked the complete hash table

### Deleting a key

With open addressing, deleting a key from the table has to be a soft delete, because we need a way to differentiate between an empty slot and a deleted key.

If during deletion we empty the slot, then we would be unable to look and reach for a key that had a collision and was placed after the key we deleted.

## Limitation of Open addressing

Since we are not having any auxiliary data structure, a major limitation of Open Addressing is that the maximum number of keys we can hold are the same as the number of slots in the hash table.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Conflict Resolution in Hash Tables with Open Addressing](https://i.ytimg.com/vi/6_yFb7icd_c/mqdefault.jpg)](https://www.youtube.com/watch?v=6_yFb7icd_c)

Although chaining is a popular way of handling Hash Table Collisions, there is a very interesting way of achieving the same and it is called Open Addressing. The key highlight of Open Addressing is that it does not require any additional data structure to hold the collided keys, making them space efficient.

In this video, we look at Open Addressing, the core idea behind it, lay the foundation for probing functions and understand how the implementation of our core Hash Table functions changes with this scheme in place.

Outline:

00:00 Agenda
02:35 Introduction
03:06 Open Addressing
04:15 Probing Functions
08:45 Hash Table Operations

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1bvdtGMKVou-bfuOHzX3izdx2FHfQTpYS/view?usp=sharing)
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