The architecture of Grab's data layer that serves millions of orders every day
===


Grab stores and processes millions of orders every day, here is the design of the systems that powers it ⚡

The architecture of Grab's order platform is divided into two main databases, one for transactional queries and the other for analytical queries.

The transactional database holds transactional data about the orders that serve as the single source of truth for ongoing orders. In contrast, the analytical database holds historical and statistical data and stores it for longer periods. This database is defined to be more efficient for read-heavy analytical queries.

## Design Goals

Given the critical role that databases play in any system, the most important criteria for a good design are stability, availability, and consistency.

Stability is critical as the database must handle high volumes of queries per second. Availability is important because the database stores orders and any downtime could lead to revenue loss. Consistency ensures that users receive updated information when performing transactional queries. Therefore, strong consistency is necessary for transactional queries, while eventual consistency is sufficient for analytical queries.

## Architecture

### DynamoDB as Transactional Database

Grab uses DynamoDB as its primary data store. DynamoDB offers strong consistency, scalability, and high availability, making it an ideal choice for transactional queries.

Grab uses key-value queries such as get, create, and update orders, and DynamoDB's internal partition balancing feature to handle spikey traffic loads and hotkeys.

The orders table in DynamoDB contains several key attributes, including order ID, the state of the order (ongoing, completed, or canceled), the time the order was created, and the user ID.

To optimize performance, a global secondary index was created on the user ID, which allows for quick retrieval of ongoing orders for a particular user. When an order is completed, it is automatically removed from the index to keep it lean.

Grab has also designed its schema to keep its global secondary index (GSI) lean and performant by removing entries from the index after three months of inactivity.

### MySQL as Analytical Database

For analytical queries, Grab uses MySQL as its Analytical database. It is partitioned by the created_at, ensuring minimal cross-partition queries, and it drops old partitions to keep the database lean and consistent.

### Sync between databases

Grab uses Kafka to handle asynchronous batch ingestion from DynamoDB to MySQL. All events from the order service are sent to Kafka, which then updates the analytics database.

## Conclusion

In conclusion, Grab's order platform is an example of a complex system that balances consistency, availability, and cost-effectiveness to process millions of orders every day. By separating transactional and analytical queries into two separate databases, using specialized processing units, and leveraging modern data storage technologies, Grab has built a system that is highly scalable, available, and cost-effective.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![The architecture of Grab's data layer that serves millions of orders every day](https://i.ytimg.com/vi/KeV4erIm47o/mqdefault.jpg)](https://www.youtube.com/watch?v=KeV4erIm47o)

Grab processes millions of Food and Mart orders every single day, and the most critical, but brittle part of the infrastructure is the database. Given how critical orders are to Grab, they have to ensure very high availability of the database while ensuring a very fast query time. So, how do they achieve this?

In this video, we take a look at the high-level architecture of the data layer of Grab's Order Platform and see the practices they follow to ensure high availability, stability, and performance at scale.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1L2CKh6YEC5oQoc8LUsT_IswlOkKygREW/view?usp=share_link)
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