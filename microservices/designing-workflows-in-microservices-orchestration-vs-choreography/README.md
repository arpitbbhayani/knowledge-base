Designing Workflows in Microservices - Orchestration vs Choreography
===


Say we are building an e-commerce website and upon every purchase made we need to send a confirmation email to the user, notify the seller to keep the shipment ready and assign a logistic delivery partner to deliver the package to the user. So, how do we implement this?

Two high-level architecture patterns help us achieve this

- Orchestration
- Choreography

# Orchestration

Orchestration is the simplest way to model workflows. The core idea of the Orchestration pattern is to keep the decision logic centralized and have a single brain in the system.

In our example, the Orders service can be that brain, and when the order is placed the order service talks to Notification, Seller, and Logistics services and get the necessary things done. The communication between them is synchronous and the Orders service acts as the coordinator.

The workflow as part of our example is a one-level simple workflow but in the real world, these workflows could become extremely complex and the Orders service would be needing to handle the coordination.

# Choreography

The core idea of the Choreography pattern is to keep the decision logic distributed and let each service decide when needs to be done upon an event. It thus laid the foundation for Event Driven Architecture.

In our example, when the order is placed the Orders service will simply emit an event to which all the involved services subscribe. Upon receiving an event, the services will react accordingly and do what they are supposed to.

All the 4 involved services are thus totally decoupled and independent; making this a truly distributed and decentralized architecture

# Orchestration vs Choreography

Most model systems are inclined towards Choreography as it gives some amazing benefits

- loose coupling: services involved are decoupled
- extensibility: extending the functionality is simple and natural
- flexibility: search service owns its own decision on the next steps
- robustness: if one service is down, it does not affect others

Observability might become a challenge here; given that we need to track each service, action it took, and completion of it.

Although people prefer choreography, it does not make Orchestration bad. Orchestration has its advantages and can be used in modeling services that are involved transactionally.

For example, sending OTP during login is best modeled synchronous instead of doing it async. Another example is when we want to render recommended items the Recommendation service talks to relevant services to enrich the information before sending it to the user.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Designing Workflows in Microservices - Orchestration vs Choreography](https://i.ytimg.com/vi/HiwOx-W1TIA/mqdefault.jpg)](https://www.youtube.com/watch?v=HiwOx-W1TIA)

In a microservices architecture there will always arise a need to design workflows; for example: when on an e-commerce website someone places an order, we need to send an email confirmation to the user, notify the seller to keep the shipment ready, and also assign a logistic delivery partner so that the package is delivered to the user.

Modeling these workflows is a challenge as it requires multiple microservices to coordinate. So, how can we implement them? There are two high-level architecture patterns to implement workflows, and they are - Orchestration and Choreography. In this video, we take a detailed look into the two patterns and see what they are, how they are implemented, and which one to use when?

Outline:

00:00 Agenda
03:02 Introduction to Workflows in Microservices
03:55 Orchestration
06:28 Choreography
09:51 When to use Orchestration, and when to use Choreography

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1h-YVs2toYWW0qnRKGoPbPdlkpDgp9M9m/view?usp=sharing)
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