Why, where, and when should we throttle or rate limit?
===


## What is throttling?

Throttling is a technique that ensures that the flow of the data or the requests being sent at the target machine/service/sub-system can be consumed at an acceptable rate.

It is a defensive measure and 3 possible reactions could be

- slowing down the incoming requests
- rejecting the surplus requests
- ignoring the surplus requests

## Why do we need throttling in the first place?

- to prevent system abuse
- to allow the amount of traffic we could handle
- control the consumption cost
- prevent cascading failures leading to a massive outage

## Real-world use-cases for throttling

### To prevent catastrophic DDoS attack

When your service is under a DDoS attack the rate limiter acts as your first line of defense that could prevent the surplus request from reaching your system. It would only allow the requests to go through at the configured rate.

### To gracefully handle a surge of users

It is possible that your product goes viral and now you are seeing a genuine surge in users. Upon getting a genuine surge in users, the stateful components like databases and caches crash which takes down the entire site.

Rate limiter in this case will help in preventing the entire site from going down; although some users would see some error, like 429- Too many requests- your product will continue to seamlessly work for the other set of users.

### Multi-tiered limits

Say, you are running a CICD company and offer 3 tiers of pricing- Tier 1 offers 200 minutes of build time, Tier 2 offers 1000 mins while Tier 3 offers unlimited build time. An internal rate limiter can keep track of the build times consumed by a customer and reject the requests once the limit is hit.

### Ensure you are not over-consuming

Say, we are consuming a super expensive third-party API and we want to ensure that we are not using it beyond a certain number otherwise the cost will shoot up. An internal rate limiter can keep a check on this to ensure the surplus request does not go through.

### Not overwhelming an unprotected system

Hard deleting from a database is an expensive operation. If we are deleting a huge number of rows from the DB it may severely affect the performance of the DB and hence it is best done in a staggered way. An internal rate limiter can help us streamline the writing by spreading them uniformly across time.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Why, where, and when should we throttle or rate limit?](https://i.ytimg.com/vi/CW4gVlU0xtU/mqdefault.jpg)](https://www.youtube.com/watch?v=CW4gVlU0xtU)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

It is a common belief that a rate limiter is always external and is designed to prevent our systems from being abused by the external world, but this is not true. In this video, we understand what throttling is, why we need it in the first place and 5 use cases where external and internal rate limiters are super useful.

Outline:
00:00 Introduction
02:56 What is Throttling?
03:37 What rate limiter does when it gets a surge of requests?
06:39 Why do we need a rate limiter?
10:45 Usecase 1: Preventing catastrophic DDoS Attack
12:20 Usecase 2: Gracefully handling a surge in legitimate users
13:46 Usecase 3: Multi-tiered limits
15:42 Usecase 4: Not overusing an expensive vendor
16:48 Usecase 5: Streamlining deletes to protect an unprotected database

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/11lTCiIbRk0aRlEaebjSI1mU6g_hTAway/view?usp=sharing)
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