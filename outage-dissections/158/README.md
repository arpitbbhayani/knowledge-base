Dissecting GitHub Outage - Downtime due to Rate Limiter
===


Rate Limiters are supposed to avoid downtimes, but what if they turn out to be the root cause of a major outage?

A large chunk of GitHub users saw elevated error rates and this happened after deploying their A/B Experimentation service. So, what went wrong? but before that let's understand what is A/B experimentation

## What is A/B Experimentation?

It is hard to decide which UI is better and hence before rolling out any critical UI change to all the users, a company tests it through an A/B experiment.

A set of users are chosen at random and a fraction of them are shown the new variation while others are shown the old one. Key vitals and metrics of the features are measured and compared to decide if the variation is indeed an improvement.

If the metrics are positive and significantly better then the new variation is rolled out to 100% of the users. This way companies ensure that the features that are rolled out are genuine improvements in the product.

## A/B Testing at GitHub

Every server that needs to participate in any A/B experiment fetches a configuration file that is dynamically generated using, say, Config Generator service.

The configuration allows granular controls for the A/B experiment and holds critical information that shapes experimentation. When any server requests for a config file, the request hits the config service and it, in turn, generates the file and sends it back to the user.

## What failed?

Because a lot of requests were made to the Configuration Service, the rate limiting module of the service started throttling and it prevented the configuration file to be generated and sent to the servers.

This affected the users who were part of this experiment and they saw elevated error rates as the frontend did not have the necessary information it required to power the experiment.

## Mitigation and Long-term Fix

As quick mitigation, the GitHub team disabled the dependency on the dynamically generated file and it restored the services to normal.

To ensure the outage would not happen due to the same reason, the Config Generator service would generate and cache the configuration files so that when a request comes, the file could be served directly from the cache instead of generating on the fly which was time consuming.

## Key Takeaways

- avoid sync dependencies between services and prefer async
- classify the services by severity tiers and run periodic audits of tier-1 services to ensure they are architected well and there are no blindspots
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage - Downtime due to Rate Limiter](https://i.ytimg.com/vi/VPZo8cO1HbI/mqdefault.jpg)](https://www.youtube.com/watch?v=VPZo8cO1HbI)

Rate limiters are supposed to avoid downtimes, but have you ever heard that a rate limiter caused a downtime? This happened with GitHub, where a big chunk of their users saw elevated error rates.

In this quick incident dissection, let's take a look at a high-level overview of how GitHub does their A/B experiments, how a low-level decision led to this incident for a large chunk of users, and conclude with some key things we all should learn from this outage.

Outline:

00:00 Agenda
02:32 What happened?
02:47 What is A/B Experimentation?
05:33 A/B Experimentation at GitHub and what failed
11:12 Mitigation and Long-term Fix
12:04 Key Takeaways

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/17xmYQ9tXQfhMUc85uYfkA880VH1ANEKH/view?usp=sharing)
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