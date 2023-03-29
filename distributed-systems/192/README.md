Exponential Information Gathering (EIG) Algorithm - Distributed Consensus even when processes crash
===


Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

Reaching a consensus

- is impossible when the network is unreliable
- is simple when there are no network/process failures
- is tricky when we have to deal with process failures

## EIG Algorithm

The core idea of the Exponential Information Gathering Algorithm is to gather a large amount of information from the network and then apply some decision rules to reach a consensus.

## EIG Data Structure

EIG algorithms require an EIG Tree that is like a Trie and is constructed level by level. If there are `n` nodes in the network and the level of the tree is `k` then the leaf of the tree contains all k-length permutations of `n` nodes.

If a node `a` received a message from a path `b, c, d` then the incoming message (value) is stored along the path `b`, `c`, `d` at the node `a`.

Thus, at each level of the tree, the number of children of each node reduces by 1. The root of the tree is labeled EMPTY, and it has `n` children, say A, B, and C.

Each node in the next level will have 2 children. A will contain `AB` and `AC` while `B` will contain `BA` and `BC`, and `C` will contain `CA` and `CB`. Thus we see at level 2 the leaves contain all 6 2-length permutations of A, B, and C.

## Algorithm

We assume at max `f` nodes would fail and hence the algorithm runs for `f + 1` rounds. In each round, a new level of EIG Tree is constructed. Each node independently constructs the level but every single node will have formed the exact same EIG Tree.

### Round 1

Every process `i`, sends its value to the entire network including itself. Upon receiving the value `v` from `j`, the nodes update their own trees and add nodes `tree[j] = v`.

At the end of round 1, every node will have an EIG tree of depth 1.

### Round > 2

Every process `i`, sends all pairs `(x, v)` from the `k - 1` level in the network where `i` is not in `x`. This would lead to the construction of the permutation tree.

After the `f + 1` rounds, each node will have the exact same copy of the EIG Tree of depth `f + 2`.

### Decision Rule

The algorithm stops after the `f + 1` rounds, and each node simply traverses through the entire EIG Tree to find all distinct values it holds.

If the number of values is 1, the node decides that as the final value. If the distinct values are many, then the node may choose the default value.

This decision-making is use-case specific, so defaulting to the old value can mean that the transaction is aborted and the node is reverting to the old value.

### Alternative Decision Strategy

Depending on the usecase, we may choose another decision strategy like picking the smallest value or the largest value or the oldest value, or the newest value.

So long as we have a total ordering of the values, we can define our own decision strategy.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Exponential Information Gathering (EIG) Algorithm - Distributed Consensus even when processes crash](https://i.ytimg.com/vi/1g0L6ISxQPE/mqdefault.jpg)](https://www.youtube.com/watch?v=1g0L6ISxQPE)

Exponential Algorithms have to be the worst possible way to solve Distributed Consensus; but are they really that bad?

In this video, we talk about an exponential, expensive yet important algorithm to achieve distributed consensus named EIG algorithm that gathers an exponential amount of information and then reaches a consensus. Although a little expensive, but this algorithm is critical in laying the foundation for Blockchain to make them resilient to malicious users.

Outline:

00:00 Agenda
02:35 Introduction to Distributed Consensus
03:43 EIG Data Structure
08:09 EIG Algorithm
18:46 Alternative Decision Strategy

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1hrBtQP4hDpjcVPEWBsExPzYDAeAW5jW1/view?usp=sharing)
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