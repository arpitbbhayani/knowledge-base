So, the outage is mitigated, now what?
===


Getting the service up is P0 during the outage, but that is not all. There are a few other things that we need to take care of once the issue is mitigated.

## Resolve Inconcistencies

During the outage, the business logic or database must have crashed while handling in-flight requests; hence there is a very high chance of the data becoming inconsistent.

For example: if the process crashed while transferring money from one account to another; it is possible that money got deducted from one account but did not credit to another.

Hence once the outage is mitigated, the first thing to be done is to ensure that the data does not remain in an inconsistent state. Achieving this depends on the usecase at hand and the tech stack involved.

## Invalidate the Cache

Another place that needs attention is cache invalidation. If the outage sustains for a long time, there is a chance that some of the entries in the cache are not valid anymore.

Hence, depending on the usecase, it is advised to go through the cache entries and delete the invalid once ensuring the end-user sees a globally consistent view of the data.

## Audit alerting and monitoring

Once the outage is mitigated and the inconsistencies are resolved, it is better if we take a look into existing alerting and monitoring practices so that we ensure that we get alerted at the right time.

In most cases, you would find that a few things could always be improved when it comes to monitoring the right things, and hence an outage is an opportunity to get alerting and monitoring improvements prioritized.

## Take preventive measures

Every outage has a root cause, and it is super-important to fix the root cause to ensure that the over never happens again for the same reason. This requires us to go in-depth and take preventive measures to ensure complete closure.

For example, re-auditing all the INT32 columns and moving them to INT64 to ensure that we never repeat the outage due to integer overflow.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![So, the outage is mitigated, now what?](https://i.ytimg.com/vi/LeT_s-UFw-U/mqdefault.jpg)](https://www.youtube.com/watch?v=LeT_s-UFw-U)

Outages happen and in such a tense situation, the main priority is to get the system back up, but is that it? Is everything done when the service is up and running?

So today let's spend some time talking about the aftermath of an outage. There are many things to take care of once the outage is mitigated and in this video, we dissect a GitHub outage, understand what happened, and look at a set of common practices that we follow to ensure closure.

Outline:

00:00 Agenda
02:31 The outage and mitigation
07:23 Solve data inconsistency
09:51 Invalidate the cache
11:03 Setup alerting
13:53 Take preventive measures

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1pDHYlKlQsTB_oDvqG9mpsvfKkHWDnkRG/view?usp=sharing)
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