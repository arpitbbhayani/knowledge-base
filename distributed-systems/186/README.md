FloodMax algorithm for Leader Election in Distributed Systems
===


Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

Leader Election should work with any topology and hence we take a look into an algorithm called FloodMax.

## FloodMax Algorithm

The Flood Max Algorithm Flood Max works with a network that is arbitrarily connected. It assumes that every node is given a comparable UID that may be randomly allotted and every node knows the network's diameter.

### The algorithm

The Flood Max algorithm is designed to elect the node with the maximum UID as the new leader and the core idea is to flood the network with the Max UID until the value converges.

The election process happens synchronously, which means every node moves forward in the algorithm in sync. There are ways to achieve this, but the implementation of synchronous behavior is out of the scope of this gist.

The algorithm stops after completing rounds equal to the diameter of the network. In each round, every node

- sends the max UID it has seen to the connected nodes
- updates the max UID it has seen so far after receiving messages from its neighbors

After completing the `diameter` number of rounds, each node will have the max UID it has seen so far which will also be the global maximum; thus every node will know who is the leader of the network.

### Complexity Analysis

It takes O(diameter) number of rounds to elect the leader and in each round the number of messages exchanged is equal to the number of edges, hence O(|E|); hence communication complexity is O(diameter x |E|).

## Reducing Communication Complexity

To decrease the number of messages exchanged during the election, nodes can send the Max UID only when it changes. This would significantly reduce the messages exchanged across the network during leader elections.

Another optimization to reduce the communication is to NOT send the Max UID in the direction of the neighbor from which it was received.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![FloodMax algorithm for Leader Election in Distributed Systems](https://i.ytimg.com/vi/4aeFQpuww4E/mqdefault.jpg)](https://www.youtube.com/watch?v=4aeFQpuww4E)

Leader Election is necessary to make Distributed Systems auto recover and remain autonomous.

In this video, we take a detailed look into a Leader Election algorithm called FloodMax that works on any network with any topology. We understand the runtime complexity of it and look at a couple of optimizations that make it efficient.

Outline:

00:00 Agenda
02:25 FloodMax Algorithm
08:45 Complexity analysis of FloodMax Algorithm
09:31 Optimizations in FloodMax Algorithm

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1yUZjPZoVKiKls7iof9Y-HF-9YsAoQpNN/view?usp=sharing)
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