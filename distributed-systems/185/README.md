TimeSlice algorithm for Leader Election in Distributed Systems
===


Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## TimeSlice Algorithm

TimeSlice algorithm for leader election is highly impractical, unbounded, yet an interesting algorithm to understand.

The algorithm assumes

- each node has a UID that is a positive integer
- the nodes are arranged in a virtual ring
- each node knows its immediate neighbor to the right
- each node knows the total number of nodes `n` in the network

### The flow

The election proceeds in phases 1, 2, 3, and so on. Each phase consists of `n` rounds. Because the algorithm is synchronous, each node knows when the algorithm is proceeding with rounds and phases.

In phase `i`, nodes can only forward the message having the candidature of UID `i`. Hence, in phase `3`, a node will forward the message to the next node, only when it is having the candidature of UID `3`.

## The flow

In phase 1, the node with UID 1 will send the message with its candidature across to the next node in the ring. If no such node exists, then no message is sent.

Thus, for `n` rounds within phase 1 there is void silence in the network. Then beings the phase 2.

Hence, we see that the messages will be sent across the ring only when the phase `i` beings where `i` is the smallest UID in the network. For all `(i - i) * n` rounds, there will be void silence in the network.

When phase `i` begins the node with UID `i` will know that it is the new leader and it initiates the message and sends it to the next neighbor. For `n` successive rounds, the message is sent across the network and thus all `n` nodes know about the new leader `i`.

## Complexity Analysis

The algorithm thus elects the node with the minimum UID as the new leader in just `O(n)` messages but takes time proportional to the `O(n*i)`.

If the minimum UID is a large integer, then the algorithm will take a longer time to elect the leader, and hence it is unbounded on the number of nodes in the network.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![TimeSlice algorithm for Leader Election in Distributed Systems](https://i.ytimg.com/vi/mcKLQVmCsG4/mqdefault.jpg)](https://www.youtube.com/watch?v=mcKLQVmCsG4)

Leader Election helps our Distributed Systems auto recover without any human intervention and makes the system autonomous.

In this video, we take a detailed look into a Leader Election algorithm called TimeSlice that is extremely impractical but it still provides us great insight into a seemingly weird implementation.

Outline:

00:00 Agenda
02:27 Introduction to the TimeSlice Algorithm
05:21 The TimeSlice Algorithm
11:03 Complexity Analysis of TimeSlice Algorithm

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1eZ2xCcikcZJ4krKj6pWuQtVvkFhCGAhL/view?usp=sharing)
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