Distributed Shortest-Path Bellman Ford Algorithm in Distributed Systems
===


Determining the shortest path in a distributed system is an important problem to address and it finds its application across multiple use cases like

- delivering messages to a node efficiently
- efficient routing of messages

A key point to consider here is the fact that "shortest" is not only about the distance, but it can also be about the congestion, time, cost of communication lines, cable infra, and much more.

## Problem statement

In a distributed network, where nodes are connected via paths/edges having some weight assigned, find the shortest path from a specific source to all the nodes

## Bellman-Ford Algorithm in Distributed System

In this gist, we discuss a synchronous approach which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

Because it is a distributed network no node knows the entire topology and weights. They just know

- total number of nodes
- their immediate neighbors, and
- the weights of the edges incident on it.

Every node keeps track of `dist` which holds the shortest distance to it from the source `i0`. Initially, `dist` at `i0` will be `0` and `dist` at all other nodes will be `inf`.

At every round, all the nodes will send their `dist` across all of their outgoing edges to their neighboring nodes. Every node `i` upon receiving an incoming `dist` from its immediate neighbor `j` compares

- its own `dist`
- incoming `dist` + `weight(i, j)`

after comparing, if the incoming distance plus the weight of the connecting edge is smaller than its own `dist` it means that the distance from `i0` to the current node could be shorter and hence, the node updates the `parent` suggesting that the shortest path from `i0` to `i` goes through `j`.

After `n - 1` rounds, the `dist` at every node will contain the shortest distance to it from source `i0`, and the `parent` will contain one of its immediate neighbors that lies in the shortest path.

## Complexity Analysis

We require `n - 1` rounds to complete the algorithm, the time complexity of Bellman-Ford Shortest Path in Distributed System is `O(n)`. At every round, every node sends `dist` message across all of its edges to its immediate neighbors, the communication complexity becomes `O(n x |E|)`.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Distributed Shortest-Path Bellman Ford Algorithm in Distributed Systems](https://i.ytimg.com/vi/tV3EQNgpZKI/mqdefault.jpg)](https://www.youtube.com/watch?v=tV3EQNgpZKI)

To keep our distributed system efficient and performant, we have to ensure that the messages that are sent within the network take up the most efficient path. We may think ... network ... graph ... efficient path ... shortest path ... so can we not use our graph algorithms?

We cannot use them directly because this is distributed system and there is no single node that holds the information about the entire topology. Every node simply knows about the incident edges, and hence we have to take baby steps while devising a solution.

In this video, we take a look into a variant of the famous Bellman-Ford shortest path algorithm and see how it operates in a distributed setting.

Outline:

00:00 Agenda
03:07 Need for Shortest Path in Distributed Systems
06:59 Bellman-Ford Shortest Path in Distributed Systems
14:35 Complexity Analysis

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1IG1MdH-DALxcbx3rtZ25KHxUwSbrwTfo/view?usp=sharing)
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

<img width="256px" src="https://edge.arpitbhayani.me/img/arpit.jpg" />

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