Overview of Discord's data platform that daily processes petabytes of data and trillion points
===


To handle trillions of data points and petabytes of data every single day, Discord needs a simple yet robust Data Platform.

Here's a quick overview of their arch and key design decisions 👇‍

## What is a Data Platform?

A data platform comprises a set of services that ensures data is replicated from various databases, put in central storage, and making it available for consumption by internal teams, and services.

Discord needs to analyze the data to

- make strategic business decisions
- power their machine learning models
- understand how people are using their product

### Why replicate data in one place?

- data is split across microservices
- firing queries that span multiple databases infeasible
- each microservice has its own flavor of database (SQL and NoSQL)

For example, firing queries across orders (MongoDB) and payments (MySQL) to get the items that generated the most revenue.

## Discrod's Data Platform - Derived

Discord uses Google's BigQuery as its Data Warehouse (a place to keep and query large volumes of data). The data is stored, processed, and consumed across 3 layers

1. Transactional Layer
2. Core Tables
3. Derived Tables

Let's understand each layer in detail.

### Transactional Layer

The transactional layer comprises the transactional databases used in powering the microservices. These databases typically act as a source of truth for the services.

Microservices are free to choose the flavor of the database - SQL or NoSQL to power their usecase.

### Core Tables

The core layer holds the series of tables in BigQuery that are populated using the transactional layer.

Data pipelines replicate the data from various transactional databases, like MongoDB, MySQL, etc into a set of structured core tables, and become the input for the subsequent Derived Layer.

### Derived Tables

Derived Tables are the actual consumable tables created from a set of core tables. Each team can create its own set of derived tables by joining a set of core tables as per their need.

Each derived table is essentially a SQL query on core tables. The specified SQL query is fired periodically to join and replicate the unprocessed data into a derived table.

Each derived table has its own configuration file that holds

- columns of the derived table
- schedule and window
- partition key, cluster key,
- dataset and SQL query

A replication strategy is also specified in the YAML file that implies if the output of the SQL query should append to, merge with, or replace the existing derived data.

A separate K8S pod is run for each derived table that ensures an isolated continuous data replication to the derived tables.

Thus, each team can define its own set of derived tables using just a SQL query, enabling teams to make data-driven decisions.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Overview of Discord's data platform that daily processes petabytes of data and trillion points](https://i.ytimg.com/vi/yGpEzO32lU4/mqdefault.jpg)](https://www.youtube.com/watch?v=yGpEzO32lU4)

When a company scales, they adopt microservices and each service typically gets its own independent database. With data being distributed across so many databases, there emerges a need to unify them to extract deep product insights, make strategic business decisions, and train ML, models.

In this video, we take a super-detailed look into how Discord built its unified Data Platform that processes trillions of data points and petabytes of data every single day.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1rnmNSk5GB9OSdMdxk7U-9TwMvwn3IRla/view?usp=share_link)
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