Exponential Information Gathering (EIG) Algorithm for Byzantine Agreement
===


Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

## Byzantine Agreement

The byzantine agreement is a problem of reaching a consensus even when one or many nodes or processes are malicious/corrupt.

## EIG Algorithm for Byzantine Agreement

The core idea of the Exponential Information Gathering Algorithm is to gather a large amount of information from the network and then apply some decision rules to reach a consensus.

## EIG Data Structure

EIG algorithms require an EIG Tree that is like a Trie and is constructed level by level. If there are `n` nodes in the network and the level of the tree is `k` then the leaf of the tree contains all k-length permutations of `n` nodes.

If a node `a` received a message from a path `b, c, d` then the incoming message (value) is stored along the path `b`, `c`, `d` at the node `a`.

Thus, at each level of the tree, the number of children of each node reduces by 1. The root of the tree is labeled EMPTY, and it has `n` children, say A, B, and C.

Each node in the next level will have 2 children. A will contain `AB` and `AC` while `B` will contain `BA` and `BC`, and `C` will contain `CA` and `CB`. Thus we see at level 2 the leaves contain all 6 2-length permutations of A, B, and C.

## The algorithm

The construction of the EIG Tree remains the same as it was in the Distributed Consensus and we assume that each node has constructed the EIG tree independently.

The algorithm is tolerant to `f` faulty process. When a process sends an ill-formed value the nodes participating in the consensus discard the value.

Ex: expected int, got string, discard.

### Decision Making

The processes propagate their values for `f + 1` rounds and each node builds its own EIG Tree. Once the EIG Tree is constructed, to make the decision, a node traverses the entire tree level by level starting from the leaves towards the root.

While traversing, the parent's value is the majority of its children's values. If there is no clear majority, then the parent sets to the default value.

The final consensus is the value that the root node of the EIG Tree decides. If any of the fault nodes send ill-formed values, the value will get absorbed along the tree because most of the nodes are honest and correct values outnumber the fault ones.

Hence, gathering exponential information is the key to resolving Byzantine agreements.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Exponential Information Gathering (EIG) Algorithm for Byzantine Agreement](https://i.ytimg.com/vi/pi3YA3m1ffw/mqdefault.jpg)](https://www.youtube.com/watch?v=pi3YA3m1ffw)

Byzantine Agreement is an important problem to address in a Distributed Network. It is all about being tolerant of the nodes that are malicious and trying to ruin the sanity, integrity, and correctness of the network.

In this video, we talk about an algorithm that gathers an exponential amount of information to build a robust understanding of different values proposed, before reaching a consensus even when a few nodes are corrupt and are trying to ruin everything.

Outline:

00:00 Agenda
02:42 Introduction to Byzantine Agreement
03:53 EIG Algorithm and the flow
09:06 Decision for Byzantine Agreement

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1nJmizLh_HnHLiSNZH-k0JVFeMlypBbkj/view?usp=sharing)
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