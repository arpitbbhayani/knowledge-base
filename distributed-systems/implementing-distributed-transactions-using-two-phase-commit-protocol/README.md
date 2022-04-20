Implementing Distributed Transactions using Two Phase Commit Protocol
===


<p>Implementing Distributed Transactions ⚡ [in a gist]</p>
<p>Distributed Transactions are not theoretical; they are very well used in many systems. An example of it is 10-min food/grocery delivery.</p>
<p>Previously we went through the theoretical foundation for the Two-phase commit protocol; in this one let's spend some time going through the implementation detail and a few things to remember while implementing a distributed transaction.</p>
<p>✨ The UX we want is: Users should see orders placed only when we have one food item and a delivery agent available to deliver.</p>
<p>A key feature we want from our databases (storage layer) is atomicity. Our storage layer can choose to provide it through atomic operations or full-fledged transactions.</p>
<p>We will have 3 microservices: Order, Store, and Delivery.</p>
<p>An important design decision: The store services have food, and every food has packets that can be purchased and assigned. Hence, instead of just playing with the count, we will play with the granular food packets while ordering.</p>
<p>✨ Phase 1: Reservation</p>
<p>Order service calls the reservation API exposed on the store and the delivery services. The individual services reserve the food packet (of the ordered food) and a delivery agent atomically (exclusive lock or atomic operation).</p>
<p>Upon reservation, the food packet and the agent become unavailable for any other transaction.</p>
<p>✨ Phase 2:</p>
<p>Order service then calls the store and delivery services to atomically assign the reserved food packet and the delivery agent to the order. Upon success assigning both to the order, the order is marked as successful, and the order service returns a 200 OK to the user.</p>
<p>The end-user will only see "Order Placed" when the food packet is assigned, and the delivery agent is assigned to the order. So, all 4 API calls should succeed for the order to be successfully placed.</p>
<p>Negative cases:</p>
<ul>
<li>If any reservation fails, the user will see "Order Not Placed"</li>
<li>If the reservation is made but assigning fails, the user will see "Order Not Placed"</li>
<li>If there is any transient issue in any service during the assignment phase, APIs will be retried by the order service to complete the order.</li>
<li>To not have a perpetual reservation, every reserved packet and delivery agent will have an expiration timer that will be large enough to cover transient outages.</li>
</ul>
<p>Thus, in any case, an end-user will never experience a moment where we say that the order is placed, but it cannot be fulfilled in the backend.</p>
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Implementing Distributed Transactions using Two Phase Commit Protocol](https://i.ytimg.com/vi/oMhESvU87jM/mqdefault.jpg)](https://www.youtube.com/watch?v=oMhESvU87jM)

<p>Previously, we built a theoretical foundation of Distributed Transaction using the Two-Phase Commit protocol. In this video, we implement the Distributed Transaction locally and mimic the food delivery system locally. While implementing we understand how to make the individual operations atomic and the entire distributed transaction atomic. We address resource contention while guaranteeing a consistent user experience.</p>
<p>Outline:</p>
<ul>
<li>00:00 Revising the Two-Phase Commit</li>
<li>07:35 Designing Database Schema</li>
<li>11:40 Defining API Endpoints</li>
<li>12:24 High-Level Architecture and Request Flow</li>
<li>19:55 No inconsistent data - Atomicity</li>
<li>24:14 Code walkthrough</li>
</ul>

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/18q2ELr9n6GCemKbJ0aS7q7NyF7wX1kL9/view?usp=sharing)
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