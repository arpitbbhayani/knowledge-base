Internal Structure of a Hash Table
===


Hash Tables are implemented through simple arrays, but how?

Hash Tables are so powerful, that OOP-based languages internally use them to power Classes and site members. Symbol tables that hold the variables mapped to a memory location are also powered through hash tables.

They are designed to provide constant-time key-based insertion, updation, and lookups while being space efficient at all times.

## Core Ideas to construct Hash Tables

- convert application keys to wide-ranged (`INT32`) hash keys
- convert hash keys to a smaller range

## Application Keys to Hash Keys

Hash Tables should support storing an object as a key and to power that the keys are first hashed to a big integer range (provided by the user) typically `INT32`. This hash key is then further used to decide how and where the KV pair would be stored in the data structure.

## Naive Implementation

A naive implementation of Hash Table would be to create an array of length INT32. To store the KV in it, we pass the key through the hash function spitting out an integer. We use this key and store the KV pair at this index in the array.

Although this would give us constant time insertion, updation, and lookups, it is highly space in-efficient, as we would need to allocate at least `4` * `INT32` = `16GB` of ram to just hold this array, with most of the slots left empty.

### Hash Keys to Smaller Range

This step is designed and introduced to make our Hash Table space efficient. Instead of having a huge array of length `INT32`, we keep it proportional to the number of keys inserted. For example, if we inserted 4 keys then our holding array could be around 8 slots big.

To achieve this, we map the hash key into a small range (same as the length of the array) and place our key at that very index. This allows us to remain space-efficient while sporting fast and efficient insertions, updations, and lookups.

## Adding more keys

The small limited-size array will not be able to hold a large number of keys and hence after a certain stage we would need a larger array to hold the data. This is done by resizing the holding array and is typically made 2x every time it is full enough.

Thus, this two-step implementation allows for near-constant time insertions, updations, and lookups while remaining space efficient.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Internal Structure of a Hash Table](https://i.ytimg.com/vi/jjW8w8ED3Ns/mqdefault.jpg)](https://www.youtube.com/watch?v=jjW8w8ED3Ns)

One of the most common data structures that we all use every single day is Hash Table. Every language has its own implementation and nomenclature for it. Python calls it dictionary, while Java calls it Hash Map. But the core idea remains the same: it holds pairs of keys and values and supports insertions, updation, and lookups in constant time.

But how are they implemented? What is its internal structure? In this video, we talk about what are hash tables, how are they structured internally, and lay a foundation to understand their constant-time implementation.

Outline:

00:00 Agenda
02:38 Introduction and Applications of Hash Tables
05:12 Core ideas to construct Hash Tables
07:07 Step 1: Application keys to Integer Hash Keys
09:38 Naive Implementation of Hash Table using Array
13:38 Step 2: Integer Hash Keys to a smaller range
17:43 Adding more keys on the fly
19:07 Do we really need the Keys to Hash Key step?

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1IKYDzO-mZEHDQYEsyoksFkF3DVyTCy6l/view?usp=sharing)
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