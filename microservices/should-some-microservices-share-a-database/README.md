Should some microservices share a database?
===


Microservices need to communicate with each other, and one such way of doing it is through a shared database.

For example: While building a multi-user blogging application, say we have a Blogs service that manages all the blogs-related information and we have an Analytics service that takes care of all the analytics like Likes, Shares, Views, etc.

Analytics service updates the information asynchronously directly in the blog's database; eg: total_views that happened on the blog. This can be easily achieved by sharing the database between Blogs and Analytics, and this pattern is the Shared Database pattern.

### Advantages of sharing the database

- the simplest way of integration
- no middleman involved
- no latency overhead
- quick development time

# Challenges with Shared Database

There are 4 challenges to using this pattern

## External parties know internal details

By sharing the database across services, an external party (Analytics) would get to know the internal details of the Blogs service; eg: deletion practice, schema, etc.

This leads to a very tight coupling between the services; which then restrains the maintainability and performance of the system. For example, whenever the Blogs service changes the schema, the Analytics Service would have to be informed about the change.

## Sharing the database is sharing the logic

To compute some information we need to query a set of tables; and say, this information is required by the Blogs, Analytics, and Recommendation service.

The business logic to compute the information has to be replicated across all the 3 services. Any change in the logic needs to be made across all the services.

## Risk of data corruption and deletion

There is a risk that one of the services might corrupt or delete some data given that the database is shared between the services.

## Abusing the shared database

One service firing expensive queries on the database will affect the performance of other services sharing the same database.

# When to share a database?

A shared database pattern is helpful when you are seeking quick development time. Although it is not the best practice, sharing the database does reduce the development effort by a massive margin.

Sharing the database is also seen where it is inconvenient to have a middleman for the communication; for example: sending a notification to a million followers of a person is simple when the Relationship database is shared with the notification fan-out service; instead of iterating the millions of followers through some middleman API.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Should some microservices share a database?](https://i.ytimg.com/vi/tV11trlimLk/mqdefault.jpg)](https://www.youtube.com/watch?v=tV11trlimLk)

Microservices need to communicate with each other. Communication between them is always about getting or updating data that is owned by the other service. What if a service gets direct access to all the data it wants? This is the simplest way for the microservices to communicate with each other, and this pattern is called Sharing the Database. The core idea here is to let anyone who needs the data from a service or wants to update something, can directly talk to its database - no middlemen needed.

Although most people think it is the wrong way of communication, we should not discard it completely. In this video, we talk about what this architecture pattern is, the 4 challenges associated with it, see ways to mitigate them, and understand when and where it could be beneficial for us to share the database rather than going through a middleman.

Outline:

00:00 Agenda
03:13 Introduction
04:14 Advantages of a sharing a database
06:55 Challenge 1: External parties getting internal details
10:30 Challenge 2: Replicating business logic
13:31 Challenge 3: Risk of data corruption and deletion
14:50 Challenge 4: Abusing the shared database
16:27 Should we share the database then?

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1ql0chRVpcjgV4Fv_MJTRaXbtIZ3QJwcI/view?usp=sharing)
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