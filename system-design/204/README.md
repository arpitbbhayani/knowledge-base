The architecture of Yelp's in-house Search Engine - nrtSearch
===


Elasticsearch is a great search engine, but Yelp was not happy with its performance, so they built their own HTTP layer on top of Lucene. Here's the architecture of it...

## Why not Elasticsearch?

1. ES replication is naive. The operations that happen on the master are re-done on replicas; hence scaling is not cheap.
2. ES suffers from the Hot Node problem and requires manual moving of the shards across nodes to balance the load.
3. ES autoscaling is time-consuming and hence we always provision it for the peak load.

## Key features of Lucene

### Near Realtime Indexes

In Lucene, the data of an index is stored in an immutable structure called Segment. Once the segment is written it can be quickly copied to a replica, in near-real-time. Thus, replication does not require the Replicas to re-index the documents, making it super-efficient to scale out.

### Concurrent Search on Segments

Search in Lucene is parallelized on segments. Hence for a given search query, Lucene can make parallel searches across segments using multiple threads and compute the most relevant results. It helps in leveraging all the cores of the underlying hardware.

Elasticsearch lacks the above features and is expensive in most cases, and hence Yelp thought of writing their own performant HTTP layer on top of Lucene, similar to Elasticsearch; and they call it nrtSearch.

## Implementation Details

### gRPC and Protobuf

Instead of using standard JSON-based endpoints for communication, nrtSearch uses gRPC/protobuf-based endpoints, saving a ton of time spent in serialization and de-serialization of the data.

To support existing systems that understand JSON, nrtSearch also provides a REST server built using gRPC-gateway. This gives clients an option to talk over gRPC or REST.

### Quick Failovers

Failovers are painful with Lucene. A standard flow is to backup the index segments on S3 and when a new node spins up, download the required segments and start serving the request.

To make failover quicker, Yelp used EBS by AWS which is like pluggable storage. The index segments are stored on these EBS volumes.

When a node goes down, and a new node spins up, instead of downloading the segments from S3, the unaffected EBS volume is attached to the new node. This makes the recovery happen in seconds instead of minutes.

### Replication

When the new segments are created on the master node, the master notifies all the replicas about it. The replicas then fetch the newly created segments from the Master over gRPC and maintain an eventual sync.

## Performance Improvements

### Virtual Sharding

Search in Lucene happens over segments, and the worst we can do is spin one thread for searching over each segment. This is sub-optimal and hence, the segments are virtually sharded.

Search Threads are capped and the segments are grouped greedily into slices. One search thread is allotted to each slice, thus searching over multiple segments in one go.

This logical abstraction helps in maintaining consistent utilization of search threads for a given search request.

### Other improvements

1. Fetching document fields in parallel
2. Segment-level search timeout to maintain consistent SLA

## Migration from ES to nrtSearch

### Dark Launch

Instead of directly launching the nrtSearch to the public, it is important to test the correctness of the response on production data. Hence, the first phase of the launch is a Dark launch.

The idea is to serve the entire 100% of requests from Elasticsearch, but send 5% of the requests to the new nrtSearch. The responses of this 5% of the request are compared with the legacy system.

Once the difference is analyzed and confidence is built on the correctness, the percentage is increased to 10, 15, 20, and 50%.

### Phased Rollout

Once there was 100% confidence in nrtSearch, the changes were rolled out to the general users in a phased manner and this time the requests we exclusively bifurcated across Elasticsearch and nrtSearch.

The initial percentage was 5%, eventually increasing it to 100% and then plugging out the legacy Elasticsearch.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![The architecture of Yelp's in-house Search Engine - nrtSearch](https://i.ytimg.com/vi/i8MweKYoG1U/mqdefault.jpg)](https://www.youtube.com/watch?v=i8MweKYoG1U)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Elasticsearch is a great search engine, but Yelp was not happy with its performance, so they built their own HTTP layer on top of Lucene. In this video, we take an in-depth look into the architecture and critical decisions Yelp took while building its own search engine on top of Lucene.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1J5gDekL7mK52vmZjgA8qO-fQFcPzNiYb/view?usp=sharing)
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