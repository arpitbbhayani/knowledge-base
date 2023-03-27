How to pick a garbage collector?
===


"Best" Garbage Collector is a myth.

If you are ever writing your Garbage Collector or trying to pick one for your workload, there are 7 metrics that you should be evaluating a GC algorithm on.

No one garbage collector can be the best across all 7 properties and it was found that any GC algorithm is at least 15% better than other algorithms on at least one of the characteristics. Hence it all boils down to the needs of your specific workload to pick one over the other. The key characteristics are

## Safety

A garbage collector is safe when it never reclaims the space of a LIVE object and always cleans up only the dead objects.

Although this looks like an obvious requirement, some GC algorithms claim space of LIVE objects just to gain that extra ounce of performance.

## Throughput

A garbage collector should be as little time cleaning up the garbage as possible; this way it would ensure that the CPU is spent on doing actual work and not just cleaning up the mess.

Most garbage collectors hence run small cycles frequently and a major cycle does deep cleaning once a while. This way they maximize the overall throughput and ensure we spend more time doing actual work.

## Completeness

A garbage collector is said to be complete when it eventually reclaims all the garbage from the heap.

It is not desirable to do a complete clean-up every time the GC is executed, but eventually, a GC should guarantee that the garbage is cleaned up ensuring zero memory leaks.

## Pause Time

Some garbage collectors pause the program execution during the cleanup and this induces a "pause". Long pauses affect the throughput of the system and may lead to unpredictable outcomes; so a GC is designed and tuned to minimize the pause time.

The garbage collector needs to pause the execution because it needs to either run defragmentation where the heap objects are shuffled freeing up larger contiguous memory segments.

## Space overhead

Garbage collectors require auxiliary data structures to track objects efficiently and the memory required to do so is pure overhead. An efficient GC should have this space overhead as low as possible allowing sufficient memory for the program execution.

## Language Specific Optimizations

Most GC algorithms are generic but when bundled with the programing language the GC can exploit the language patterns and object allocation nuances. So, it is important to pick the GC that can leverage these details and make its execution as efficient as possible.

For example, in some programming languages, GC runs in constant time by exploiting how objects are allocated on the heap.

## Scalability

Most GC are efficient in cleaning up a small chunk of memory, but a scalable GC would run efficiently even on a server with large RAM. Similarly, a GC should be able to leverage multiple CPU cores, if available, to speed up the execution.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How to pick a garbage collector?](https://i.ytimg.com/vi/IojMqbegejk/mqdefault.jpg)](https://www.youtube.com/watch?v=IojMqbegejk)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

"Best" Garbage Collector is a myth.

If you are building your Garbage Collector or trying to pick the best for your use case, 7 parameters would help you objectively make the decision. These parameters define a Garbage Collector and determine its performance.

In the previous video we talked about why languages need an automatic garbage collection - primarily because engineers are unreliable, and in this one, we talk about the 7 key metrics and characteristics of a Garbage Collector that can help us compare and judge which one is better than the other for a specific workload;
 
Something all senior engineers spend their time on to get the performance out of their systems.

Outline:

00:00 Introduction
03:13 7 Characteristics and Metrics of a Garbage Collector
06:53 Safety
08:21 Throughput
11:12 Completeness
12:52 Pause Time
17:44 Space Overhead
19:58 Language-Specific Optimizations
22:27 Scalability

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1eHwPYsx-k61JoLCz4FudN4DFZMAe-_3j/view?usp=sharing)
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