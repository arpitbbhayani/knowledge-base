Conflict Resolution in Hash Tables with Chaining
===


Collisions are inevitable in Hash Tables, and a common way of handling them is through chaining using Linked List. But can we use some other data structure?

Collisions are inevitable in Hash Tables, as we are mapping a large range of application keys to a smaller range of array slots. So, there are chances that the hash function spits out the same value for two different application keys.

Because Hash Tables cannot be lossy, we need a way to handle these collisions and allow storing of multiple keys that are hashed to the same slot. A way to achieve this is chaining, and it is very commonly implemented through a Linked List.

## Data Structures

To accommodate this, the Hash Tables are now implemented as an array of Linked List where all the keys that collide are placed.

### Adding a Key

While adding a key to the hash table, we first pass it through the hash function and get the slot index. We then create a node holding the key and add it to the linked list.

We can add the new node at one of the 3 places

- always at the head of the list - O(1)
- always at the tail of the list - O(1)
- in the middle of the list while maintaining a sort order - O(p)

### Deleting a Key

To delete a key, we first pass it through the hash function and get the slot index. We then iterate through the linked list present at the slot, element by element, and locate our key of interest.

While iterating, we keep track of the pointer to the previous node so that once we reach the node to be deleted, we adjust the pointers and free up the node.

### Key Lookup

Key lookups are similar to delete operations. We first pass the key through the hash function to get the slot index. We then iterate through the list present at the slot and locate our key. The operation requires us to iterate the list iteratively.

## Other Data structures for chaining

Linked List is not the only data structure that we have to use to chain the collided keys. Depending on the use case, access pattern, and constraint, we can pick a data structure that suits us.

For example, if our array is small, and we cannot resize it, then we may end up having many collisions. If we are trying to read, then iterating over this list will reduce the throughput as it is a linear scan.

To optimally perform a key lookup, when the collisions are high, we can use a self-balancing search tree, like BST or Red-Black. This way, we get an optimal lookup performance on keys hashed to the same slot.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Conflict Resolution in Hash Tables with Chaining](https://i.ytimg.com/vi/9rb8oILi4lU/mqdefault.jpg)](https://www.youtube.com/watch?v=9rb8oILi4lU)

Collisions happen in Hash Tables as we are trying to map a huge space of application keys in a small array. But there are ways to solve it and one of the most common ways is called Chaining.

In this video, we go in-depth about collisions in Hash Tables, resolve them through chaining, explore some really granular details that would help us squeeze the best performance out of our implementation, and most importantly look at a different data structure to implement it.

Outline:

00:00 Agenda
02:29 Introduction
03:42 Chaining
04:58 Chaining with Linked List
08:03 Adding a key in the Hash Table
14:04 Deleting a key from the Hash Table
15:47 Lookup a key in the Hash Table
17:15 Chaining with Binary Search Trees

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1so447uSDzZZuJXAyMB_jGqHCM0RX3hbL/view?usp=sharing)
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