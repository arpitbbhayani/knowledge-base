Synchronous and Asynchronous Communication between Microservices
===


Say, we are building a Social Network and anytime someone reacts to your post, you need to be notified. So, how should the Reaction service talk to the Notification service to send out a notification?

The communication would be much simpler and reliable, just a function call if it was a monolith; but things become tricky as we go distributed.

Microservices need to talk to each other to exchange information and get things done; and there are two categories of communication patterns - Synchronous and Asynchronous.

## Synchronous Communication

Communication is synchronous when one service sends a request to another service and waits for the response before proceeding further.

The most common implementation of Sync communication is over HTTP using protocols like REST, GraphQL, and gRPC.

### Advantages of Synchronous Communication

- It is simple and intuitive
- Communication happens in realtime

### Disadvantages of Synchronous Communication

- Caller is blocked until the response is received
- Servers need to be pro-actively provisioned for peaks
- There is a risk of cascading failures
- The participating services are strongly coupled

### When to use Synchronous Communication

- When you cannot proceed without a response from the other service
- When you want real-time responses
- When it takes less time to compute and respond

## Asynchronous Communication

The communication is asynchronous when the one service sends a request to another service and does NOT wait for the response; instead, it continues with its own execution.

Async communication is most commonly implemented using a message broker like RabbitMQ, SQS, Kafka, Kinesis, etc.

### Advantages of Asynchronous Communication

- Services do not need to wait for the response and can move on
- Services can handle surges and spikes better
- Servers do not need to be proactively provisioned
- No extra network hop due to Load Balancer
- No request drop due to target service being overwhelmed
- Better control over failures and retires is possible
- Services are truly decoupled

### Disadvantages of Asynchronous Communication

- Eventual consistency
- Broker could become a SPoF
- It is harder to track the flow of the message between services

### When to use Asynchronous Communication

- When delay in processing is okay
- When the job at hand is long-running and takes time to execute
- When multiple services need to react to the same event
- When it is okay for the processing to fail and you are allowed to retry
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Synchronous and Asynchronous Communication between Microservices](https://i.ytimg.com/vi/ewUw0sUxHI4/mqdefault.jpg)](https://www.youtube.com/watch?v=ewUw0sUxHI4)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

How should two microservices talk to each other? Picking the right communication pattern is super-important as a good decision will ensure a great user experience and scalability while a bad one will ruin the party.

There are overall two categories of communication: Synchronous and Asynchronous; In this video, we in-depth discuss what synchronous communication is and how it is done, what asynchronous communication is and how it is done, the advantages and disadvantages of both of them, and most importantly understand how to decide which one to opt for with some real-world examples.

Outline:

00:00 Agenda
03:08 Need for Communication between Microservices
05:10 Synchronous Communication
08:17 Advantages of Synchronous Communication
09:07 Disadvantages of Synchronous Communication
15:58 When to use Synchronous Communication
18:40 Asynchronous Communication
23:01 Advantages of Asynchronous Communication
31:41 Disadvantages of Asynchronous Communication
34:39 When to use Asynchronous Communication

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/16T1TszFP0yXXxFWAk9wQnzii5JIeo5O2/view?usp=sharing)
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

<img width="256px" src="https://edge.arpitbhayani.me/img/arpit.jpg" />

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