Introduction to RPC - Remote Procedure Calls
===


What are Remote Procedure Calls? How were they conceptualized? and Why are people adopting them? Here's why 👇‍

The two services need to communicate with each other so as to get things done. The most common way to do it today is to make a REST call over HTTP to the other service.

With this approach, every service needs to write logic to make HTTP call to the other service and handle things like failures, retries, compression, and security. Can we not abstract these complexities in some way?

RPCs were conceptualized to solve this problem.

## Remote Procedure Calls

RPCs are designed to make remote network calls look and feel like local procedures. They abstract out all the complexities of remote invocations like Marshalling, Unmarshalling, Compressions, Retries, Security, etc.

RPCs achieve this level of coherence using Stubs that sit in between the two services and convert incoming and outgoing packets into native objects.

## Stubs

Stubs are the common piece of auto-generated code that defines the interface, in a given language, exposed by the server, and used by the client to consume the data.

The interface is defined in a common language like Protobuf and holds the information about functions that the server exposes and the request response object types. A generator is shipped with the RPC runtime that would take this interface and generate code in the target language.

For example, if the Auth service is written in Golang, the generator would generate a working code with the interface along with the transport details. This way, we can solely focus on writing the business logic and not worry about the network or other repetitive things.

## Communication RPC

RPC can use any transport protocol for communication - Raw TCP, UDP, HTTP 1.1, or even HTTP 2. The transport is just a way through which the marshaled information will be sent across systems; and depending on the features an RPC runtime plans to support, an appropriate protocol will be chosen.

## Advantages of using RPC

- easy to use
- strong API contract
- remote invocations are just local function calls
- cross language communication is a breeze
- mundane tasks like retries, compression, etc are abstracted
- get performance out-of-the-box - streaming, connection pool
- security is just a plug
- no need to write client libraries, they can be auto-generated

## Concerns while adopting RPC

- stubs need to be re-generated whenever the signature changes
- testing RPC is n trivial for beginners
- getting started can be a little challenging
- browser support for RPC is pretty limited
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Introduction to RPC - Remote Procedure Calls](https://i.ytimg.com/vi/eRndYq8iTio/mqdefault.jpg)](https://www.youtube.com/watch?v=eRndYq8iTio)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

One of the most interesting things that revived itself after a decade is Remote Procedure Calls, fondly called as RPCs; and they are widely adopted to do inter-service communication over the network.

The core highlight that sets RPCs apart is that they are designed to make the network call look just like a local function call. It does this by abstracting out all the complexities like serialization, deserialization, and transport.

In this video, let's take an in-depth look into what RPC is, where it fits, what are stubs, how communication happens between the services, and conclude by going through the advantages and disadvantages of using RPCs.

Outline:

00:00 Agenda
03:01 Introduction to Inter-Service Communication
03:43 Why RPCs were conceptualized?
08:50 What is RPC?
11:42 What are stubs in RPC?
17:07 Interface Definition and Stub Generation
22:09 Communication in RPC
22:57 Advantages of using RPC
29:16 Concerns while using RPC

https://github.com/arpitbbhayani/grpc-advcalc

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1UiyrR6YbvzWa_yTzXlSIL-lvaS23eMED/view?usp=sharing)
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