Implementing Hash Sets with Hash Tables
===


The set data structure, when implemented with Hash Tables, is called a Hash Set; and just like a regular set, it supports operations like Union, Intersection, and Difference.

## Key Implementation Details

Hash sets are required to store the application keys that could be strings, integers, objects, etc., but the Hash Table understands only integers. We first pass the application keys through a hash function to map it to a 32-bit integer, and then the usual Hash Table operation takes over.

Given that the application key to hash key is a frequent operation, we would keep it handy by storing it alongside the application key. This helps us save repeated computations.

It is quite possible that multiple application keys would map to the same hash key, hence while looking up a key in the hash set, we first reach the slot, and then compare if the key present there is really the key we are looking for as we cannot just rely on the equality of the hash keys.
 
To achieve this, our Hash Set would need to accept a comparator function that can be used to compare two application keys for equality. Hash Set would use this comparator to check for the key equality, making our implementation agnostic.

## Hash Sets with Chained Hash Tables

Each node of the linked list in the chained hash table would have the following structure

```
struct node {
    int32 hash_key;
    void *key;
    struct node *next;
}
```

`void * key` would allow us to hold a key of any type, while `int32 hash_key` would enable us to hold a pre-computed hash, saving a lot of runtime computations.

At the Hash Table level, we would hold

- the array of linked list
- the size of the array
- number of keys
- key comparator function

## Hash Sets with Hash Tables having open addressing

Each slot of the hash table will have the following structure

```
struct node {
    int32 hash_key;
    void *key;
    bool is_empty;
    bool is_deleted;
}
```

`void * key` would allow us to hold a key of any type, while `int32 hash_key` would enable us to hold a pre-computed hash, saving a lot of runtime computations. `is_empty` would tell us if the slot is empty, while `is_deleted` would represent a soft deleted slot.

At the Hash Table level, we would hold

- the array of linked list
- the size of the array
- number of active keys
- number of used slots
- key comparator function

Note: here the load factor will be computed as the number of used slots/size of the array because the soft deleted keys also affect the performance of the hash table.

During insert, lookup, and delete when we find the matching hash, we need to explicitly compare the application key because multiple application keys can hash to the same location, and hence we cannot rely on just hash key equivalence.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Implementing Hash Sets with Hash Tables](https://i.ytimg.com/vi/CcoMvgIdrD8/mqdefault.jpg)](https://www.youtube.com/watch?v=CcoMvgIdrD8)

Sets are amazing, but how are they implemented?

In this 10th video of this Hash Table Internals series, we take an in-depth look into the implementation of Sets using Hash Tables, popularly called Hash Sets.

We will go into implementation details and performance tuning of Sets and see how they are built on top of Tables having Chaining and on Tables having Open Addressing.

Outline:

00:00 Agenda
02:26 Introduction to Hash Sets
05:10 Key Implementation Details
09:01 Implementing Sets with Chained Hash Tables
11:03 Implementing Sets with Hash Tables with Open Addressing

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1mkT3gt19e6LrG6CJzYaodbbjsLBZVlLY/view?usp=sharing)
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