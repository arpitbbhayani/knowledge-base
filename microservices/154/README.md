10 Challenges in Adopting and Implementing Microservices
===


We always hear great things about Microservices. But today let's talk about the top 10 challenges that come with adopting Microservices.

## Managing Microservices

As the number of microservices increases, managing them becomes tough. If there is no plan or accountability then we might end up with a lot of tiny microservices or with a huge macro-service.

## Extensive Monitoring and Logging

Monitoring what happens across the entire infra is critical. Along with this, we would also need an ability to trace end user request path spanning services - also called Distributed Tracing.

## Service Discovery

It does not take much time for our services to grow beyond 100 and at that scale, discovering a service becomes a pain requiring us to put Service Discovery.

3 ways to do it are

- a central service registry
- load balancer-based discovery
- pure service mesh implementation

## Authentication and Authorization

Inter-service communication should be secure to ensure that a service does not abuse others; hence we need to put auth in place that allows authorized services to talk to each other.

## Config Management

Every microservice has a set of configs, like DB passwords, and API Keys. Committing them to the repository is an unacceptable practice, and we would not want every service to have its own config server.

Hence we need to have about a central config management system that is fault tolerant, robust, and scales well.

## No going back

It is extremely difficult to move back to monolith after the teams have tasted microservices. A few reasons would be

- services are written in various languages
- teams used to being autonomous
- teams have adopted new tools and processes

## Fault Tolerance

Outages are inevitable and as engineers, we always try to minimize them. A way to achieve this is to keep services loosely coupled that keep outages isolated ensuring no cascading failures.

## Internal and External Testing

End-to-end testing becomes complex as it is hard to spin up environments with all services running fine.

## Design with Failures in mind

Robust microservices require a counter-intuitive approach, and we need to assume everything would collapse after every line of code. Then we amend the code and architecture to handle it and re-iterate.

## Dependency Management is a nightmare

Managing dependencies across services is tough and it leads to a slowdown. The 3 kinds of dependency to be careful about

- sync dependency on other services
- services sharing a common library
- service depending on data coming from other services
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![10 Challenges in Adopting and Implementing Microservices](https://i.ytimg.com/vi/yTSq6hJFmUg/mqdefault.jpg)](https://www.youtube.com/watch?v=yTSq6hJFmUg)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

We always hear great things about Microservices. But, every few months every senior engineer gets a feeling, can we not go back to a simpler time and have monolithic architecture again?

In this video, let's understand the 10 challenges that come with adopting microservices. Today, we would spend time talking about both engineering or tech challenges and organizational challenges that we all should be aware of and address while we adopt microservices.

Outline:

00:00 Agenda
02:34 Managing Microservices
05:25 Monitoring and Logging
08:26 Service Discovery
10:44 Authentication and Authorization
12:17 Configuration Management
14:09 There's no going back
16:56 Fault Tolerance
18:43 Internal and External Testing
20:05 Design with Failures in mind
21:23 Dependency Management is a Nightmare

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1qOCi_CaT5qYO_Qbm-6UB2IN-qcGc8AYB/view?usp=sharing)
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