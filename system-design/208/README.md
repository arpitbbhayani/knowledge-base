How Booking com designed and scaled their highly available and performant User Review System
===


The review system for Booking is one critical service as it drives business and hence making it highly available becomes extremely crucial.

Here's a thread about building a highly available system and the architecture of Booking's Review Service 👇‍

## Importance

Review shown on Booking.com are authentic and it helps people make a decision and thus bring in revenue.

The review system is also a high-throughput system as people can land on it from Search Engines or internal navigation.

## Review API Service

The core Review Service will be a simple REST-based API that exposes endpoints to create, read, update, and delete reviews.

Review Service of Booking handles 10,000 requests per second at peak with p99 of 50ms.

Given that the latncy requirement is too stringent, Booking serves most of the review from a centralized remote Cache and has done a bunch of optimizations on the Database through materialized views.

## Configuring storage

Booking.com has 250 million reviews and given the amount of info a review holds, they store these reviews in a shared datastore. 

Given Booking needs storage to be highly available, they configured each database to have multiple replicas and that too across regions to tolerate regional outages.

## Auto-scaling Storage

Given that the traffic for a travel business surges during the holiday season, the database needs to be scaled up to handle the load.

But keeping the database scaled up throughout the year without much load is very inefficient and hence Booking.com required some so of storage autoscaling.

Scaling up and down a sharded database requires us to add and remove nodes; but doing this naively requires the data to be re-partitioned.

To keep the movement to a bare minimum during scaling, Booking.com chose Consistent Hashing for determining data ownership.

## Architecture

1. Review Service is a simple REST service
2. Centralised cache and materialized views for quicker response
3. Database is sharded to handle larger loads
4. Data ownership is determined by Consistent Hashing
5. Database is replicated across within and across regions for HA
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Booking com designed and scaled their highly available and performant User Review System](https://i.ytimg.com/vi/BFyWl9MNDjY/mqdefault.jpg)](https://www.youtube.com/watch?v=BFyWl9MNDjY)

Designing a highly available and performant service is really difficult but booking.com does it really well. The rating and review service is one of the most critical services for Booking and in this video, we dive deep into how they designed and scaled it to ensure they seamlessly handle peak traffic of more than 10,000 requests per second.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1oxo-BsAUbqCGnfCjYTqw82kpLU1OZ_Cw/view?usp=share_link)
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