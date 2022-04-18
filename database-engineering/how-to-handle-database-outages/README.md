How to handle database outages?
===


How to handle database outages?

Why a database goes down?
An unexpected heavy load on your database can lead to a process crash or a massive slowdown.

Before jumping to the potential short-term and long-term solutions, ensure you monitor the database well. CPU, Memory, Disk, and Connections are being closely monitored.

✨ Short term solutions

- Kill the queries that have been running for a long time
- Quickly scale up your database if you have been seeing a consistent heavy usage
- Check if the recent deployment is the culprit; if so, revert asap
- Reboot the database will calm the storm and buy you some time

✨ Long term solutions

- Ensure the right set of indexes are in place
- Tune your database default parameters to gain optimal performance
- Check for the notorious N+1 Queries
- Upgrade the database version to get the best that DB can offer
- Evaluate the need for Horizontal scaling using Replicas and Sharding


In this video, we talk about why a database goes down, what happens when the database is down, a few short-term solutions to minimize the downtime, and a few long-term solutions that you should be doing to ensure that your database does not go down again.

Outline:

 - 00:00 Why a database goes down?
 - 06:10 What happens when a DB is down?
 - 09:46 Short-term solutions to get your DB up
 - 17:33 Long-term solutions to fix the database

[![How to handle database outages?](https://i.ytimg.com/vi/UT_TVldzA64/mqdefault.jpg)](https://www.youtube.com/watch?v=UT_TVldzA64)


# Notes

The notes used in the video is can be found in the current folder and on [Google Drive](https://drive.google.com/file/d/1Q6YokLBvmfW1Tw1mpndOfx-I2NyRGVG0/view).


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