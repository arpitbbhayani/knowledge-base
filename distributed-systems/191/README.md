FloodSet Algorithm - Distributed Consensus even when processes crash
===


Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

Reaching a consensus

- is impossible when the network is unreliable
- is simple when there are no network/process failures
- is tricky when we have to deal with process failures

## FloodSet Algorithm

The core idea of the FloodSet algorithm is to keep track of all the values seen so far and use some decision rule such that all nodes choose the same value.

Every node maintains a set `W` to hold all the values seen so far. If we assume at max `f` nodes would fail then the FloodSet algorithm runs for `f + 1` rounds, giving chances for processes to fail.

Every node starts with `W = {v}`, its own value. In each round, every node broadcasts `W` in the network. When a node receives the `W` from other nodes it updates its `W` by doing a set union.

After the `f + 1` rounds, every node will have the same `W` that holds all possible values of the network participating in the transaction.

### Decision Making

The decision-making is decentralized. If `W` contains just one value then the node converges to that value. If it contains more than one value, the node defaults to the last value.

This decision-making is use-case specific, so defaulting to the old value can mean that the transaction is aborted and the node is reverting to the old value.

### Alternative Decision Strategy

Depending on the usecase, we may choose another decision strategy like picking the smallest value or the largest value or the oldest value, or the newest value.

So long as we have a total ordering of the values, we can define our own decision strategy.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![FloodSet Algorithm - Distributed Consensus even when processes crash](https://i.ytimg.com/vi/uS19mAa_tFA/mqdefault.jpg)](https://www.youtube.com/watch?v=uS19mAa_tFA)

Reaching a consensus is extremely critical in a Distributed System as we would have situations day-in and day-out where we need nodes to agree upon a common value. The tricky part here is to achieve agreement even when the nodes participating in the consensus crash.

In this video, we talk about the simplest algorithm called the FloodSet algorithm that helps us achieve fault-tolerant Distributed Consensus, look at how it fits into the real world, and talk about the complexity it incurs.

Outline:

00:00 Agenda
02:32 Distributed Consensus
04:09 Problem Statement
06:58 FloodSet Algorithm
12:22 Alternate Decision Strategy
14:34 Complexity Analysis

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1RnSNfalo0RiwFqeYYd5Dy03of8_AXvI7/view?usp=sharing)
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