How to scope a microservice?
===


It is always exciting to create new microservices as it gives us so many things to look forward to- a fresh codebase, a new tech stack, or even maybe a clean CICD setup. But does this mean we should create as many microservices as possible?

Whenever we decide to create a new microservice, it is very important to understand its scope of it. If you create a new service for every utility then you are effectively creating a mesh of network calls that is prone to a cascading failure. If your scope is too big, it would lead to the classic problem of a monolithic codebase.

There are a couple of guiding principles that would help us with scoping of microservice.

## Loose Coupling

Services are loosely coupled if changes made in one service do not require a change in other. This is the core ideology behind microservices as well, but while designing a system we tend to forget it.

Say, we have an Orders service and a Logistics service. These services are loosely coupled when they do not share anything in common and are communicating with each other via API contracts.

To achieve loose coupling, make your microservices expose as little information as possible. The other service should just know how to consume the data and that is it. No internals, no extra details.

## High Cohesion

The principle of High Cohesion says that the related behavior should sit together as part of one service while the unrelated ones should be separate. This would encourage services to be operating independently.

If the Orders service also owns the customer data then when the changes are deployed in one might affect the other module. So the scope of testing before taking things to production increases.

If there is a very strong coupling between the services then it may also happen that the changes in one lead to deploy a few other services- all at the same time. Deploying multiple services at the same time is very risky; because one glitch and the almost entire product is down.

Hence it is not favorable for heterogeneous components to be part of the same service. Keep it crisp and short; and while designing try to keep services loosely coupled and split it to a level where the unrelated components are split up.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How to scope a microservice?](https://i.ytimg.com/vi/nfkdKHcKxbE/mqdefault.jpg)](https://www.youtube.com/watch?v=nfkdKHcKxbE)

Microservices are extremely tempting and you will always feel like writing a new service for every problem at hand. You might build a service with very fine-grained responsibilities or you can build one that covers a big spectrum. So, what is the best approach? How should you decide?

In this video, we talk about ways to model and scope a microservice such that the architecture remains robust and flexible; and to achieve this we use the two key guiding concepts - Loose Coupling and High Cohesion.

Outline:

00:00 What is the problem with Microservice?
03:05 Why do we love building microservices?
04:04 What happens if we do not scope our services well?
05:52 Two key guiding principles to scope a microservice
07:19 Loose Coupling
12:15 High Cohesion

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1_P8YVcw7uwr0wfs2V6W-1gpOwnoG2Zdf/view?usp=sharing)
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