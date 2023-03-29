HS algorithm for Leader Election in Distributed Systems
===


Leader Election is a critical component in any distributed system. It enables the system to auto-recover from leader failures. When a leader node goes down, the Leader Election algorithm is triggered to elect the new leader.

## HS Algorithm

HS algorithm is synchronous which means every node proceeds with the algorithm in sync. A key highlight of this algorithm is that it has communication complexity i.e. number of messages exchanged, of O(n long).

The algorithm works with the following assumptions

- every node has a comparable unique ID
- the communication between nodes is bidirectional
- the nodes are virtually arranged in a circular ring
- the nodes know their immediate neighbors

### The flow

Every node participates in the election. To pitch itself, it creates a message with its UID and sends it to its immediate neighbors in both directions.

To reduce the number of messages required to elect the new leader, the nodes who knows their UID is smaller, they quickly drop out of the election.

The election proceeds in phases. In each phase `i`, the nodes participating in the election send their candidature to a hop distance of 2^i and wait for it to come back.

Every node along the path, upon receiving the message,

- if the incoming is greater than its own, it forwards it
- if the incoming is lesser than its own, it discards

If the node, receives its UID as an incoming message from both directions then it knows that it has the maximum UID in the 2^i neighborhood. With each phase, the hop distance increases exponentially.

With each phase, the nodes with smaller UIDs start to drop off from the election while still acting as the transmitter of the messages. After certain phases, there will be only one node remaining and that becomes the new leader.

### Halting

The leader election in the HS algorithm halts when the node receives its probe message and thus it knows that it is the only one left and hence declares itself as the new leader.

The new leader creates the announcement message and relays it across the ring announcing itself as the new leader all the nodes locally update it and the election is concluded.

### Key Implementation Detail

The message sent across during the election contains `<uid, hops, direction>`. It helps the node know

- the number of hops the message has taken
- stop forwarding when the hop count becomes 0
- in which direction to reply
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![HS algorithm for Leader Election in Distributed Systems](https://i.ytimg.com/vi/inzQQm-kXCo/mqdefault.jpg)](https://www.youtube.com/watch?v=inzQQm-kXCo)

Leader Election is important in every single distributed system out there as it enables us to auto recover from the failures.

In this video, we take a detailed look at a synchronous ring-based algorithm called the HS algorithm and see how it works on a bidirectional network in O(N logN) complexity.

Outline:

00:00 Agenda
02:22 Introduction to HS Algorithm
05:07 The HS Algorithm
14:37 Halting the HS algorithm
16:18 Key implementation detail of HS algorithm

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1CHtYoRO_-LFEkX_R0xtTLPVsWfCO9jQd/view?usp=sharing)
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