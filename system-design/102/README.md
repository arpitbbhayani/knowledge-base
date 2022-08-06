Implementing Idempotence in a Payments Microservice
===


Idempotence is executing the same action multiple times, but the result is as if the operation was applied just once.

Example: Double tapping a post multiple times on Instagram does not increase the like count. It just increases the first time and by 1.

Idempotence becomes extremely critical when money is involved. If A wants to transfer money to B, the transfer should happen just once. If due for any reason, the payment is implicitly retried, the funds will be deducted twice, which is unacceptable.

### Why would a transaction repeat?

Before we talk about idempotence, it is important to understand why it would repeat in the first place.

Consider a situation where the payments service initiated a payment with a Payment Gateway, the money got deducted, but the payments service did not get the response. This would make the Payments service retry the API call, which would lead to a double deduction.

## Implementing idempotence

Check and Update: Weave everything with a single ID.

The idea is to retry only after checking if the payment is processed or not. But how do we do this? The implementation is pretty simple- a global payment ID that weaves all the services and parties together.

The flow is:

1. Payments service calls the PG and generates a unique Payment ID
2. Payments service passes this ID to the end-user and all involved services
3. Payments service initiates the payment with Payment Gateway with this ID specifying the transfer between A and B
4. If there are any failures, the Payment service retries and in that request specifies the Payment ID
5. Using the payment ID, the payment gateway checks if the transfer was indeed done or not and would transfer only when it was not done

Although we talked about the Payments service here, this approach of implementing idempotence is pretty common across all the use cases. The core idea is to have a single ID (acting as the Idempotence Key) weaving all the involved services and parties together.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Implementing Idempotence in a Payments Microservice](https://i.ytimg.com/vi/m6DtqSb1BDM/mqdefault.jpg)](https://www.youtube.com/watch?v=m6DtqSb1BDM)

Idempotence is an extremely critical property that we must consider while implementing an API or designing a microservice. The situation becomes even more critical when the money is involved - ensuring no matter how many times the user or internal service retries, the amount is transferred just once between the two users in one transaction.

This video looks at idempotence, why there is even a need for it, and, more importantly, one common implementation approach commonly observed in payments services.

Outline:

00:00 What is Idempotence?
02:32 Examples where Idempotence is relevant
04:06 Why do we even need to retry?
07:18 Implementation Approach 1: Do not retry
09:45 Implementation Approach 1: Check and Update

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1Zyt8qN11IiAZJKrdan4wi1c5J6n_eAyU/view?usp=sharing)
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