Why do programming languages need automatic garbage collection?
===


Our programs need memory, typically in the form of variables and objects, to do their job. The objects are either allocated on Stack or Heap.

## Stack allocated objects

A locally declared variable "int a = 10;" is allocated on the stack i.e. the stack frame of the function call and hence when the function returns the stack frame is popped, making the variable non-existent. Hence variables allocated on Stack do not need to be freed explicitly.

## Heap allocated objects

A variable allocated on the heap is typically done through functions like the "new" or "malloc". The object space allocated for such entities is in RAM and they outlive the function scope and execution, and hence they need to be explicitly freed as we are done with it.

## Why do we need a Heap?

Objects assigned on Heap need to be garbage collected, but why do we need the heap in the first place? There are 3 main reasons:

 - We cannot grow your stack-allocated objects dynamically,
 - We need dynamically growing objects like Arrays, LinkedList, Trees
 - We might need objects that could be larger than what Stack can fit in
 - We might need to share the same object across multiple threads
 - We do not want our functions to copy and pass bulk objects

## Garbage Collection: Explicit De-allocation

Primitive programming languages like C and C++ do not have their garbage collection instead expect the developer to not only allocate the object but also deallocate it explicitly. Hence we see the functions like "malloc" and "free".

The objects we allocate using "malloc" will continue to exist unless they are reclaimed using "free". The explicit need to "Free-ing" the allocated object is called Explicit Deacclocation.

Although cleaning up the mess we created is a good idea, it is not reliable that we rely on the engineers and developers to always free the objects they allocated. Hence this gives rise to the need for automatic cleanup of unused variables- automatic garbage collection.

The two key side-effects of not cleaning up the unused objects we allocate are

- Memory Leak: Leading to an eventual process crash
- Dangling Pointer: Program behaving unpredictably

Hence, to reduce human error, and make the process more reliable and performant the runtimes of the programming languages implement their automatic garbage collection.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Why do programming languages need automatic garbage collection?](https://i.ytimg.com/vi/jcMxuLZCcqU/mqdefault.jpg)](https://www.youtube.com/watch?v=jcMxuLZCcqU)

We know how important Garbage Collection is for any programming language. So, today we explore why programming languages need automatic garbage collection in the first place?

In this video, we understand - the basics of memory management, the need to allocate objects on the heap, the constructs of explicit deallocation, what happens when we do not do our garbage collection well, and why we need automatic garbage collection.

Outline:

00:00 Basics of Memory Management
04:39 Why do we need heap allocations?
06:59 Explicit Deallocation constructs
09:26 Memory leak - when we do not delete an allocated object
11:00 Dangling pointer - when we dereference an already freed object
15:08 Why we need automatic garbage collection

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1vdsTC6j4eDJFzcTOhhIM0JQOR2fW1l61/view?usp=sharing)
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