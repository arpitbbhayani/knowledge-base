Should some microservices share a database?
===



<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Should some microservices share a database?](https://i.ytimg.com/vi/tV11trlimLk/mqdefault.jpg)](https://www.youtube.com/watch?v=tV11trlimLk)

Microservices need to communicate with each other. Communication between them is always about getting or updating data that is owned by the other service. What if a service gets direct access to all the data it wants? This is the simplest way for the microservices to communicate with each other, and this pattern is called Sharing the Database. The core idea here is to let anyone who needs the data from a service or wants to update something, can directly talk to its database - no middlemen needed.

Although most people think it is the wrong way of communication, we should not discard it completely. In this video, we talk about what this architecture pattern is, the 4 challenges associated with it, see ways to mitigate them, and understand when and where it could be beneficial for us to share the database rather than going through a middleman.

Outline:

00:00 Agenda
03:13 Introduction
04:14 Advantages of a sharing a database
06:55 Challenge 1: External parties getting internal details
10:30 Challenge 2: Replicating business logic
13:31 Challenge 3: Risk of data corruption and deletion
14:50 Challenge 4: Abusing the shared database
16:27 Should we share the database then?

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes]()
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