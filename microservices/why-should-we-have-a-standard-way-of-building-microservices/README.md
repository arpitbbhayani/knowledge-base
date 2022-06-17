Why should we have a standard way of building Microservices?
===


We all love creating microservices, but there should be a standard way of creating them?

If we give complete autonomy to engineers to build their services then we will end up with the chaos of languages, frameworks, tools, and conventions. Hence standardization becomes essential to limit the chaos.

Standardization allows us to keep the entire system coherent and uniform and the 3 verticals that need standardization are:

## Monitoring

Monitoring one microservice is relatively a simpler problem, and with easy-to-integrate tools, it becomes a breeze. Few examples

- logging tools - ELK or EFK
- APM tools - NewRelic or DataDog
- status code monitoring on cloud consoles

Monitoring how a request originates from the user and goes through various services is important and this problem of Distributed Tracing can be solved through tools like Zipkin and AWS X-Ray.

Microservices need a standard way of reporting key metrics like CPU, Memory, Disk, and App Metrics into a central system like NewRelic or CloudWatch allowing everyone to get the necessary transparency.

## Interfaces

There are 100s of ways through which the microservices could talk to each other. This demands standardization and we need to consolidate on a few ways of interfacing.

Consolidating to REST for user-to-service communication and gRPC for service-to-service communication seems to be the most popular choices. But it is totally up to you to pick the ones.

We cannot allow the communication to happen over a variety of formats and hence we need to consolidate on a few like - JSON and ProtoBuf.

We also need to standardize the nomenclature and how REST endpoints are written. This would ensure that the entire engineering team feels familiar while writing any inter-service communication.

Other aspects that need standardization are Versioning, Timeouts, and Retries. Having this standardization would allow us to write common libraries to abstract out the implementation complexities and save redundant efforts.

## Tolerance

Every service needs to shield itself from getting bombarded. Standardizing the tolerance would save us redundant efforts and implementations. A common protection layer would not only prevent the service from getting overwhelmed but also ensure no cascading failures.

Some standard configurations could be

- limit the number of incoming calls from a service
- ability to cut off incoming and outgoing requests from/to a service

Such abilities would help us reduce outage times and prevent cascading failures as engineers would be aware of exactly what to do to cut off.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Why should we have a standard way of building Microservices?](https://i.ytimg.com/vi/0q61wIUmVDY/mqdefault.jpg)](https://www.youtube.com/watch?v=0q61wIUmVDY)

We all love creating microservices, but what if every team creates its own microservice uniquely and uses its own conventions? it would create massive chaos of practices, protocols, frameworks, and conventions.

This propels us to have some standardization on how we build a microservice and hence in this video, we talk about, why it is essential to standardize some aspects of a microservice, how enforcing a few practices helps us in the long run, and, look at the 3 most essential verticals that you should definitely standardize while adopting microservices.

Outline:

00:00 Agenda
02:39 Need for standardization
09:42 Standardizing Monitoring
14:21 Standardizing Interfaces
18:39 Standardizing Tolerance

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1JrK5rL7SxQxBCDJTzRhHMQ5r-4Hx8-1q/view?usp=sharing)
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