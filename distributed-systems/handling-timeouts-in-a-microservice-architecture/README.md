Handling timeouts in a microservice architecture
===


# Gist

How to handle timeouts in a microservice architecture? [ in a gist ]

Microservices give us the flexibility to pick the best tech stack to solve the problem optimally. But one thing that ruins the real thrill is Timeouts.

Say we have a blogging website where a user can search for blogs. The request comes to the Search service, and it finds the most relevant blogs for the query.

In the response, a field called "total_views" should hold the total number of views the blog received in its lifetime. The search services should talk to the Analytics service synchronously to get the data. This synchronous dependency is the root of all evil.

The core problem: Delays can be arbitrarily large

Because the delay from depending on service can be arbitrarily large, we know how long to wait for the response. We for sure cannot wait forever, and hence we introduce Timeout. Every time the Search service invokes the Analytics service, it starts a timer, and if it does not get a response in the stipulated time, it timeout and moves on.

There are 5 approaches to handling timeouts.

Approach 1: Ignore the timeout and move on
Approach 2: Use some default value if you timed out
Approach 3: Retry the request
Approach 4: Retry only when needed
Approach 5: Re-architect and make synchronous dependency an async one


Handling timeout well is extremely critical as it makes your distributed system robust and ensures you provide a consistent user experience by adhering to SLA guarantees. In this video, we discover how a synchronous dependency on a microservice leads to long delays becoming a big problem, understand how timeout addresses the concern, and discuss 5 approaches to handle service timeouts.

Outline:
 - 00:00 Why is handling timeout critical?
 - 01:13 Synchronous communication and timeouts
 - 05:39 A rule of thumb: Timeout
 - 07:52 Approach 1: Ignore the timeout
 - 10:28 Approach 2: Configure and use defaults
 - 11:27 Approach 3: Retry when timeout
 - 16:36 Approach 4: Retry only when needed
 - 20:06 Approach 5: Rearchitect and remove synchronous dependency

[![Handling timeouts in a microservice architecture](https://i.ytimg.com/vi/Hxja4crycBg/mqdefault.jpg)](https://www.youtube.com/watch?v=Hxja4crycBg)


# Notes

The notes used in the video is can be found in the current folder and on [Google Drive](https://drive.google.com/file/d/1GjObZ3xpLFxDEOO3EGRCj0Pq8bWLixjU/view).


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