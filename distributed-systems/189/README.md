Minimum Spanning Tree in Distributed Systems - GHS Algorithm - and its Applications
===


Minimum Spanning Trees are super-critical in distributed systems, and they form the crux of building efficient broadcasting systems.

## Spanning Tree

A tree that covers all the nodes through selective edges. MST is the Spanning Tree such that the summation of the weights of the covered edges is minimum.

The weights on the edges can quantify communication latency, congestion, cost of the communication, or even distance.

## Distributed Setup

In a distributed setup, every node does not have information about the entire topology, instead, it holds the information about just itself, the nodes connected to it, and the incident edges.

## GHS Algorithm

The algorithm operates on a "level" and each level is a collection of a bunch of spanning trees. The core idea of this algorithm is to continue grouping spanning trees into a bigger ones until we are left with one huge spanning tree.

Level 0 consists of all the nodes and no edges and if we have `n` nodes, there will be `n` spanning trees (components) in the forest.

Every spanning tree would know

- total number of nodes n
- incident edges to it
- its UID of the leader of its component

Each node within the component sends a search message to the component to get MWOE (Minimum Weight Outgoing Edge).

Each node upon receiving the message searches for an outgoing edge that is connecting to the node that is not part of the component. Of all such edges, the node picks the edge with the min weight and sends it across to the leader of the component.

### How to test if another node is in another component?

Every node knows its leader UID and hence a node sends a `test` message to its immediate neighbors and they revert back with their leader UIDs. Comparing this UID with its own, the node knows if the other node is part of the same component or not.

### Merging the components

Now that the leader has the all minimum outgoing edges from the peripheral nodes, it can find a global minimum outgoing edge that is going out of its component.

The leader of the component now talks to the nodes connected over MWOE and tells them to mark itself in under this component. The new leader of the merged component is one of the two nodes with a higher UID connected over the MWOE.

### Level by Level

The spanning tree is constructed level by level. It starts with all nodes being their own Spanning Tree. Then Two Level 0 nodes merge to form Level 1 nodes, and then Level 2 and so on.

### Termination of the algorithm

The algorithm will terminate when the leader of the component is trying to find MWOE but none of the nodes sends it any information given they are all part of the same tree.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Minimum Spanning Tree in Distributed Systems - GHS Algorithm - and its Applications](https://i.ytimg.com/vi/c5t1rP6CvNs/mqdefault.jpg)](https://www.youtube.com/watch?v=c5t1rP6CvNs)

Nodes in a distributed system need to exchange a lot of messages; a naive way to do this is to flood the network with the message across all the connection lines across all the nodes.

This is highly inefficient and would unnecessarily congest the network. Hence we need our distributed network to maintain a Minimum Spanning Tree so that we can do an easy broadcast of the message to all nodes in the most efficient way.

Hence, in this video, we take a look into the famous GHS algorithm to construct the Minimum Spanning Tree in a distributed setup, go through the algorithm step by step, and see how a spanning tree makes leader election a piece of cake.

Outline:

00:00 Agenda
02:45 Need for Minimum Spanning Tree
06:49 GHS Algorithm to build Minimum Spanning Tree in Distributed System
22:20 Termination of GHS Algorithm
24:36 Complexity Analysis
26:48 Leader Election using MST

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1s_N8lpPSDdORbAfH818joLsxA3rlR-Om/view?usp=sharing)
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