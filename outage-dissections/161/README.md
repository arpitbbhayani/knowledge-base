Dissecting GitHub Outage - Multiple Leaders in Zookeeper Cluster
===


The split-brain problem in Distributed Systems is not theoretical. GitHub had an outage because their Zookeeper cluster ended up having two leaders, leading to writes to Kafka failing.

Zookeeper is an essential component for Kafka as the clients connect to get information about the brokers and cluster internally using it to manage its state.

## What happened?

During scheduled maintenance the Zookeeper nodes were getting upgraded/patched and during this time, many new nodes were added "too quickly" to the zookeeper cluster.

With a lot of new nodes added "too quickly", they were unable to self-discover or understand the topology and the way the bootstrap code of Zookeeper is written, they thought the cluster was leaderless. This made them trigger a Leader Election.

Given that a lot of new nodes were added, they formed the majority and elected a new leader. These nodes formed a logical second cluster operating independently. Thus the cluster is now having a split-leadership problem.

## Broker Connected

One of the Kafka broker (node) connected to the second cluster and found that no other nodes are present (because second zookeeper cluster had no entries) and hence elected itself as the controller.

When the Kafka clients (producers) were trying to connect to the Kafka cluster they got conflicting information which led to the 10% of writes failing.

If the number of brokers connecting to the new cluster were more, then it could have led to even data consistency issues. But because only one node connected, the impact was minimal.

## Recovery

The zookeeper cluster would have auto-healed but it would have taken a long time to converge, and hence a quick way to fix this is to manually update the zookeeper entries and configure it to have a single leader.

To keep things clean, the nodes that were part of second zookeeper cluster could have been deleted as well.

## Ensuring zero data loss

Even though 10% of write requests failed, why did it not lead to a data loss? the secret is Dead Letter Queue.

It is a very standard architectural pattern that ensures zero data loss even when the message broker (queue) crashes. The idea is to have a secondary queuing system that you can push messages to if the write on the primary fails.

All the messages that client tried to write to Kafka failed, but they were persisted in DLQ which they processed later.

## Key Learnings

- Make consumers idempotent
- Automate cluster provisioning
- Have a DLQ for all critical queueing systems
- Have retries with exponential back-offs on clients
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage - Multiple Leaders in Zookeeper Cluster](https://i.ytimg.com/vi/bycFzB6yrK0/mqdefault.jpg)](https://www.youtube.com/watch?v=bycFzB6yrK0)

Distributed Systems are prone to problems that seem very obscure. GitHub had an outage because a set of nodes in the Zookeeper cluster ran an election and elected a second leader. How obscure is that?

In this video, we dissect a GitHub outage that would tell us how weird is the world of Distributed Systems. We also talk about Zookeeper and its importance for managing a Kafka cluster. We see what happened during the outage, and how GitHub was able to mitigate it with ZERO data loss and a brilliant fallback strategy.

Outline:

00:00 Agenda
02:37 Zookeeper and Kafka
05:27 What happened
06:25 Bootstrapping Zookeeper Node and Leader Election
09:06 Broker connecting to the new cluster
14:05 Recovery
15:55 Dead Letter Queue and Fallback Strategy
18:07 Key Learnings

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1ut8trVZ5IF4hB6amfKpZSzPJl_8eRiCk/view?usp=sharing)
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