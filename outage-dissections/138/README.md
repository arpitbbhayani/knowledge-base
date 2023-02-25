Dissecting GitHub Outage - Downtime due to ALTER TABLE
===


Can an ALTER TABLE command take down your production? 🤯

It happened to GitHub on 27th November 2021 when most of their services were down because of a large schema migration.

## Why did the outage happen?

GitHub ran a migration on a massive MySQL table and it made their replicas enter deadlock and crash. Here are the 5 insights about their architecture

### Insight 1: Schema migration can take weeks to complete

Schema migrations are intense operations as in most cases require you to copy the entire table with the new schema. Hence it might take a schema migration weeks to complete.

### Insight 2: The last step of migration is RENAME

To protect the database from not taking excessive locks during the migration, we create an empty ghost table from the main table, apply migration, copy the data, and then rename the table. This reduces the locks we need for the migration.

### Insight 3: Read Replicas can have deadlocks

The writes happening through the replication job and the production read load can create deadlocks on the read replicas.

### Insight 4: Have a separate fleet of replicas for internal traffic

Have a separate fleet of Read Replicas for internal workflows ex: analytics, etc. This way, any internal load will not affect the production load.

### Insight 5: Database failures cascade

When a replica fails, the load on healthy one's increases; which may them down and hence the cascading effect.

## Mitigation

The outage happened because there were not enough read replicas to handle the load, hence in order to mitigate it the way out was to add more read replicas. GitHub team very smartly promoted the replicas used for internal workloads to handle production.

Although the move was smart, it did not mitigate the outage because the incoming load was so high that the new replicas added also started crashing.

### Data Integrity over Availability

To ensure that the data integrity is not compromised because of repeated crashes, GitHub took a call and let the Read traffic fail. They took the replica out of the production fleet, gave it time to complete the migration, and then added it back.

This way all the replicas got the time they needed to complete the schema migration. It took some but the issue was completely mitigated.

## Long-term fix

Vertical Partitioning is a long-term fix for this problem. The idea is to create smaller databases that hold related tables; ex: all tables related to Repositories can go in one DB. This allows migration to quickly complete and during an outage, only the involved functionalities will be affected.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage - Downtime due to ALTER TABLE](https://i.ytimg.com/vi/82Xywy74kfE/mqdefault.jpg)](https://www.youtube.com/watch?v=82Xywy74kfE)

Can an ALTER TABLE command take down your production? 🤯

GitHub had a major outage and it all started with a schema migration. The outage affected their core services like GitHub actions, API requests, pull requests, and many more. Today, we dissect this outage and do an intense deep dive to extract 5 amazing insights. We also see how they very smartly mitigated the outage along with a potential long-term fix. 

Outline:

00:00 Agenda
02:57 Introduction
03:23 Insight 1: Schema Migrations can take weeks to complete
05:48 Insight 2: How schema are altered when the table is huge
08:52 Insight 3: Deadlocks on Read Replicas
11:20 Insight 4: Separate Replica fleet for internal read traffic
13:59 Insight 5: Database failures cascade
18:13 Mitigation Strategy
29:28 Lont-term Fix

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/14jdP8o2wFZYL0iFtsCbqKr3jEX0QstaY/view?usp=sharing)
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