Mark and Sweep Garbage Collection Algorithm
===


The Mark-and-Sweep garbage collection algorithm is one of the most common and widely adopted garbage collection algorithms out there. It leverages the power of Graph data structure along with DFS to power the cleanup.

Almost all programming languages support allocating objects in heap and referring them via pointers to another object. This reference creates a small graph of all the references linked to the one root node.

The root node could be a global variable (object) or something allocated on the thread stack, and anything and everything referenced from that becomes the child nodes and the process continues.

### Indirect Collection Algorithm

The mark-and-Sweep garbage collection algorithm is an indirect collection algorithm, which means it does not have any direct information about the garbage, instead, it identifies the garbage by eliminating everything LIVE.

## When is the GC triggered?

The garbage collection is triggered when the runtime environment is unable to allocate any new object on the heap. When the language tries to fire `new` and it is unable to allocate space, it first triggers a quick garbage collection and then tries to re-allocate; if not successful again it throws an OutOfMemory exception, and in most cases, it is a fatal error.

## Mark-and-Sweep Algorithm

Although the algorithm is primarily split into two phases Mark and Sweep; to build a better understanding we split it into 4.

### Prepare the root list

The first step of this algorithm is to extract and prepare the root list, and the roots could be global variables or variables referenced in the thread stack. These become the seed objects on which we then trigger a DFS.

### Mark the roots and proceed

Once we identified all the roots, we mark all the roots as `LIVE` and proceed with the Mark phase. A super optimization that some implementations apply is to invoke the Mark phase for every root as it would help us keep the stack smaller.

### Mark

The mark phase is just a Depth First Search traversal on one root node and the idea is to mark every node as `LIVE` that is reachable from the root node. Once all the nodes are marked, we can conclude that the nodes that remain unmarked are garbage; and the ones to be cleaned up.

### Sweep

The nodes left unmarked are the garbage and hence in the sweep phase, the GC iterates through all the objects and frees the unmarked objects, and resets the marked object to prepare them for the next cycle.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Mark and Sweep Garbage Collection Algorithm](https://i.ytimg.com/vi/4qLf0FJMyf0/mqdefault.jpg)](https://www.youtube.com/watch?v=4qLf0FJMyf0)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Garbage Collection has to be one of the most interesting topics of discussion out there. In the previous videos, we took a look at why programming languages need an automatic garbage collection and what are the key metrics and characteristics we look at while picking one.

In this video, we take a detailed look into one of the most common GC algorithms out there called Mark-and-Sweep. We will talk about the two key phases of the algorithms, also dive into the important details and nuances of it, and take a look at two super-interesting optimizations that would algorithm a massive boost to the performance.

Outline:

00:00 Agenda
02:57 Introduction to the Mark and Sweep Algorithm
06:12 Mutator Threads, Collector Threads, and assumptions
09:30 When is Garbage Collector invoked?
13:11 Phase 1: Prepare the root list
14:35 Phase 2: Mark roots, proceed, and a super optimization
17:19 Phase 3: Mark and DFS Traversal
19:22 Phase 4: Sweep and a super optimization

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1_sCJpp4EQlk0GoAzsJEp06JYWEboAnom/view?usp=sharing)
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