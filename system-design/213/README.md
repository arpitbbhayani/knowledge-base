How @ShopifyEngineering avoids hot shards by moving data across databases without any downtime
===


Shopify is an e-commerce platform that enables individuals to create their online stores. Shopify uses MySQL database to hold their transactional data and each table has a column called `shop_id` that enables easy identification of rows belonging to a specific shop.

Shopify uses a distributed architecture to handle a large number of shops. A set of shops is grouped in a logical entity called Pod and all of them share the same database. Thus Shopify has multiple pods and each pod has multiple shops sharing the same database.

As the platform grows and more shops sign up, there arises a need to balance the load on different pods by moving the data across databases without downtime.

Let's discuss how they do it in detail.

## Routing Layer

The routing module uses NGINX and is the front-facing entity in the architecture. It routes requests to the pod that is supposed to handle them.

## Distribution of Shops in Shards

Distribution based on the number of shops is not a good idea because two 'heavy shops' may end up on one shard, risking failure due to over-utilization and inconsistent database utilization.

The decision of which shop lives in which shard depends on the 'heuristics' applied by the Shopify data science team. They consider historical database utilization, historical traffic on the shop, and forecasted load.

## Moving Shops Without Downtime

When moving a shop from one pod to another, Shopify ensures that there is no downtime or data loss. Shopify follows three high-level phases to move a shop from one pod to another.

### Phase 1: Batch Copy and Tail Binlog

In the first phase, Shopify uses an internal tool named ghostferry to batch and pick the rows with a particular shop id from multiple tables of the source database and write them to another database present in another pod.

While the batch copy is happening, the newer changes are consumed through `Binlog` and pushed into a queue after filtering out irrelevant events.

### Phase 2: Prepare for Cutover

Once the batch copy is complete, the newer changes are consumed from the queue and applied to the new database until the 'lag' is down to seconds.

When newer events are almost immediately consumed, the writes to the source database are stopped. The source DB's binlog coordinates are recorded, and as soon as the target DB reaches that point, we say replication is done.

### Phase 3: Cutover and Updating the Routing

At this stage, there are no new writes to the source DB, and the source DB is equal to the target DB.

The routing table is then updated and traffic is switched on. The requests for the shop now go to the new pod. After doing a few sanity checks, we mark the shop migration as complete.

## Conclusion

Shopify moves shops from one pod to another to balance shards. Shopify uses an internal tool named ghostferry to move a shop's data from one pod to another. Shopify ensures that there is no downtime or data loss while moving a shop from one pod to another. This article discussed how Shopify balances shards without downtime.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How @ShopifyEngineering avoids hot shards by moving data across databases without any downtime](https://i.ytimg.com/vi/7v-wrJjcg4k/mqdefault.jpg)](https://www.youtube.com/watch?v=7v-wrJjcg4k)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

A truly scalable system is one that can be scaled horizontally. A database is typically scaled by splitting the data across multiple shards. But what happens when a particular shard becomes hot due to excessive load hitting it, while others are underutilized? A classic way to address this is by moving a fragment of data from one node to another. But how?

In this video, we look at how Shopify re-balances the shard by moving a fragment of data from one database to another without incurring any downtime.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1W5AM_NXAZ7CjpmjcRzUKzq8Fpq0KpQ1p/view?usp=sharing)
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