GitHub Outage  - How databases are managed in production
===


Managing databases in production is not easy and it does require a lot of tooling to keep it up and running. GitHub had an outage that gives us a glimpse of the toolings they use in production. So, here's what happened

## Incident Summary

The GitHub team updated the ProxySQL and a week later a master node in a critical database cluster crashed. A replica was promoted as the new master, and it also crashed. The team tried to manually recover, but the manually promoted replica also crashed.

Finally, the GitHub team did a full revert - reverted all the code changes, and also downgraded the ProxySQL version. Post this, things become normal and the master did not crash.

## ProxySQL

ProxySQL is a database proxy that sits between the servers and the database cluster. The server seamlessly connects to the ProxySQL and fires the usual SQL queries and the proxy forwards it to the data node as per the configuration.

### Why do we need ProxySQL

- better connection management
- as a cache for SQL query responses
- a gatekeeper to handle security and routing

## Orchestrator

Orchestrator is a MySQL topology management tool that helps us achieve High Availability on a MySQL cluster. It keeps an eye on all the nodes and takes corrective actions whenever something goes wrong.

We configure Orchestrator to keep an eye on the master node and as the node crashers, it promotes a replica to become the new master. Given that all of this happens automatically, it just takes a few seconds for the cluster to recover from the master crash.

### Anti-flapping policy

A very common cascading failure happens when the master fails and a replica is promoted to be the new master. Due to the high load, say the new master also crashed. The cycle thus continues until all nodes crash leading to a complete outage.

The anti-flapping policy of Orchestrator prevents this complete outage by not promoting replica to master until the cool-off period ends. Once the replica is promoted to be the new master, Orchestrator does not promote another replica until the cool-off period ends.

Although the master is down, this anti-flapping policy ensures that we are at least partially functional and can continue serving some reads. Along with this, we see only a small subset of nodes are thrown in the fire and hence have fewer data nodes to recover.

## Mitigation

To mitigate the issue, the GitHub team

- reverted the ProxySQL version
- reverted the code that required an upgraded version of ProxySQL

With this full revert, the master node stopped crashing and things become normal again.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![GitHub Outage  - How databases are managed in production](https://i.ytimg.com/vi/4mVJQJbw6Vw/mqdefault.jpg)](https://www.youtube.com/watch?v=4mVJQJbw6Vw)

So, how are databases managed in production? When the master goes down, how a replica is chosen and promoted to be the new master? Is this a manual step or something that can be automated?

In this video, we dissect yet another GitHub outage and apart from understanding what happened, we would spend a significant amount of time learning how databases are managed in production, and the kind of tools companies use to ensure optimal DB performance and High Availability.

Outline:

00:00 Agenda
02:39 What happened?
03:20 ProxySQL and why it is used in production?
09:14 Orchestrator and what it does?
14:12 Anti-flapping policy of orchestrator
18:10 Root cause and mitigation
19:46 Key takeaways

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1Fqad5kpmlvrNMFXSojlOvBwOAOu7c2nd/view?usp=sharing)
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