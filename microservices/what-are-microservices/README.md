What are Microservices?
===


Everyone's talking about Microservices, but what exactly are they? Are they just a set of functions hosted over a network or something more?

Microservices in simple terms are like the regular functions from our programming language but just a more extensive set of responsibilities and served via a network.

So, you may have a microservice that handles everything related to Payments, a service that handles Notifications, and a service that deals with analytics. We see each service having focussed responsibility.

Microservices are no silver bullet, and they would not magically solve all the problems you have. It has its own fair share of drawbacks.

## Monolith

Almost all products start monolith where every feature is put into a single codebase which is deployed as one artifact across all the servers. For example, the code handling payments, notifications, and analytics are all part of the same codebase deployed within the same binary.

Monoliths are always simple to build, develop, test, and scale. Given their simplicity, they are the go-to option for anyone starting up. With a lean team working on monolith would ensure very quick feature delivery.

### Disadvantages of Monolith

- monolith is tightly coupled
- the deployment artifact - binary/JAR is bulky
- the tech stack is homogeneous
- bug in one module affects other modules
- scaling one module requires scaling everything
- large monolithic codebase is intimidating and it slows down delivery

### Monolith to Microservices

Migrating from monolith to microservices is a slow process and to start you would club a related set of functions and fork out a service out of it. The process would be repeated for other sets of functions, eventually breaking the entire monolith.

## Characteristics of Microservices

- microservices are autonomous
- microservices are focused and specialized
- microservices are built around a business usecase/need

## Advantages of Microservices

- agility: small independent teams can move much faster
- scaling: you can precisely scale one service as per the load
- freedom: you can pick the best-suited tech stack for the service
- given the scope is focused, a microservice is simple to understand
- microservices can be reused across the platform
- if a service goes down, it is easy to isolate it using a circuit breaker

## Anti-patterns

- do not start with microservices; start with a monolith
- do not make services too small; they should a larger responsibility
- don't reinvent the wheel, use existing tooling as much as possible
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![What are Microservices?](https://i.ytimg.com/vi/qoAox0FGzRQ/mqdefault.jpg)](https://www.youtube.com/watch?v=qoAox0FGzRQ)

Everyone is doing Microservices, but what are they after all? From a distance, it looks like a function put over the network. Is it really just that? There are so many things to explore about microservices, so let me introduce you to this world today.

In this video, we talk about what are microservices, understand how it starts with a simple monolith and eventually evolve into microservices, look at their key characteristics, understand their advantages, and conclude with some anti-patterns that we all should keep in mind to ensure we do not do it wrong.

Outline:

00:00 Agenda
02:38 Idea of a Microservice
09:26 Monolith Architecture
16:19 Monolith to Microservice
18:49 Characteristics of a Microservice
21:09 Advantages of Microservices
24:06 Anti-patterns in Microservices

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1SaDvF80ZirInE4XyVRu8F6PnIm-1b8vl/view?usp=sharing)
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