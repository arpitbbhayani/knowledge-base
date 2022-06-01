Database per Service Pattern in Microservices
===


Should every microservice have its own database?

Microservices need some persistence to store the state of the application. They also need to be loosely coupled with others so as to be autonomous and having a separate database for itself really helps, and this is the Database Per Service pattern.

## Modeling a social network

The importance of having a database per service can be seen when we model a social network. For every usecase, we would need a specialized database to keep our latencies to a bare minimum.

- Chat: a partitioned non-relational database like Cassandra
- Auth: a simple relational database with replicas like MySQL
- Profile: a nonrelational schemaless database like MongoDB
- Analytics: a massively scalable columnar storage like Redshift
- Videos: blob storage like S3

## Advantages of Database Per Service Pattern

### Loosely coupled components

Because the databases are separate, the services could not connect to other databases and would have to directly talk to each other making them loosely coupled.

### Specific DB for specific usecase

Services can pick the best database for their usecase making them super performant and efficient. For example, picking a Graph database to model relations in social networks instead of relational.

### Granular control and scaling

Services can choose their scaling strategies as per the load it is getting; be it vertical, horizontal, replicas, partitioned, or decentralized.

### Smaller blast radius

When any database is experiencing an outage only the services that are directly or indirectly dependent on it get affected and everything else continues to operate normally. For example, we can continue to accept the payments even when the profile service is down.

### Compliance

Compliance requires us to make changes in how our data is stored and moved across. Separate databases would help us in implementing changes on a fraction of data instead of the whole.

## Downsides of Database Per Service Pattern

### Transactions are distributed and expensive

If we need strong consistency across, we would need distributed transactions and those are expensive and complex to implement.

### Conveying updates requires brokers

Conveying updates from one service to another would require us to have message brokers, thus adding more things to manage and maintain.

### More infra to manage

Having a database per service bloats up our infra and we would need to build expertise in maintaining and managing them.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Database per Service Pattern in Microservices](https://i.ytimg.com/vi/la2q1vFA5q0/mqdefault.jpg)](https://www.youtube.com/watch?v=la2q1vFA5q0)

Microservices should be loosely coupled and autonomous so that they can take their own decision and be as performant as they can be. A high-level architecture pattern that allows us to achieve this is the database-per-service pattern in which each microservice owns its database and take independent decisions about it.

In this video, we quickly talk about the database-per-service architecture pattern, look at how it helps in modeling massive systems, understand the advantages of adopting it, and conclude by going through some drawbacks of this architecture pattern.

Outline:

00:00 Agenda
02:39 INtroducing Database Per Service Pattern
04:02 Modeling Social Networks
07:33 Advantages of adopting Database Per Service Pattern
16:22 Downsides of adopting Database Per Service Pattern

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1D7bEh7tacBZsBxzxnVbH4OvFuTOgY-yh/view?usp=sharing)
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