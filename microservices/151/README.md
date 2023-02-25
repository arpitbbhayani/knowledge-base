API Composition Pattern in Microservices
===


Say, we have 3 microservices - Order, Payments, and Logistics - and to get the order details we need data from all of them, merge it, and then respond to the client. A common pattern to achieve this is API Composition.

## API Composition

It is a high-level pattern to query microservices. It puts a composer right in the middle abstracting out the microservices.

With the composer sitting in between, the request from the client first hits the composer, and the composer then talks to the relevant services to get the response. It then merges the responses before sending them to the client.

## Implementing API Composition

Instead of building it from scratch, we can use tools that specialize in achieving this - ex: API Gateways like KrakenD, Kong, and AWS API Gateway.

## Improving user's experience using composer

An API Composer not only helps in making the backend simpler, but it also helps in gaining a good UX.

If we do not have an API composer, the client (browser/app) would have to make multiple API calls to microservices to get the information and render the interface. The multiple calls would require multiple round trips of the data increasing the latency and will also eat up the user's data.

By having an API composer sitting in between the client would only need to make one API call and the fan-out happening at composer will be within the infra. This would reduce the latency for clients and improve the UX.

## Branch Composition

For a complex usecase, it is quite possible that a downstream service may use another composer to reach out to another set of services to get things done. A dependency like this would create a multi-level API composition also called Branch composition.

This would create a hierarchical dependency between services solved through multiple API composers and it is a common pattern observed in complex e-commerce platforms.

## Advantages of using API Composition

- Simple to implement
- Client has a single point to interact
- Hides the implementation complexities
- Security and Limiting applied only to the composer
- Can cover the "bad" design decisions with a shiny new interface
- Hides legacy system allowing us to gradually move out of it

## Disadvantages of using API Composition

- If the dataset we fetch from microservices is large, it would make the composer in-efficient
- Overall availability is challenged as the number of services increase
- Having a transactional data consistency is difficult
- Composer needs to be managed and maintained
- Composer may become a bottleneck at scale
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![API Composition Pattern in Microservices](https://i.ytimg.com/vi/5pYLlYsy6fQ/mqdefault.jpg)](https://www.youtube.com/watch?v=5pYLlYsy6fQ)

Say, we have very happily created 6/7 microservices and everything is going well. Now for a new usecase that is introduced in the product, we have to talk to not one but 3 services together to compile a response. So, what is a good way of implementing and supporting this kind of request? A high-level pattern that helps us do it is called API Composition.

In this video, let's in-depth talk about this super simple pattern to query Microservices, see what it is, how to implement it, understand how it not only helps in improving end user experience, and conclude by going through the advantages and disadvantages of adopting it.

Outline:

00:00 Agenda
02:54 Introducing API Composition
04:53 Implementing API Composition using API Gateway
06:44 Sequential vs Parallel Invocation
09:21 Improving end-user experience using API Composition
12:43 Branch or Multi-level API Composition
14:03 Advantages of API Composition and Gateways
18:49 Disadvantages of API Composition and Gateways

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1e5AqRKDRQ8c_3rqWWfBTDa3cKXkuCvTt/view?usp=sharing)
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