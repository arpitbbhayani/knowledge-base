Getting the best performance from the Hash Table
===


Hash Tables are designed to give a constant time performance and to do this, it needs to have a large number of slots available. So, which factors decide its performance?

## Load Factor

Load Factor is a quantification that makes it simple for us to tell how loaded the Hash Table is, and it is just a simple division of the number of keys and the number of slots in the hash table.

As the load factor increases, the performance of the Hash Table decreases. It happens purely because it takes longer for us to do a slot lookup and find an empty slot to place the key.

## The Best Strategy

Every probing strategy or collision resolution strategy has its merit and demerit, and they all perform the best in a certain condition and the worse in others. Let's take a detailed look.

### Chained Hashing

Chained Hashing is costly, as it requires us to do a linear traversal of the linked list to find the key we are looking for. As the collisions increase, the lookup time shoots up, degrading the performance.

Chained Hashing is not cache-friendly, as it requires us to do random lookups in the memory while hopping from one linked list node to another.

### Double Hashing

Evaluating two hash functions requires extra CPU cycles that could get taxing. Double hashing is also not cache-friendly, as it requires us to jump across the Hash Table to hunt an empty slot.

The optimal strategy is contextual. If the performance of the Hash Table is critical, then we need to experiment, tune, and evaluate the best that fits us.

## Lookup Time vs Load Factor

Lookup Time is the most critical metric in evaluating the performance of the Hash Table; when we benchmark Lookup Time vs Load Factor, we would see

- perf of Open Addressing degrades as the load factor increases
- perf of Chained Hashing degrades gracefully with load factor
- Linear Probing would be slower than Double Hashing
- Probes required for Double Hashing would be shorter

## Making Chained Hashing cache efficient

Chained Hashing is known for being cache-inefficient, as it requires us to traverse through linked list nodes that may be present across the heap. Can we somehow make it cache efficient?

To make Chained Hashing cache-friendly, we have to ensure that the nodes of the linked list are allocated contiguously instead of randomly. Hence, instead of allocating one node at a time, we allocate the space for 5 nodes (like an array) at a time and then form the linked list out of them.

This would make the linked list leverage the CPU cache well and ensure our iterations are efficient as the next nodes will be available in the CPU cache, not requiring us to fetch them from the main memory.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Getting the best performance from the Hash Table](https://i.ytimg.com/vi/oD2yaTtu69w/mqdefault.jpg)](https://www.youtube.com/watch?v=oD2yaTtu69w)

In the previous 6 videos, we talked about the internals of Hash Table, ways to implement them, and how to gracefully handle collisions.

In this video, we put our focus on performance and would look at how to quantify the load on the hash table, the impact of chaining and open addressing on perf, understanding the performance gains and losses for each strategy, and conclude with very interesting performance optimization.

Outline:

00:00 Agenda
02:28 Load Factor
03:36 Load Factor for resolution strategies
09:22 The best strategy for a Hash Table
14:29 Lookup time vs Load Factor
20:03 Making chained hashing cache-friendly

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1maLTNs7gFIu6zCQvX-v-_BKQy_F5Tgqv/view?usp=sharing)
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