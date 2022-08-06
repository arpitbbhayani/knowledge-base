BFF - Backend for Frontend - Pattern in Microservices
===


Say, we are launching an e-commerce website that people can use from their desktop and place orders. We want to render the product details that include - name, description, sellers, variants, reviews, and faqs. The site did well and now we decide to launch a mobile app.

Given that the mobile has limited real estate, it is very hard to render the same information that we do on the Web. Hence, we choose not to render Reviews and FAQs. Thus even if we receive the reviews and faqs in the response, while rendering we choose not to render them.

This is a waste of user bandwidth, data, and processing power. Ideally, we should not be sending unnecessary fields from the backend. So, how do we implement this?

## Backend for Frontend

BFF is a layer that sits between the clients and the backend. Every type of client has a dedicated BFF; for exampDesktop Web has its own BFF while Mobile has its own.

Depending on the request, the BFF then talks to the backend, grabs the data, filters out the unnecessary fields, and responds. It can also optionally transform the data in a client-specific format.

This way, we keep the backend simple and apply all presentation-level hacks and tweaks on BFF.

## BFF and Microservices

BFF acts as a perfect abstraction for underlying microservices. For an API, it can connect to necessary microservices, gather the responses, and respond. This ensures that we are not fetching data that we don't need.

For example, Given compatibility and constraints, a Desktop BFF can talk to Orders, Sellers, and Reviews Services, while a Mobile BFF can talk to Orders, Sellers, and AR services to respond to the same API endpoint.

## Advantages

- we can add client-specific tweaks and hacks on BFF
- we can hide sensitive information from specific clients
- we can patch client-specific vulnerabilities on respective BFF
- we can pick the best communication stack for the client and BFFs
- we can have a general-purpose backend supporting all kinds of clients

## Disadvantages

- a large chunk of code would be duplicated
- needs to support high fan-out, hence pick a stack that suits
- there is a slight increase in latency with the new network hop
- by adding BFFs we are adding more moving parts that need to be managed, maintained, monitored, and deployed

## Adopting BFF

We should adopt BFF when

- the interface between different clients varies significantly
- the communication format/protocol is different from what your backend supports (eg: legacy integration might need XML while your backend serves JSON)
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![BFF - Backend for Frontend - Pattern in Microservices](https://i.ytimg.com/vi/GCx0aouuEkU/mqdefault.jpg)](https://www.youtube.com/watch?v=GCx0aouuEkU)

As your application evolves, supporting multiple types of clients like Desktop, Mobile apps, etc becomes tricky. The backend becomes complicated, and you start applying a  lot of hacks to serve them properly.

In this video, we take a look at an interesting high-level architectural pattern in microservices, that solves this exact problem, called Backend For Frontend, fondly called BFF. We would see in detail what this pattern is all about, where it is used, how to implement it, look at its advantages and disadvantages, and conclude by building an understanding of when to use it.

Outline:

00:00 Agenda
02:47 Supporting multiple clients
10:05 Backend for Frontend Pattern
16:27 Advantages of BFF
21:25 Disadvantages and challenges with BFF
24:35 When to use BFF

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/19qxDMRlcABJ466roqny6x5ktFY7Gq5JU/view?usp=sharing)
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