LCR algorithm for Leader Election in Distributed Systems
===


Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## LCR Algorithm

LCR Algorithm for leader election is the simplest and the easiest to understand and implement, and its variant can be seen in action in a bunch of distributed systems.

The LCR algorithm expects the network to have the following properties

### Unique ID

Every node in the network has a unique identification - UID - that can be compared with other UIDs.

### Virtual Circular Ring

LCR also assumes that the nodes in the network are virtually arranged in a circular ring, and each node knows the node to its right in the ring.

Although we want a circular ring, the nodes may be physically connected to other nodes through any topology. The ring mandate is purely virtual and can be maintained only for powering elections.

### The Algorithm

In the election, every node participates to be the new leader. To participate, it creates a message having its UID and sends it to its neighbor.

When a node receives a UID, it compares the incoming UID with its own, and

- if the incoming is greater than its own, it forwards it
- if the incoming is lesser than its own, it discards
- if the incoming UID == its own, it declares itself as the new leader

When a node receives its UID as an incoming message, it implies that the message survived the entire iteration leading to the assertion that the node has the highest UID in the network; and hence can become the new leader.

The new leader is then announced through another message passed across the ring.

### Halting the algorithm

Halting is one of the most important aspects of any distributed algorithm, as it can get tricky to know when to stop.

LCR algorithm stops when the new leader initiates the message and announces itself. To announce, it initiates the `HALT` message and sends it across.

The node receiving the `HALT` message understands that the new leader has been elected and needs to stop participating in the election. The node updates its local state with this information and forwards the message to the next node.

## Complexity

Each node participates in the election and sends messages across the entire ring. Every node could potentially receive the message from every other node; the communication complexity, the number of messages shared, is thus O(n^2).
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![LCR algorithm for Leader Election in Distributed Systems](https://i.ytimg.com/vi/NDBJr37dBzc/mqdefault.jpg)](https://www.youtube.com/watch?v=NDBJr37dBzc)

Leader Election is important for our distributed systems to auto recover from the failures.

In this video, we take a detailed look into a simple, naive, and intuitive distributed Leader Election algorithm called LCR, and understand how simple yet effective this algorithm can be.

Outline:

00:00 Agenda
02:19 Introduction to LCR Algorithm
05:07 The LCR Algorithm
09:54 Halting the LCR Algorithm
11:44 Complexity Analysis of LCR Algorithm

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1W-9SA2qEo6jKvxcM4iMi326R63lK7XVm/view?usp=sharing)
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