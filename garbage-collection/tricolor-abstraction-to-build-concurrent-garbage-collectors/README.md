Tricolor Abstraction to build concurrent Garbage Collectors
===


The Mark and Sweep garbage collection algorithm is a simple DFS traversal with two phases - Mark and Sweep. In the mark phase, it marks all the objects that are reachable from the root, and the Sweep phase clears off all the unreachable ones.

This crude algorithm is slow and requires a program pause which means everything stops when the GC is cleaning up. This affects the performance and throughput of the program.

So, can we write a GC that runs concurrently with the program and does not need to always stop the world?

The foundation of concurrent Garbage Collector is based on a concept called Tricolour Abstraction which was developed by Dijkstra and Lamport, known for their work on core algorithms and distributed systems.

# States of an object

While tracing the objects across the heap we can see that each object can be in one of the 3 states: unprocessed, processing, and processed; and this becomes our three colors

White: unprocessed objects
Grey: visited but whose children are yet to be visited
Black: done processing

## The garbage collection flow

Every node starts white. Once we see an object we color it Grey and once we are done visiting its children we mark it Black. This way we have 3 sets of objects: white, great, and black, and the objects move from white to grey and from grey to black.

A key thing to note here is that we will never have an object that moves directly from white to black; i.e. there will never be an edge that connects one black and one white node.

## How does Tricoloration make it better?

Because a black node is never connected to a white node, we ensure correctness i.e. a live object will never be cleaned up.

Our GC flow can now be simplified as

- pick the object from the grey set
- color all the children of the node grey
- move the grey object to the black

repeat the flow until the grey set is empty. Once done, we can just visit the white set, which now contains all the unreachable objects, and clean them up.

## Speedup

Now that we segregated the objects into sets we can ensure a quick cleanup by putting more threads at work on the grey set. It is hard to make a crude DFS concurrent and structuring it as sets make implementation much simpler.

We make our system reactive by keeping an eye on the grey set and triggering GC as soon as it hits some threshold.

This method of garbage collection is called "on-the-fly" which runs concurrently with the program and mutates the color of the objects as part of program execution and does not wait for a separate GC cycle. This reduces the load on GC and minimizes the pause.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Tricolor Abstraction to build concurrent Garbage Collectors](https://i.ytimg.com/vi/lhrRwjVPXPo/mqdefault.jpg)](https://www.youtube.com/watch?v=lhrRwjVPXPo)

A basic Mark-and-Sweep garbage collection algorithm operates in Stop-the-World mode, which means the program execution pauses while the GC runs. So, can we write a GC that runs concurrently with the program and does not need to always stop the world?

In this video, we take a look into something foundational called the Tricolour Invariant that enables us to build concurrent garbage collectors with low pause times. The concept we discuss is something that was contributed by Dijkstra, famously known for his Shortest Path algorithm.

Outline:

00:00 Agenda
03:06 Recap of Mark and Sweep Garbage Collection
03:56 States of an object during GC
06:04 Tricolour Abstraction
09:07 How does Tricolor Abstraction make things better?
12:46 The Garbage Collection Flow with the Coloured Sets
15:06 Why did we do this at all?

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1k6y-oTQ3i46VUKs58qHRxK6QuG87z1-5/view?usp=sharing)
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