Dissecting GitHub Outage - Master failover failed
===


Master failover failed for GitHub leading to a 5-hour long incident, let's see what happened.

## Incident Summary

For five hours, GitHub users observed delays in data being visible on the interface and API after it was written on the database. This happened during the maintenance when they were switching the Master DB.

## Planned Maintenance

Planned maintenance is a popular way for companies to take a small downtime and execute all the maintenance activities. Some activities for which we do plan database maintenance are

- applying security patches
- apply version upgrades
- parameter tuning
- hardware replacement
- periodic reboots

A popular activity during database maintenance is to switch the Master node i.e. shift the traffic coming from the master node to a new node so that we could patch the old instance.

For a very short duration, when the config switch is happening, the database would be unavailable leading to a small outage; and this is expected behavior.

## Database Crash

During the failover, when the traffic was moved to the new database, the `mysqld` process crashed. This led to incoming writes failing. To quickly mitigate the issue, the team moved the traffic to the old database. This solved the issue and the site was up and running.

## Something interesting happened

The new database before crashing served the write traffic for 6 seconds. So, after the crash when the traffic was redirected to the old database, it did not have the data that was written in that 6 seconds window.

This is a huge concern, as it would lead to bad UX, and in the worst case consistency failures. So, how to remediate this issue?

## Remediating master failovers

In order to remediate this, we take the help of the Write Ahead Log or Commit log of the database. Whenever we do a failover, we always keep track of the `BINLOG` coordinates.

Once we moved the traffic to the old database, all we have to do is iterate through the BINLOG and apply all the changes that happened on the new database post the noted coordinate on the old database.

This would re-create or modify the exact data that was written to the new database on the old database, leading to zero data loss or consistency breach.

## Cleaning up the mess

Typically when we have such a failover, it is better that we restore the read replicas and hence GitHub team rotated all the replicas. Creating a read replica takes time, given the scale of GitHub.

It took them 4 hours to set up replicas and 1 hour to re-configure the cluster hence for over 5 hours the incident was affecting the users.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Dissecting GitHub Outage - Master failover failed](https://i.ytimg.com/vi/ZirBDq1JwpY/mqdefault.jpg)](https://www.youtube.com/watch?v=ZirBDq1JwpY)

Companies announce their planned maintenance, what happens during that? Could something go wrong while running maintenance?

GitHub team was switching their Master databases from one node to another; while doing this something went wrong and the new database crashed. This led to data divergence and a production incident that lasted over 5 hours.

In this video, we dissect this incident and understand what happens during planned maintenance, what went wrong with GitHub, how GitHub mitigated it, and understand some really cool things about switching databases and solving data divergence.

Outline:

00:00 Agenda
02:42 What happened?
03:29 Scaling reads with Read Replicas
04:40 Planned Database Maintenance
10:08 Database crashed and quick mitigation
11:44 Data Divergence between two masters
13:54 Remediating Data Divergence
18:23 Read Replica taking time to spin up

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1uzicMXBufPqkPTzrxyQOS6zn1x6WURwi/view?usp=sharing)
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