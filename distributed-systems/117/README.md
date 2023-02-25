Distributed Transactions: Two-Phase Commit Protocol
===


Distributed Transactions are essential to have strong consistency in a distributed setup.

An example could be as simple as a 10-min food/grocery delivery- where to guarantee a 10-min delivery, you can only accept orders when there are goods available in the dark store, and a delivery agent is available to deliver the goods.

This is a classic case of Distributed Transaction where you need a guarantee of atomicity and consistency across two different services. In a distributed setup, we can achieve it using an algorithm called Two-phase Commit.

The core idea of 2PC is: Split the transaction into two phases: Reservation and Assignment.

## Phase 1: Reservation

The Order service will first talk to store service to reserve food items and delivery service to reserve a delivery partner. When the food or delivery partner is reserved, they are not notified. By reserving them, we are just making them unavailable for everyone else.

If the order service fails to reserve any of these, we roll back the reservation and abort the transaction informing the user that the order is not placed. Reservation comes with a timer, which means if we cannot assign a reserved food item to order in "n" minutes, we will be releasing the reservation, making them available for other transactions.

We move forward to the Commit phase only when the order service reserves both- a food item and a delivery agent.

## Phase 2: Commit

In the Commit phase, the order services reach out to the store service and the delivery service to assign the food and agent to the order. Because the food and the agent were reserved, no other transaction could see it, and hence with a simple assignment, we can get the reserved food and agent assigned to an order.

Upon this assignment, the store and the delivery agent are notified about the order and proceed with their respective duties.

We retry a few times if any of the assignments fail (which could happen only if the service goes down). If we still cannot get the assignment done, we inform the user that the order cannot be placed.

The order is placed only after the food item, and the delivery agent is assigned to the order.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Distributed Transactions: Two-Phase Commit Protocol](https://i.ytimg.com/vi/7FgU1D4EnpQ/mqdefault.jpg)](https://www.youtube.com/watch?v=7FgU1D4EnpQ)

Distributed Transactions are tough and intimidating. It is hard to guarantee atomicity across microservices given the network delays, resource contention, and unreliable services.

In this video, we discuss and take a detailed look into Distributed Transactions, understand why they are needed with a real-world example of Zomato's 10-minute food delivery, and build our understanding of the workings of the Two-Phase Commit protocol.

Outline:

00:00 Why Distributed Transactions
03:44 Atomicity in Distributed Transactions
06:47 Two-Phase Commit Protocol for Distributed Transactions
18:29 Advantages and Disadvantages of Two-Phase Commit

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/18WDFAstffIe_vGbtTz_CS117XhvDcBx3/view?usp=sharing)
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