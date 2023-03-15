Implementing Vertical Sharding
===


Vertical sharding is fine, but how can we actually implement it? 🤔

## Vertical Sharding

Vertical sharding is splitting a database by the tables. Shards will hold a subset of tables. For example, all payments-related tables go to one shard, while all auth-related tables go to another.

So, how to implement it?

## Need for a configuration store

For our API servers to talk to the correct database we would need a configuration store that holds the information for all the tables mapped to the database server that holds it.

For example, the Users table is present on DB1 while Transactions on DB2

Whenever the request comes, the API servers first check the config to find which DB holds the table and then fire the SQL query to that specific database for the table.

### Reactive update

All API servers will cache the configuration to avoid an expensive network call to get the database ensuring we get a solid boost to the performance.

When a table is moved from one database server to another, the configuration will be updated and hence the changes would need to be reactively propagated to all the API servers. Hence our config store needs to support reactive communication.

This is where we choose Zookeeper which is resilient and battle-tested to achieve this.

## Moving tables

Say, we are moving table `T2` from database server DB1 to DB2. Moving the table from one server to another is done in 4 simple steps.

### Dump the table `T2`

We first dump the table `T2` from DB1 transactionally using the utility `mysqldump` that not only dumps the table data but also records the position in the `binlog`. This is like taking a point-in-time snapshot of the table.

### Restore the dump

We now restore the dump to database DB2. This way we will have a database server with the table `T2` containing data till a certain point in time.

### Sync table `T2` on DB1 and DB2

We now setup the replication from DB1 to DB2 specifically for sync changes happening on table `T2`. It is done through a custom job that will use the recorded `binlog` position and start syncing from it.

### Cutover

Once the table `T2` is synced with almost 0 replication lag on DB1 and DB2 we cutover. We first rename the table to `T2_bak` and update the config in Zookeeper.

As we rename the table any queries going to DB1 for table `T2` will start throwing "Table not found" errors, but as Zookeeper will propagate the changes to all API servers they would use DB2 to fire any query on table `T2`, thus completing the table movement.

This is how you can implement vertical sharding.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Implementing Vertical Sharding](https://i.ytimg.com/vi/9iAJjtvBwyI/mqdefault.jpg)](https://www.youtube.com/watch?v=9iAJjtvBwyI)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Sharding is super-important when you want to handle the traffic that cannot be handled through one server. Sharding comes in two flavors - Horizontal and Vertical. In horizontal sharding, we split the table by rows and keep them on separate servers. In vertical sharding, we distribute the tables across multiple database servers.

For example, keeping all the payments-related tables in one database server, and all the auth-related tables in another. Vertical sharding comes in super handy when we are moving from monolith to microservices. All this sounds simple yet awesome theoretically, but would we actually implement it?

In this video, we take an in-depth look, not at the theoretical side of vertical sharding, but at the implementation side of it. We will see how Vertical Sharding is implemented with minimal downtime and what are the exact steps to do it.

Outline:

00:00 Agenda
03:17 Introduction to Vertical Sharding
05:23 Implementing Vertical Sharding
05:55 Picking a configuration store
10:34 Moving a table from one server to another
18:58 Summarizing the overall flow

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1AxijzqfIksP_QOKc9eKhuXba7apUugCT/view?usp=sharing)
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