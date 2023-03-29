Dissecting GitHub Outage Downtime due to creating an Index
===


Imagine you created an index on a table and instead of boosting the performance, it lead to an outage 🤦‍♂️ GitHub ran a migration to reverse an index and it lead to a 60 mins outage.

Note: The example we have taken is pure speculation, the official incident report had minimal information about the outage. But the write-up will make you aware of possible challenges that might come during such situations.

## Reverse an index

Reversing the order of the index is done when we have a multi-column index and the query requires different sorting orders on them; for example, `DESC` on `date` and `ASC` on `user_id`.

For a query to be optimally executed on the database, we would need an index that physically stores the index ordered by the `date` in the descending order and `user_id` in the ascending order.

MySQL by default stores any index in `ASC` order and hence, GitHub had to run the migration to reverse the order of the index and gain a boost.

## What could go wrong?

A reverse index would require a Full Table Scan during the creation putting a load on the database. Also, upon changing the order of the index, it is possible we overlook another query that is more frequent but optimal with the old order.

The database does its best to create an optimal execution plan and it might not use the reverse index we just created. We can solve this by specifying Index Hints like `USE INDEX` and `FORCE INDEX`, ensuring that it uses our index to evaluate the query.

## Cascading Effect

Because one of the queries was doing a Full Table Scan, it put a load on the database which had a cascading effect on the service eventually propagating to the end user. All the intermediate services will timeout giving a degraded experience to the user.

## Key Takeaways

### Never blindly trust ORM

ORMs are designed to make our lives simpler but they might not generate the most optimal queries, and hence it is always better to periodically audit the queries and ensure they are optimal.

Poorly generated queries will put a load on the database choking the entire performance.

### Check the query execution plan

While updating a query or changing a schema always check the query execution plan. We can get the execution plan for any query using the `EXPLAIN` statement.

The diff in the plan would give tell us if any of our queries would perform a full table scan.

### Audit the queries and indexes

Keep an inventory of the queries we fire and the indexes it uses during execution. So, whenever we change any index, we can quickly run an audit and ensure zero regressions.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage Downtime due to creating an Index](https://i.ytimg.com/vi/df2QgLW0QC4/mqdefault.jpg)](https://www.youtube.com/watch?v=df2QgLW0QC4)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

GitHub wanted to optimize their SQL query performance, and they had to reverse a database index. Instead of getting a performance boost, thy incurred a downtime of more than 60 minutes. Imagine the state of the team who wanted to do good, but were stuck in this fix.

This outage gives us a super-in-depth insight into MySQL and its indexing structure. It is indeed fascinating to see the kind of optimizations engineers have to make while operating at scale.

In this video, let's dissect this outage and understand what happened, why GitHub had to flip their index, how things went wrong and affected end users like us, and conclude with 3 key takeaways from this outage.

Outline:

00:00 Agenda
02:47 What happened?
03:52 Need of Reversing an Index
07:21 What could go wrong during and after Indexing?
14:52 Cascading Failures
17:16 Mitigation and Key Takeaways

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1JrtyE2wt9ikic3iOTy36NYKxEPESMt4a/view?usp=sharing)
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

<img width="256px" src="https://edge.arpitbhayani.me/img/arpit.jpg" />

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