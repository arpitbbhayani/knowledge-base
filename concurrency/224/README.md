Writing efficient and fair multi threaded programs with hands on examples
===


Writing concurrent programs can be easy, but ensuring their correctness and optimality can be tricky, especially when dealing with multi-threaded programs. In this article, we'll discuss some best practices for writing good multi-threaded programs that are both correct and efficient.

## Ensuring Correctness: Locking and Atomic Instructions

When dealing with multi-threaded programs, it's important to ensure that the program's correctness is maintained even when multiple threads are accessing the same resources simultaneously. This is where locking and atomic instructions come into play.

Locking is a technique used to synchronize access to shared resources. By using locks, we can ensure that only one thread can access a shared resource at a time, thus preventing race conditions and ensuring correctness.

Atomic instructions, on the other hand, are low-level operations that are executed atomically, meaning that they are indivisible and can't be interrupted by other threads. These operations are useful when updating shared resources, as they ensure that the update is performed atomically and that no other thread can interfere with the update.

## Ensuring Optimality: Fairness and Efficient Logic

In addition to ensuring correctness, it's also important to ensure that our multi-threaded programs are efficient and optimal. One way to achieve this is by ensuring fairness, which means that all threads are given an equal chance to execute and that no thread is starved and all threads complete nearly at the same time.

## Counting prime numbers

For example, let's consider the problem of counting prime numbers to 200 million. We can use a sequential approach to check each number for divisibility by any of its peers. However, this approach can be slow and inefficient. By adding threads, we can speed up the process, but it's important to ensure that the workload is evenly distributed among the threads to avoid bottlenecks.

### Approach 1: Threads handling a range

We can divide the workload among 10 threads, with each thread handling an equal range of numbers. But this isn't optimal.

The smaller numbers can be quickly checked for primality which means the threads handling larger numbers will take longer to complete.

### Approach 2: Threads as workers

Let's have a global variable called `currentNum`, which is updated atomically to keep track of the next unprocessed number.

Each thread can then loop until all numbers have been processed, incrementing `currentNum` atomically to check the next unprocessed number for primality.

By using this approach, we can ensure both correctness and optimality, with all threads completing their work nearly simultaneously.

## Conclusion

In summary, writing good multi-threaded programs requires careful consideration of correctness and optimality.

By using locking and atomic instructions, we can ensure correctness, while threading with fairness and efficient logic can ensure optimality. With these best practices in mind, we can write multi-threaded programs that are both correct and efficient.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Writing efficient and fair multi threaded programs with hands on examples](https://i.ytimg.com/vi/2PjlaUnrAMQ/mqdefault.jpg)](https://www.youtube.com/watch?v=2PjlaUnrAMQ)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Writing a multi-threaded program is easy, but writing an efficient multithreaded program is difficult. In this video, we take a look at a hands-on example to understand how to write good multi-threaded programs that are not only fast but also efficient and optimal.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1inBtu78zfjMMooxUfRZsajWsUqovFTyO/view?usp=share_link)
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