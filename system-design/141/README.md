An in-depth introduction to Canary Deployments
===


Canary Deployments is a deployment pattern that rolls out the changes to a limited set of users before doing it for 100%.

We compare the vitals side-by-side from the old setup and the canary servers to ensure everything is as expected. If all is okay, then we incrementally roll out to a wider audience. If not, we immediately roll back our changes from the canaries.

Canary Deployment thus acts as an Early Warning Indicator to prevent a potential outage.

## Why canary deployment is named canary deployment?

In 1920, coal miners used to carry caged canaries with them. If the gases in the mines were highly toxic the canaries would die and that alerted the miners to evacuate immediately, thus saving their lives.

In canary deployment, the canary servers are the caged canaries that alert us when anything goes wrong.

## Implementing canary deployment

Canary deployments are implemented through a setup where a few servers serve the newer version while the reset serves the old version.

A router (load balancer / API gateway) is placed in front of the setup and it routes some traffic to the new fleet while the other requests continue to go to the old one.

## Pros of Canary Deployment

- we test our changes on real traffic
- rollbacks are much faster
- if something's wrong only a fraction of users are affected
- zero downtime deployments
- we can gradually roll out the changes to users
- we can power A/B Testing

## Cons of Canary Deployment

- engineers will get habituated to testing things in production
- a little complex setup
- a parallel monitoring setup is required to compare vitals side-by-side

## Selecting users/servers for canary deployment?

The selection is use-case specific, but the common strategies are:

- geographical selection to power regional roll-out
- create specific user cohorts eg: beta users
- random selection

## When we absolutely need Canary Deployments

Say you own the Auth service that is written in Java and you chose to re-write it in - Golang. When taking it to production, you would NOT want to make a direct 100% roll-out given that the new codebase might have a lot of bugs.

This is where canary is super-helpful when we a fraction of servers serving requests from Golang server while others from the existing setup. We now forward 5% traffic to the new ones and observe how it reacts.

Once we have enough confidence in the newer setup, we increase the roll-out fraction to 15%, 50%, 75%, and eventually 100%. Canary setup thus gives us a seamless transition from our old server to a newer one.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![An in-depth introduction to Canary Deployments](https://i.ytimg.com/vi/nnseeKxovaM/mqdefault.jpg)](https://www.youtube.com/watch?v=nnseeKxovaM)

Deployments are stressful; what if something goes wrong? What if you forgot to handle an edge case that was also missed during the unit test, integration test, or an internal QA iteration.

Putting such code into production can take down your entire infrastructure and could cause a massive outage. In order or handle such a situation gracefully and provide us with an early warning about something's wrong we have Canary Deployment.

In this video, we take an in-depth look into canary deployments, learn why canary deployments are called canary deployments, and understand how they are actually implemented, talk about the pros and cons of this deployment pattern, and conclude with a one really solid use case where you absolutely need them.

Outline:

00:00 Agenda
03:05 Introduction to Canary Deployment
06:06 Why Canary Deployments are called Canary Deployments?
08:04 How to implement Canary Deployments?
10:03 Pros of having Canary Deployments
16:21 How to pick servers and users for a rollout?
19:08 Cons of having Canary Deployments
21:25 When we absolutely need Canary Deployment

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1JJD_Pa9AkUvhaZ7Dzwd4sQiGdC8nPn5t/view?usp=sharing)
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