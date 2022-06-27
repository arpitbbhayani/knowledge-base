Best practices that make microservices integration easy
===


Running Microservices in isolation does not make any sense; it is natural for them to work together and solve a bigger problem. This would require each microservice to expose a well-defined API interface simplifying others to talk to it.

The following are the best practices that we should follow that would make interfacing and integration easy.

## Forward and Backward Compatability

While rolling out any changes in a microservice, we need to ensure they are both forward and backward compatible. If not, it would break the consumers or interfacing microservices.

Three key places where we need to be extra careful are

- while changing the database schema
- while changing the API response body
- while changing the message format in async communication

We can ensure forward and backward compatibility if we

- never abruptly delete any column/attribute
- never abruptly change the type of the column/attribute

We should always roll out breaking changes in phases ensuring the dependent services remain unaffected.

## Make APIs tech-agnostic

Tech evolves quickly in the world of software engineering, and hence we would always feel like using the new shiny thing available. While having that urge, we should always ensure we are not picking the technology that would induce tight coupling.

For example, we should not pick a framework that would require the interfacing services to be written in a particular language or require them to use a specific tech stack. This would take away autonomity from the interfacing services as we are dictating which stack to use.

## Dead simple consumption

Microservices are built to interact with other services and get things done. So, the core focus should be to make things super simple for anyone to integrate.

It does not matter how good your LLD is if the API interface is hard to integrate. Be consumer-centric while desinging the interface of a microservice and ensure you have

- simple API
- simple data format
- use common protocols

## Hide internal implementation details

Never let other microservice learn about the internal implementation detail of your service. If they interact using internal details this would create a tight coupling between the two services.

Internal details could be

- broker for internal communication
- building dependency on transitive dependencies
- allowing directly connecting to the private database

It is always safe to hide the internal implementation details and expose a strict interface to interact with the service. The interface could be REST, gRPC, or anything that your org uses.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Best practices that make microservices integration easy](https://i.ytimg.com/vi/Wby0d9Li5Hw/mqdefault.jpg)](https://www.youtube.com/watch?v=Wby0d9Li5Hw)

Running microservices in isolation does not make any sense. To get something done, multiple microservices need to talk to each other and put a task to completion. This requires the services to interface with each other.

How would the services interface and integrate? is there a common way to do it?

In this video, we talk about 4 best practices we should follow while designing microservices to encourage inter-service integration. These practices would help us keep interfacing simple, easy, and intuitive.

Outline:

00:00 Agenda
02:36 Introduction
03:00 Backward and Forward Compatability
06:29 Make API interface tech agnostic
09:01 Dead simple consumption
11:00 Hide internal implementation details

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1vEur6ubY3ro_7C0JKEjs93ClboPJIMh5/view?usp=sharing)
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