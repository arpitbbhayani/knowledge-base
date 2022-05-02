Database Sharding and Partitioning
===


Sharding and partitioning come in very handy when we want to scale our systems. Let's talk about these concepts in detail.

# How is the database scaled?

A database server is just a database process (like MySQL, MongoDB) running on a virtual server like EC2. Now when we put our database in production it starts getting from real good traction, say 100 writes per second (WPS).

### Steady user growth

Say, your product started getting some traction, and we find that the database is not able to handle the load, we scale it up by adding more CPU, RAM, and Disk to the server. This way we are now handling 200 WPS.

### More read traffic  

If we see nor reads then can also choose to add a Read Replica and divert some of the read traffic to this node, while the master node can take in 200 WPS.

### Viral Growth

Say, your product went viral and you now got 5x more load which means now you have to handle 1000 WPS. To achieve this you again scale it up vertically and handle the desired load.

### Insane growth

Say, you now cracked the PMF and are getting some really solid traction and need to handle 1500 WPS, and when you visit the database console you found out that it is not possible to vertically scale your database any further, so how do you handle 1500 WPS?

This is where the horizontal scaling comes into the picture.

## Scaling the database horizontally

We know one database server can handle 1000 WPS, but we need to handle 1500 WPS, so we split the data into half and split it across two databases such that each database owns half of the data and all the writes for that data goes to that particular instance.

This way each server will get 750 WPS, which it can very easily handle, and owns 50% of the data. Thus by adding more database servers we handled 1500 WPS (more than what a single machine could handle)

# Sharding and Partitioning

Each database server in the above architecture is called a Shard while the data is said to be partitioned. Overall, a database is sharded and the data is partitioned.

## Partitioned data on shards

It is possible to have more partitions and fewer shards and in that case, each shard will own multiple partitions. Say, we have 100GB of data and it is split into 5 partitions and we have 2 shards. One shard will be responsible for 3 partitions while the other for 2.

# Advantages and Disadvantages

### Advantages of Sharding

- handle more reads and writes
- increases overall storage capacity
- overall high availability

### Disadvantages of Sharding

- sharding is operationally complex
- cross-shard queries are super-expensive
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Database Sharding and Partitioning](https://i.ytimg.com/vi/wXvljefXyEo/mqdefault.jpg)](https://www.youtube.com/watch?v=wXvljefXyEo)

Sharding and partitioning come in very handy when we want to scale our systems. These concepts operate on the database and help us improve the overall throughput and availability of the system.

In this video, we take a detailed look into how a database is scaled and evolved through different stages, what sharding and partitioning are, understand the difference between them, see at which stage should we introduce this complexity, and a few advantages and disadvantages of adopting them.

Outline:

00:00 Introduction and Agenda
03:05 How a database is progressively scaled?
08:10 Scaling beyond the limit of vertical scaling
11:57 Sharding vs Partitioning
12:43 Example of Data Partitioning
17:15 Sharding and Partitioning together
20:20 Advantages and Disadvantages of Sharding and Partitioning

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/14RqKYjN2pgqYTaVB1DYlH4WjZ0A8XQ02/view?usp=sharing)
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