The Architecture of Pinterest's Time Series Database - Goku
===


Pinterest built their own time-series database named Goku because existing databases did not fit their requirements, here is the architecture of it.

## Existing OpenTSDB setup

Pinterest used OpenTSDB to hold their time-series data but it didn't work very well at scale. The two key aspects that hurt them were

- Long GC Pauses
- Frequent process crash

## Challenges

1. OpenTSDB disk-based scans are inefficient
2. The data stored in OpenTSDB does not have a good compression
3. OpenTSDB is JSON based and hence very inefficient
4. OpenTSDB is distributed and for a query that spans multiple shards, it first collects the data in one node and then evaluates the query.

## Key Decisions

1. To make the scan efficient, Goku stores data in-memory
2. Goku uses Gorilla engine which gives 12x compression
3. Goku computes a partial response at each shard and then sends it to the proxy; thus doing a minimal data transfer.
4. Goku uses Thrift Binary protocol, much more efficient than JSON

## Architecture

Goku stores 24 hours' worth of data in-memory with a configured periodic flush to the disk. The most recent query is fired to this in-memory store for quick evaluation.

Goku is a shared time-series database and each shard may contain data from multiple time series. Each Goku instance holds Bucket Map within which the time-series data resides. Each bucket holds data for a 2-hour window.

The writes on each time-series data go to the bucket map, within which it writes to a mutable buffer. Once the window is done, the buffer becomes immutable.

During a query, the request comes to a Goku Proxy which, if required, fans it out to all the involved shards. Each shard does the computation on its share of data and sends the response back to the coordinator/proxy node.

The coordinator/proxy node aggregates the response and sends it back to the client, thus completing the operation.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![The Architecture of Pinterest's Time Series Database - Goku](https://i.ytimg.com/vi/tZPTpa3JcKA/mqdefault.jpg)](https://www.youtube.com/watch?v=tZPTpa3JcKA)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

It is extremely critical to continuously monitor the health of the services and infrastructure. We use Time Series Databases to hold the key vitals like CPU, RAM, Disk, Requests, Network IO, etc. Pinterest generates millions of data points every second and the existing Time Series Databases were not performant enough to meet their needs, hence they built one in-house.

In this video, we take a detailed look into the architecture and key design decisions that Pinterest took while designing their own in-house time series database named Goku.

Outline:

00:00 Agenda
02:44 Need for Time Series Database
03:49 Time Series Data Model
06:53 Challenges and Key Decisions
10:45 Architecture of Goku

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1AqR4FuiCZbjuHl5v5H4cVFi8CPJwcFWX/view?usp=sharing)
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