Why are Hash Tables always doubled?
===


To maintain consistent performance, the hash table has to be resized - be it growing or shrinking. The trigger to resize depends on the load factor, which is defined as the ratio of the number of keys that the hash table holds to the total number of slots.

## When should we resize?

The Hash Table is resized when the load factor hits a certain threshold. If we get too aggressive or too lenient, we would not be able to get the optimal efficiency. Hence, we have to find a sweet spot.

We typically grow the hash table when the load factor hits 0.5 and shrink when we hit 0.125.

## Why do we always double?

We have heard and seen so many times, that when a Hash Table is required to grow, we always double the underlying array; but why? Can we not just increase it by 1 every time we are trying to insert?

### Resizing by 1 every time

Let's take an example: say, we grow the array by 1 every time we insert an element in the Hash Table. Let's compute the time it requires to fill `n` elements.

Inserting the 1st element is: allocating an array of size 1, and inserting 1 element; so in all O(1) operations.

Inserting the 2nd element is: allocating an array of size 2, copying 1 element from the old array, and then inserting the 2nd element; so in all O(2) operations.

Hence, inserting the nth element is: allocating an array of size n, copying n-1 elements from the old array, and then inserting the nth element; so in all O(n) operations.

Total operations to insert `n` elements = 1 + 2 + ... + n = (n(n-1))/2 which is O(n^2).

### Doubling every time

If we double every time, inserting `n` elements requires O(n) time, as it is spacing out an expensive resize operation. We would be inserting n/2 elements before resizing the array to 2n.

Note: For a detailed amortized analysis, please refer to the video attached here, where I have explained the reasoning in depth.

## Why is a hash table array always a power of 2?

For a power of 2, the MOD and the bitwise AND spit out the same result and given that the bitwise AND is a magnitude faster than the MOD, we get the best performance out of our Hash Tables when we use AND

```
(i % 2^k) == (i & (2^k) - 1)
```

This is why the length of the underlying array is always a power of 2, making our most-frequent operation efficient.

## Shrinking the Hash Table

To ensure we are not wasting space, we trigger the shrink when we do not utilize the underlying array enough. While triggering a shrink, we also need to ensure that we are not aggressive enough that we have to grow immediately after the shrink.

Hence, we shrink the hash table when the load factor hits 1/8 i.e. in a table of length 64 if we are only holding 8 keys, we trigger a shrink and that reduces the length to 32.

Note: To understand why we do it at load factor = 1/8, please refer to the video.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Why are Hash Tables always doubled?](https://i.ytimg.com/vi/zt1E0akArqQ/mqdefault.jpg)](https://www.youtube.com/watch?v=zt1E0akArqQ)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Why are the underlying arrays of the hash tables always a power of 2? When we trigger a resize why are Hash Tables always doubled? like 2, 4, 8, 16, 32? What is the reason behind it?

In this 8th video of the Hash Table Internals series, we answer some super-cool questions and go in-depth on Hash Table resizing. We understand why we do it, how we do it, why hash tables are always doubled upon resize, why they are always sized as a power of 2, and conclude with an understanding of how and when we shrink them.

Outline:

00:00 Agenda
02:35 Why resize a Hash Table?
03:19 When to resize a Hash Table?
04:20 How to resize a Hash Table?
07:40 Why are Hash Tables always doubled upon resize?
17:27 Why are Hash Tables slots always a power of 2?
23:30 Shrinking a Hash Table

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1aHWaOIGT7-zB88T83In05pHIdpuJTSk7/view?usp=sharing)
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