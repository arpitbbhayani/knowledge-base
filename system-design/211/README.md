How @twitter keeps its Search systems up and stable at scale
===


Managing massive, talking hundreds of terabytes here, Search clusters is no joke, especially at @Twitter's scale.

To manage them efficiently, Twitter built a bunch of toolings, here's a quick gist about it 🧵👇

Twitter uses ES to power the search of tweets, users, and DMs. ES gives them the necessary speed, performance, and horizontal scalability.

Given massive adoption, they needed to ensure the efficiency, and stability of these clusters and provide some standardized way of access.

## Elasticsearch Proxy

The Twitter team built a simple proxy for Elasticsearch that transparently sits in front of the Elasticsearch cluster.

The proxy is an extremely simple and lightweight TCP and HTTP-based relay that...

in a standard way, captures all critical metrics like - cluster health, latency, success, and failure rates here; along with this we can also

- throttle when some client abuses
- apply security practices
- route to a specific node
- authenticate

## Ingestion Service

ES performance degrades when there is a massive surge in traffic. We typically see an

- increased indexing latencies
- increased query latencies

But it is a common usecase for Twitter to ingest massive data (tweets) every now and then, hence they tweaked the ingestion...

The write requests that come to the ES proxy are sent to Kafka. Consumers read from Kafka and relay them to the ES cluster.

Doing it asynchronously allows us to

- do batch writes
- and retry if the ES down
- consume at a comfortable pace
- slow down if ES is overwhelmed

## Backfill Service

Twitter has a constant need of ingesting 100s of TBs of data in the Elasticsearch clusters.

Doing massive ingestion through Map Reduce jobs directly on ES will take down the entire cluster and doing it through Kafka makes it unnecessarily granular;

hence a backfill service ...

The backfill indexing requests are dumped on an HDFS.

The requests are partitioned and read using distributed jobs and indexed in Elasticsearch.

A separate orchestrator computes the number of workers required to consume the indexing requests.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How @twitter keeps its Search systems up and stable at scale](https://i.ytimg.com/vi/dOyCq_mMtdI/mqdefault.jpg)](https://www.youtube.com/watch?v=dOyCq_mMtdI)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Search is one of the most important services for any product and at the Twitter scale, it becomes ultra important. But what does it take to maintain Search at scale, how can we ensure that the search service continues to function no matter what kind of load hits the service?

In this video, we dive deep into how Twitter built tooling around their Elasticsearch that helps handle massive surges in the search traffic, do real-time ingestion, and 100s of terabytes of back-fill.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/10Q3u6wvppumrooEZODudwRKp_sW_6M5q/view?usp=share_link)
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