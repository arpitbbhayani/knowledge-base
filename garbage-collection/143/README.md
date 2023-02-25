Why caching would not speed up Mark-and-Sweep GC?
===


Mark and Sweep GC is one of the most common garbage collection algorithms that has seen a massive adoption. The algorithm has two phases:

- Mark Phase: we iterate through the object reference graph and mark all the reachable objects as live; and
- Sweep Phase: we iterate through all the objects in the main memory and delete all the objects that are not marked live; thus cleaning up the garbage

## We need Garbage Collectors to be fast

Garbage collectors need to be fast because we want the CPU cycles to be used in running the core business logic of the user program and not cleaning up unused variables.

## What is a Cache?

A cache is anything that stores the data so that future requests are served faster. The data we can cache can be

- results from the previous computation
- a copy of the data from a slower storage

## When does caching improve performance?

Caching improves the performance of an application only when the use case exhibits one of the following two behaviors

### Temporal Locality

A recently accessed memory location is likely to be accessed again.

By caching the data, we can thus serve the information from the cache instead of doing an expensive lookup or computation.

### Spatial Locality

If a location is recently accessed, the location adjacent to that is likely to be accessed soon.

By caching the data, we can thus serve the information from the cache instead of going through slower storage like disk or main memory.

## Hardware and Cache Prefetching

To leverage caching, modern hardware pre-fetches the data, likely to be accessed, from the slower storage and caches it. This boosts the performance of the application.

There are two ways to pre-fetch:

- hardware intelligently pre-fetches the data as per the access pattern
- hardware exposing "prefetch" instruction leaving to the business logic to prefetch

## Why caching would not improve GC performance?

As we established, for caching to improve the performance our use-case would need to exhibit either spatial or temporal locality. Do mark and sweep exhibit either of them?

### Mark n Sweep and Temporal Locality

Mark and Sweep GC does not exhibit temporal locality given that we mark all the reachable objects in one iteration and in other iteration we go through the unreachables one and free them.

### Mark n Sweep and Spatial Locality

Mark and Sweep GC does not exhibit spatial locality given we we do a DFS on object reference tree which hopes from one object too another in random order. So pre-fetching of memory locations would not help.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Why caching would not speed up Mark-and-Sweep GC?](https://i.ytimg.com/vi/LkympMbgmCo/mqdefault.jpg)](https://www.youtube.com/watch?v=LkympMbgmCo)

So, caching doesn't always work!

What would happen if we apply caching to speed up our Mark and Sweep Gargabge collector? Will it improve its performance?

Today we understand the key patterns that are essential for our caching to work. If those patterns do not exist, caching would be ineffective. The concept we discuss today is something that holds true universally and is not restricted just to the world of Garbage Collectors.

Today we take an in-depth look into caching, how it works, why it works, and understand why there would not be a significant performance improvement if we apply caching to our Mark and Sweep Garbage collector?

Outline:

00:00 Agenda
03:09 Refresher about Mark and Sweep
04:06 Why garbage collection needs to be fast?
05:00 What is a cache?
08:36 When would a cache improve performance?
11:09 Hardware and Cache Prefetching
14:50 Why caching would not improve Mark and Sweep's performance?
19:14 A minor speed-up through caching

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1GpbYMPJPS78hOlN6KRagF58S7lvQfhh4/view?usp=sharing)
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