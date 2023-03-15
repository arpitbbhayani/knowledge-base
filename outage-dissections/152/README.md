Dissecting GitHub Outage - Downtime they thought was avoided
===


GitHub thought they avoided an outage by fixing a possible root cause 6 months in advance, but fate had different plans.

## Check Suites and Workflows

When we push any changes to any GitHub repository there are some checks that run. We can see them on our Pull Request and it basically prevents us from merging the PR until all checks are successful. We can also add custom checks on our own to the workflow.

An entry is made in the database for every execution of the check suite. This is a high frequency that would lead to heavy ingestion in the database table. A side effect it would be that the auto-incrementing ID column, which is typically a 32-bit integer would exhaust leading to the writes getting failed.

## GitHub's Anticipation

GitHub anticipated this situation 6 months in advance and they altered the column from 32-bit integers to 64-bit integers ensuring that even when the ID range exhausts the 32-bit limit it would lead to downtime.

But still, the team faced an outage, how? what happened?

## What exactly happened?

The service was able to create entries in the database about the check suite execution as the database supported 64-bit integers, but there was one external dependency that unmarshalled JSON strings to native objects which only supported 32-bit integers.

The service was responsible for pulling the jobs from the database and putting it in the queue to be picked up by executors. This service depended on the library and hence it was unable to execute the checks. This led to all the checks remaining in the pending state during the course of this outage.

## Impact on the Search service

The search service was also impacted by this as the indexing used queue as the source. Since the newer jobs were not put in the queue, they were not indexed in the search cluster (eg: ElasticSearch), and hence when the user searched, they could not find the latest checks and workflows.

## Mitigation

In order to mitigate the issue, the GitHub team released a code fix. Speculation: they would have updated the library version that would support 64-bit integers, or they might have quickly forked and patched it with the changes, or they might have written some ad-hoc job that temporarily pulled the jobs and put them in the queue.

This incident shows that no matter how big the company gets and how prepared are you for an extreme event, there would always be some blind spots in the system that would bite us back.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage - Downtime they thought was avoided](https://i.ytimg.com/vi/9GHh_U-ud9U/mqdefault.jpg)](https://www.youtube.com/watch?v=9GHh_U-ud9U)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Has it ever happened to you that you anticipated that something would go wrong, you pro-actively fixed it, but it still went wrong? This exact thing happened to GitHub on March 1, 2021, in a situation for which they were prepared for 6 months. This is a very amusing incident as it teaches us a lot about the blind spots that exist in every system out there.

In this video, we talk about an outage that GitHub faced with their Actions service. and take an in-depth look into what happened, why it actually happened, and what GitHub did to prepare for this very situation, but it still went wrong.

Outline:

00:00 Agenda
02:46 What happened?
05:12 Table Exploded with Data and IT reached its limit
07:03 GitHub's Anticipation and What went wrong?
12:27 Mitigation
14:04 Impact on the Search Service

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1J9wbS2sK5BrW5Ftgdz2tmPrt86tAhQaA/view?usp=sharing)
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