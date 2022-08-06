Control an outage by localizing the failures
===


Outages are inevitable; but we should design our architecture and ensure that if a component is down, it should not lead to a complete outage.

## What happened with GitHub?

GitHub saw a lot of failures with their Actions service and this led to delays in queued jobs from being processed. The root cause was some infrastructure error in the SQL layer.

## Insights about their architecture

A couple of insights about their architecture

### Synchronous dependency

Although GitHub Actions look like a single feature, internally it consists of multiple microservices. Some of these, have a synchronous dependency on the database. Because of this, when the DB had a hiccup, the entire Actions feature was hindered.

### Zero trust communication

The service that was most affected in this outage handled communication; why would services need authentication? After all, they are all internal to the infrastructure?

Microservices talk. The communication needs to be protected with auth so that any engineer/service gone rogue cannot abuse the system in any capacity. Only authenticated and authorized services are allowed to take action.

## What about automatic failover?

Given that the outage happened on the database layer, why did the database do not auto-recover? It is a standard procedure and configuration that would have just promoted a replica to be the new master.

Although it is a common config, during this outage the metrics did not show any issue with the database, and hence the auto-failover was never triggered. It took a long time to even understand the root cause and then start mitigation.

## Long-Term Fixes

### Update the automation scripts

The automation that reads the telemetry and decides to do a failover needs to be updated so that such failures are detected and action is taken.

### Localizing failures

An important long-term change that needs to be driven is to localize the failure. In this outage, we learned how a hiccup in one database/service causes downtime of all dependent Microservices. This shouldn't have happened, as the Microservices are supposed to solve this very problem.

A good way to ensure that the blast radius of the outage is minima; is by ensuring the failures are localized, implying, that when a service is down, only the service is affected while everything else is functioning perfectly fine.

A common approach to getting this loose coupling is by powering inter-service communication through the asynchronous medium instead of synchronous API calls. Thus, if something breaks, we could fix it and continue to process the messages.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Control an outage by localizing the failures](https://i.ytimg.com/vi/Of3FS2qDM28/mqdefault.jpg)](https://www.youtube.com/watch?v=Of3FS2qDM28)

Outages are inevitable; but we should design our architecture such that if a component is down, it should not lead to a complete outage. It is easy to say this, but hard to implement.

In this video, we dissect yet another GitHub outage, gather a few interesting insights about their Microservices architecture, and spend some time discussing and understanding the importance of having a smaller blast radius and a fool-proof way of achieving that.

Outline:

00:00 Agenda
02:36 What happened
04:30 Root Cause
05:14 Insights about their architecture
08:50 Master failover did not happen
13:40 Long-term fixes and Localizing failures

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1V_nuSi4KDsuTD_p0beIWoBDmRN9T5d5V/view?usp=sharing)
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