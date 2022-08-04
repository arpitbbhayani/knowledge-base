Quadratic Probing for Conflict Resolution in Hash Tables
===


Linear probing is a popular way to handle Hash Table collisions, but is that the only way? Definitely not.

## Challenges with linear Probing

Linear Probing suffers from one significant challenge, and that is clustered collision. With a poor hash function, it is very much possible that some slots are preferred more over others, and upon collision, they are placed next to each other.

Hence, we would see clusters of collided keys forming across the entire hash table, and this is called Clustered Collision. Linear Probing suffers from this the most.

## Quadratic Probing

Quadratic Probing determines the next slots as per an arbitrary probing function

```
p(k, i) = h(k) + c1 * i + c2 * i^2
```

For attempt 0, we get the primary slot `h(k)` and post that for each attempt we move quadratically through the hash table to hunt for the next available slot.

Because of the quadratic jump, we do not form clustered collisions, instead, we cover a good chunk of the hash table. A simple quadratic sequence would be

```
h(k) + 1
h(k) + 4
h(k) + 9
h(k) + 16
.
.
```

Where `h(k)` is the primary slot we got by passing the key through the hash function and 1, 4, 9, and 16 are the quadratic offsets.

## Properties of Quadratic Probing

### Reducing clustered collisions

Quadratic Probing reduces the clustered collisions by distributing collided slots quadratically across the hash table and utilizing the entire hash table space.

### Good Locality of Reference

Quadratic Probing has a good locality of reference. When we access a particular slot of the hash table, we are also bringing in neighboring slots to the CPU cache. Upon collisions, when we access a few next quadratic slots, we need not fetch it from the RAM.

The locality of reference is not as high as Linear Probing, but it is decent enough when we observe fewer collisions per slot.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Quadratic Probing for Conflict Resolution in Hash Tables](https://i.ytimg.com/vi/F-8pWiJv8ik/mqdefault.jpg)](https://www.youtube.com/watch?v=F-8pWiJv8ik)

In the previous video, we looked at Linear Probing as a way to handle Hash Table collisions, but is that the only way? or Can we do better? In this video, we take a look at Quadratic Probing as an alternative to Linear Probing.

We spend time understanding what Quadratic Probing is, and how it is better than the Linear counterpart.

Outline:

00:00 Agenda
02:22 Introduction
03:52 Challenges with Linear Probing
05:44 Quadratic Probing
07:56 How Quadratic is better than Linear
08:56 Properties of Quadratic Probing

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1UAB8YOoRQwygQwILlpTTR7Wfgns_tHke/view?usp=sharing)
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