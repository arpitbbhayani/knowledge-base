Unsolvable Distributed Consensus and The Two Generals' Problem
===


Reaching consensus is extremely important in any distributed network. For example, we cannot have two data nodes in a cluster where one thinks that `price` is `$1000` while the other thinks it is `$2000`.

So, we need the nodes to talk to each other and reach a consensus and converge on the true value of `price`. Reaching consensus is easy when there are no failures - no network failures, or process failures.

But, reaching a consensus becomes impossible when we cannot guarantee message delivery.

## Two Generals' Problem

Say, there are two generals - A and B - and they want to attack the enemy from two different directions. The only way to conquer the enemy is when both generals attack simultaneously. If only one attacks, then the enemy wins.

The generals communicate via foot soldiers. These foot soldiers can be captured by the enemy and hence the message that generals wanted to send to each other can be lost. So, how would generals coordinate the attack?

### When no messages are lost?

If the communication channel is reliable, then the generals all send each other messages to agree to attack and everyone responds/ack to everyone else, thus coordinating the attack.


## Real World Analogy

Committing to a distributed database. The commit should succeed when all the nodes of the database agree to commit. If anyone cannot commit then the commit cannot go through.

## When messages are lost

When general A sent a message to general B, what if B's response got lost? then general A would not know if it should attack or not.

Also, since B did not receive an ack from A, then it cannot decide if it should attack or not either.

This is where we see both generals will keep on waiting for an acknowledgment of an acknowledgment, purely because the communication channel is unreliable.

This is the class Two Generals' Problem where it is impossible to reach a consensus when the underlying communication channel is unreliable.

## How should the generals decide?

Generals, instead of sending just a foot soldier, can send multiple foot soldiers increasing the probability that at least one of them would go through.

This is like we are flooding an unreliable network to get our message delivered.

## But how do we do this in the Real World?

In the real world, hence we do not assume a completely unreliable network. Instead, we assume a certain fraction of messages will be lost - eg: 1 in 2. Hence to overcompensate we send 2 messages instead of one.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Unsolvable Distributed Consensus and The Two Generals' Problem](https://i.ytimg.com/vi/DnOlqghKJMY/mqdefault.jpg)](https://www.youtube.com/watch?v=DnOlqghKJMY)

Distributed Consensus is extremely important to build a robust distributed system; because it is very common for a bunch of nodes to have a need to agree upon a common value - like Leader Node, some secret value, some meta information, or a value of a key.

In this video, we understand why it is impossible to achieve consensus in a distributed system where the communication channel is unreliable through a real-world analogy called the Two Generals Problem.

Outline:

00:00 Agenda
02:35 Distributed Consensus
03:39 Two Generals' Problem
05:14 When networks are reliable
06:59 Distributed Consensus in Real World
08:13 When networks are unreliable
10:37 How should the generals decide?
12:25 How systems are built then?

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1IZorhAB-Dzq_CsLcqlKwHddY1iP-s9Nw/view?usp=sharing)
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