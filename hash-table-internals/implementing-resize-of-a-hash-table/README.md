Implementing Resize of a Hash Table
===


Resizing a Hash Table is important to maintain consistent performance and efficiency, but how do we actually implement it?

Resize is all about

- allocating a new array of the desired size
- insert existing keys in this new array
- delete the old array

But a few granular details are specific to the type of hash table.

## Resizing a Chained Hash Table

Resizing a table happens when the load factor hits a threshold. To implement an efficient resize, a Hash Table that uses chaining needs to keep track of

- number of keys
- total number of slots

This would help us avoid reevaluation, and we can instantly compute the load factor.

### Resize during insert

While we are inserting a key in the Hash Table, we keep on checking the load factor. If it breaches the threshold, we trigger the resize.

```
insert_key(k, table) {
    ------
    LF = count_keys / total_slots;
    if (LF >= 0.5) {
        resize(table, total_slots * 2)
    }
}
```

### Shrinking during delete

While we delete a key from the Hash Table, we check the load factor. If it breaches the threshold, we trigger the shrink. The pseudocode is fairly similar to the above one.

### Two ways to implement resize

Chained Hashing is implemented using Linked List and there are two ways to resize

1. we iterate through the keys and re-insert them into the new array
2. we iterate through the keys and just adjust the pointers of the nodes, instead of re-allocating the new set of nodes.

## Resizing a Hash Table with Open Addressing

In open addressing, we always soft delete so that we can reach the elements placed further in the collision chain. To handle this gracefully, we need two counters at the hash table

1. Key Counter: number of active keys in the table
2. Used Counter: number of used slots in the table

For open addressing, the load factor will be counted as the used counter divided by the total slots. The deleted keys also affect the performance as we have to go past them looking for the keys.

Hence, the Key Counter will increase and decrease upon every insert and delete, while the used counter would increase upon insert but would reduce only when we do a resize.

### Resize during insert

While we are inserting a key in the Hash Table, we check the load factor. If it breaches the threshold, we trigger the resize. Resize operation would skip the deleted keys and re-insert only the active keys.

### Shrinking during delete

The shrinking of the hash table will be triggered when the number of active keys falls beyond the threshold, and hence here our load factor for this operation would be active keys / total_slots.

Similar to the insert phase, we would skip the deleted keys and re-insert only the active keys in the new array. The key counter and the user counters are adjusted accordingly.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Implementing Resize of a Hash Table](https://i.ytimg.com/vi/mmPwVBm-8n0/mqdefault.jpg)](https://www.youtube.com/watch?v=mmPwVBm-8n0)

So, the Hash Table needs to be resized in order to maintain consistent performance, but how exactly?

In this 9th Video of the Hash Table Internals series, we go into the implementation details of resize operation and talk about, where and when in the code should we trigger resize, 2 ways to implement resize while using Chained Hashing, and things to remember while resizing a Hash Table that uses open addressing.

Outline:

00:00 Agenda
02:28 Introduction to Resize
03:18 Implementing Resize on Chained Hash Tables
08:55 Implementing Resize on Hash Tables with Open Addressing

Learn Hash Tables Internals in a structured way at https://courses.arpitbhayani.me/hash-table-internals

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1wJWnXlQS4SKJBdmCg799gwb2dL7JSaPv/view?usp=sharing)
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