How Airbnb designed and scaled its central authorization system - Himeji
===


Building a central, robust, extensible and highly available authorization service is no joke

and @Airbnb does it beautifully

here's a thread about its architecture and key design decisions... 🧵👇

## What is authorization?

It is all about managing fine-grained control over different entities, example:

- can user A edit comment C?
- can user B access hotels in region R?
- can user C read a file in folder F shared with group G?

why do we need a service for this?

## Why a central service?

If each microservice handles its own authorization, then there would be

- duplication of auth logic
- inter-service calls to check for auth

hence, it is beneficial to create a central auth service. Let's see how it is modeled.

## Auth model

- Principal: user or service that needs to be tested
- Entity: on which we are checking the access
- Relation: between entity and principal

can user A edit comment C?

A - is the principal,
C - is the entity, and
edit - is the relation

The tuple is represented and (optionally stored) in the database as

```
<entity> # <relation> @ <principal>
```

if user A has owner privileges on comment C, it will be represented (and optionally stored) as

```
C # OWNER @ A
```

Storing one entry for each entity and relation will make the data explode, For example:

if A owns a comment C, then he/she can read and write to it as well. This would make us have 3 entries in the database

- `C # READ @ A`
- `C # WRITE @ A`
- `C # OWNER @ A`

hence...

we need a way to define relations between relations and entities to reduce the size of the data.

A simple YAML-based config would look like this

```
LISTING:

  # WRITE:
    union:
      - # WRITE
      - # OWNER

  # READ:
    union:
      - # READ
      - # WRITE
```

The above configuration imples,

1. WRITE relation is a union of WRITE and OWNER
2. READ relation is a union of READ and WRITE

Anyone with the write and owner relation can write and anyone with read and write (and transitively owner) relations can read the listing on Airbnb.

To check if user A can read listing L, we hit

```
check (listing:L, READ, user:A)
```

It evaluates as

- LISTING:L # READ @ user:A
- LISTING:L # WRITE @ user:A
- LISTING:L # OWNER @ user:A

because of `union`, if anyone of these exists in DB, `check` evaluates to True.

## Architecture

Himeji (authorization) service is consist of 3 layers

1. Data Layer
2. Caching Layer
3. Orchestration Layer

Let's take a detailed look at each in detail.

### Data Layer

The data layer of the Himeji service consists of

- persistent relational database
- data is logically shared within the same instance
- any mutation in the data is read through CDC, streamed through Kafka, and used in invalidating the cache

### Caching Layer

The caching layer of the Himeji service is super-critical for performance as it ensures low response time at scale.

- ensures 98% hit ratio
- cache cluster is sharded
- consistent hashing determines the data ownership across the cluster

### Orchestration Layer

The orchestration layer is used by clients and internal jobs to interact with the service. The layer

- forwards reads to caching
- forwards the writes to the data layer
- computes response as per the config

This design is taken from @Airbnb's Engineering Blog and it is linked in the description of the video attached.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How Airbnb designed and scaled its central authorization system - Himeji](https://i.ytimg.com/vi/5FIPtC3xJSQ/mqdefault.jpg)](https://www.youtube.com/watch?v=5FIPtC3xJSQ)

Authorization plays a critical role in ensuring that the platform is not abused. For example, Instagram ensures that if an account is made private, only the people allowed can see the posts from it. Such granular fine-grained access control requires a very robust and flexible authorization system.

In this video, we dive deep into how Airbnb achieves this through its in-house service named Himeji and explore its architecture and key design decisions that ensure robustness, extensibility, availability, and ability to scale to millions of users.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1qK0P95w7RxSnyKfh0tpf-oXiPXUf7wVM/view?usp=share_link)
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