Dissecting GitHub Outage: Downtime due to an Edge Case
===


An edge case took down GitHub 🤯

GitHub experienced an outage where their MySQL database went into a degraded state. Upon investigation, it was found out that the outage happened because of an edge case. So, how can an edge case take down a database?

## What happened?

The outage happened because of an edge case which lead to the generation of an inefficient SQL query that was executed very frequently on the database. The database was thus put under a massive load which eventually made it crash leading to an outage.

### Could retry have helped?

Automatic retries always help in recovering from a transient issue. During this outage, retries made things worse. Automatic retries added the load on the database that was already under stress.

## Fictional Example

Now, we take a look at a fictional example where an edge case could potentially take down a DB.

Say, we have an API that returns the number of commits made by a user in the last `n` days. The way, this API could be implemented is to get the `start_date` as an integer through the query parameter, and the API server could then fire a SQL query like

```
SELECT count(id) FROM commits
WHERE user_id = 123 AND start_time > start_time
```

In order to fire the query, we convert the string `start_time` to an integer, create the query, and then fire it. In the regular case, we get the correct input and then compute the number of commits and respond.

But as an edge case, what if we do not get the query parameter or we get a non-integer value; then depending on the language at hand we may actually use the default integer value like `0` as our `start_time`.

There is a very high chance of this happening when we are using Golang which uses `0` as the default integer value. In such a case, the query that gets executed would be

```
SELECT count(id) FROM commits
WHERE user_id = 123 AND start_time > 0
```

  
The above query when executed iterates through all the rows of the table for a particular user, instead of the rows for the last 7 days; making it super inefficient and expensive. The above query would put a huge load on the database and a frequent invocation can actually take down the entire database.

### Ways to avoid such situations

1. Always sanitize the input before executing the query
2. Put guard rails that prevent you from iterating the entire table. For example: putting `LIMIT 1000` would have made you iterate over 1000 rows in the worst case.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Dissecting GitHub Outage: Downtime due to an Edge Case](https://i.ytimg.com/vi/iqapVyfoFqc/mqdefault.jpg)](https://www.youtube.com/watch?v=iqapVyfoFqc)

In August 2021, GitHub experienced an outage where their MySQL Master database went into a degraded state. Upon investigation, they found out it was due to an edge case. So, how can an edge case take down a database?

In this video, we understand what happened, take a fictional example of how an edge case can put extra load on the database, and conclude with an exciting way to make our SQL queries fool-proof.

Outline:

00:00 Agenda
00:27 Outage Overview
07:38 What could have happened?
08:51 A fictional example of an edge case taking down DB
17:18 How to avoid edge cases on SQL queries

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1PI302Cvutu8LJKmZu7fiIVOAqRhiSMek/view?usp=sharing)
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