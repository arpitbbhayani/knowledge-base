What are Embedded Databases?
===

<p align="center">
    <img src="https://media.giphy.com/media/uk3R91z24SoUZ27WTh/giphy.gif" width="320px" />
</p>


<p>What are Embedded Databases? [ in a gist ]</p>
<p>Traditional databases like MySQL, Postgres, MongoDB run on their server on a specific port. Anyone who wants to talk to the database can directly connect and talk.</p>
<p>Embedded Databases are different from these traditional databases, and they operate in their own confined space within a process. There is no separate process of the database.</p>
<p>No one can directly connect to this database, unlike how we do it with MySQL and other databases. The role and the use of the embedded database are limited to the process it is confined to.</p>
<p>✨ Popular embedded databases are</p>
<p>SQLite: an embedded SQL-like database
LevelDB: on disk KV store by Google
RocksDB: on disk KV store optimized for performance
Berkeley DB: KV store with ACID, Replication, and Locking</p>
<p>An embedded database is always designed to solve one niche really well.</p>
<p>✨ Application of Embedded Databases</p>
<p>Every modern browser uses an embedded database called IndexedDB to store browsing history and other configuration settings locally. The browser is confined to a machine, and the IndexedDB is contained in the browser; there is no separate process to connect to.</p>
<p>Every Android phone has support for SQLite database that we can use to store any information like game scores, stats, information locally on the phone.</p>
<p>The core idea: When we need to store and query data that could be confined within a space and does not need to be centralized, we choose to use an Embedded Database.</p>
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![What are Embedded Databases?](https://i.ytimg.com/vi/xELqRiovEcI/mqdefault.jpg)](https://www.youtube.com/watch?v=xELqRiovEcI)

<p>Embedded databases are coupled with the application they are part of and operate in a confined space. They are designed to solve one problem for their niche very well. In this video, we take an introductory look into this amazing class of databases, understand the core reason why they exist, talk about a few popular ones, and understand a few use cases.</p>
<p>Outline:
 - 00:00 Server-based Databases
 - 02:32 Embedded Databases
 - 06:35 Popular Embedded Databases
 - 10:39 Applications of Embedded Databases</p>

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1_iXh0rCmGVZJj5CLWP7gJ4YzAP-yIiGb/view?usp=sharing)
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