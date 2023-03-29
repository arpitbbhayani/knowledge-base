An in-depth introduction to Rolling Deployments
===


Rolling Deployment is a deployment strategy that slowly replaces the previous version of the application with the new one by replacing the underlying infrastructure.

Say we have 9 servers and each one is running version 1 of the code. With rolling deployment, we roll out our changes i.e. version 2 of the code to one server at a time eventually covering all 9 servers. This is the core idea of the rolling deployment, however, the implementation could vary a bit.

A key thing to note here is the fact that deployment is incremental in nature which means during the deployment there would be a few servers that are serving the old version of the code and the remaining servers serving the newer version. Hence the changes we push should be both backward and forward compatible.

## Implementing Rolling Deployment

Rolling deployments are always gradual and graceful, and we typically happen through the below steps

1. Pick a server for deployment
2. Stop the incoming traffic by removing it from the load balancer
3. Wait for the existing requests to be completed
4. if we are not replacing the infra, pull the latest code and reload
5. if we are replacing the infra, delete the server and launch a new one with the new code
6. attach the server behind the load balancer and start serving the requests

## Tuning Rolling Deployment

### Concurrent Servers

Instead of deploying to one server at a time, we can deploy changes to `n` servers concurrently. This would complete the entire deployment quicker.

Choosing the appropriate `n` is critical as a small value would mean the deployment takes ages to complete and a large one would affect the availability during deployment.

### Double-Half Deployment

An interesting way to implement rolling deployment is to double the infrastructure and then delete the older half.

Say, we have 4 servers with version 1 of our code so in order to deploy the changes we add 4 new servers with the new version of the code to the infra taking our total count to 8, and then delete the 4 older servers. This way, what remains are the 4 servers with the newer version of the code.

## Pros of Rolling Deployments

- Cost efficient
- Rollouts are gradual
- Rollbacks are simple
- Deployment incurs zero downtime
- Much faster than Blue-Green Deployment
- Any hiccup during deployment affects only a fraction of the users

## Cons of Rolling Deployments

- No environment isolation
- Naive deployment takes a long time to complete
- Stateful applications are affected during deployment
- Changes we rollout should be backward and forward compatible
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![An in-depth introduction to Rolling Deployments](https://i.ytimg.com/vi/9kjUG_yvVqM/mqdefault.jpg)](https://www.youtube.com/watch?v=9kjUG_yvVqM)

One of the simplest deployment strategies that make deployment a breeze is Rolling Deployment. It is the most widely adopted deployment strategy purely because of its simplicity and cost-effectiveness. Most of the deployment tool has this as their default deployment strategy.

In this video, we take an in-depth look into what Rolling deployment is, how they are implemented, how to tune it, some key challenges we face during adoption, and conclude with an understanding of the pros and the cons of adopting it.

Outline:

00:00 Agenda
02:37 Introduction to Rolling Deployments
05:43 How to implement Rolling Deployment
11:32 Tuning Rolling Deployments
15:59 Pros of Rolling Deployment
18:37 Cons of Rolling Deployment

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1Mtox_ulRNSajmbVXXyLyJrhV3GZouOiv/view?usp=sharing)
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

<img width="256px" src="https://edge.arpitbhayani.me/img/arpit.jpg" />

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