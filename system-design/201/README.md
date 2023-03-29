Aggregating DynamoDB data in realtime to list restaurants at Deliveroo
===


DynamoDB does not support aggregation queries, but we need it for a use case; let's build a real-time DDB aggregation today...

Deliveroo, a food delivery startup had a similar problem. On their app, people can mark a restaurant as "favorite" and now they wanted to render restaurants ordered by most favorite first.

## Data Model

We have a `favorites` table in which we store users and their favorite restaurants. The table has `restaurant_id_user_id` as their primary key and `created_at`, and `user_id`, as other attributes.

With the above data model, getting if a user marked a restaurant as a favorite is an O(1) lookup and so are the marking and unmarking activites.

## Getting restaurants ordered by favorite count

With this data model, it becomes near impossible to get restaurants ordered by their favorite count, purely because DynamoDB does not support aggregations.

### Core idea

Maintain a separate table having aggregated favorite count as one of the attributes and use it to get tables ordered by favorite count.

### Data Model

Introducing a new table `aggregated_favourites` having the following schema

- `rastaurant_id` as the primary key
- `time_window` as the sort key
- `favourite_count`, `updated_at` as other attributes.

### Data Flow

We set up a DynamoDB stream that would contain all the events happening on the `favorites` table. This stream will be consumed by an AWS lambda function.

The lambda function will transactional do `count++` upon every creation and `count--` on deletion.

This way, we maintain the aggregated favorite count for each restaurant in near-realtime without doing any fancy code changes.

### Advantages

- extremely cost coefficient for Deliveroo scale
- count updation is asynchronous, hence API response time unaffected
- better than running a daily cron job or doing a sync write to the aggregated table.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Aggregating DynamoDB data in realtime to list restaurants at Deliveroo](https://i.ytimg.com/vi/VNvTEin2liY/mqdefault.jpg)](https://www.youtube.com/watch?v=VNvTEin2liY)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

DynamoDB is an extremely powerful, scalable, and fast KV store but it lacks Aggregations.

In this video, we design a usecase that is very common for food delivery startups like Deliveroo and Swiggy that would require us to do real-time aggregation of the DynamoDB data in an extremely cost-efficient way.

Outline:

00:00 Agenda
02:28 Marking Restaurants as Favourite
04:49 Realtime aggregating DynamoDB data using Streams
11:10 Why Serverless?

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1EuEW8z07r7mJ0dXO8yWIJ9xJpc_8LQFW/view?usp=sharing)
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