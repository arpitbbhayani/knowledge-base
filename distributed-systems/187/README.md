Synchronous Breadth First Search Algorithm to power broadcast in Distributed Systems
===


Breadth First Search is a critical algorithm in Distributed systems as it powers key features like

- Broadcast in minimum time
- Building topological understanding
- Topological stat like Diameter

In this gist, we discuss a synchronous approach which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

## Output of BFS

The output of this traversal is a Breadth-First Directed Spanning tree that covers all the nodes but a subset of edges. This output is important because we can use this spanning tree as a foundation for other applications and algorithms.

## The algorithm

The node `i0` initiates the BFS and it sends the `search` message to its neighbors. The nodes can either be marked or unmarked. If marked, they are part of the spanning tree already.

When an unmarked node receives the `search` message,

- it marks itself
- updates its parent to the node it received the `search` message from

In the next round, the nodes that received the message in the previous round participate, and send `search` messages to their neighbors, and the nodes receiving the messages do the needful.

Eventually, every node will be receiving the `search` message from some or the other node and will be part of the spanning tree.

## Complexity Analysis

Time taken to complete the BFS is proportional to the diameter of the network and the number of messages exchanged will be equal to the number of outgoing edges in the network.

## Conveying the children

With the current algorithm, every node knows its parent in the spanning tree but every node also needs to know which of its neighbors are its children in the spanning tree.

To achieve this, each node has to respond to the `search` message with a `parent/non-parent` message that tells the node if it was chosen to be the parent or not. This way, every node will know its parent and children in the spanning tree.

## Termination of BFS

The most important part of any distributed algorithm is its termination. How would the node know that BFS is done?

The approach we use is called Convergecast.

The idea is to respond to the search message only when it received responses from all its children. This ensures that the node initiating the BFS would receive the messages from its children only after all the nodes respond to their corresponding parents.

## Applications

After constructing the BFS Spanning Tree, we can use this constructed path to

- do an efficient broadcast on the network
- do distributed computation in the network
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Synchronous Breadth First Search Algorithm to power broadcast in Distributed Systems](https://i.ytimg.com/vi/PTlYBBqAYXA/mqdefault.jpg)](https://www.youtube.com/watch?v=PTlYBBqAYXA)

In a distributed system, what if one of the nodes wants to efficiently broadcast a message in the network?

The situation is not as simple as it sounds, because there is no single node that holds the information about the entire topology; they just know about their immediate neighbors.

In this video, we take a look into an algorithm that powers synchronous Breadth-First Search traversal in a distributed setup, understand its time and communication complexity, and talk about its applications.

Outline:

00:00 Agenda
02:36 Breadth-First Search and Distributed Systems
06:26 BFS Distributed Algorithm
13:58 Termination of the Algorithm
18:57 Applications of BFS in Distributed Systems

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1s39L6dNbDCN0xk_ZpyVKRf2a2OgZsCdr/view?usp=sharing)
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