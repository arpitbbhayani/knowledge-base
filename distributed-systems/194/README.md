Two Phase Commit to power Distributed Transactions in a Distributed System
===


Say, we have a distributed database with three nodes, and we want our "commit" to succeed when it is successful in all three nodes otherwise we "abort".

This is a classic Distributed Transaction.

Assumptions:

- no messages are lost
- processes can fail in the middle of the transaction
- every node knows about every other node in the network

## Two-Phase Commit

Say have the transaction, and N processes are participating. One of the `N` processes becomes the coordinator and it coordinates until the end of the protocol.

### Phase 1

All the nodes send if they can `commit` or `abort` to the coordinator process. If a process does not send any information, the coordinator will mark it as `abort`.

At the end of phase 1, the coordinator will have the local decisions of all the nodes. The coordinator decides `commit` if all the nodes can `commit`, otherwise the decision is `abort`.

### Phase 2

Process A broadcasts its decision to all the nodes in the network, and thus the entire network either commits or aborts; thus completing the transaction.

## Failure Scenarios

If the coordinator fails before the start of phase 1, then since the consensus did not even start, all the nodes can safely abort.

If the coordinator fails after initiating phase 1, some of the nodes might have sent their local decision and would be waiting to hear back the final decision. These nodes would remain blocked.

If a participant crashes before sending its local decision to the coordinator, then the coordinator keeps on waiting for the local decision.

If the coordinator and one participant crash in phase 2 without other participants knowing anything about the decision then the new coordinator that comes up would have no idea about the decision.

No one could proceed, because the new coordinator does not know if the crashed node was committed or aborted.

The Two-Phase Commit looks super-simple but it has a major flaw in the failure scenarios, and hence distributed systems take even finer steps to remediate and reach a consensus more robustly.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Two Phase Commit to power Distributed Transactions in a Distributed System](https://i.ytimg.com/vi/sZVCpjuVUL8/mqdefault.jpg)](https://www.youtube.com/watch?v=sZVCpjuVUL8)

Distributed Transactions are the heart and soul of Distributed Systems and getting all the participating nodes to agree to commit or abort is not an easy job.

In this video, we talk about the Two-Phase Commit protocol that takes baby steps to ensure that we can get all the nodes to commit or abort a distributed transaction and never let the data go into an inconsistent state.

Outline:

00:00 Agenda
02:30 Two Phase Commit
08:37 Failure Scenarios in 2PC

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1FJa0DQPOxVJP2kXdyZDSttdMDI4Q2fUx/view?usp=sharing)
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