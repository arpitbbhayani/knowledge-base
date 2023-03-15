How Gojek masks and keeps users' phone numbers secure at scale?
===


Phone numbers can be misused if gone into the wrong hands. But sometimes delivery agents need to reach out to us for directions.

So, do delivery agents get our phone numbers?

Here's how Gojek ensures seamless communication without sharing actual phone numbers.

## Problem Statement

Say, customer A ordered something from Gojek and a delivery agent D gets assigned to this order.

We want to

- enable A to contact D
- enable D to contact A

but neither should have the other's phone numbers.

and we achieve this using...

## Virtual Phone Numbers

Instead of sharing the actual phone numbers of the users, we create virtual phone numbers which are

- temporary but functional
- can be assigned to any user at will

Telecom operators and providers like Twilio and Exotel provide these services.

### Is it for everyone?

If we assign a fixed VN to every user in the system

- does not improve the security posture
- we would need millions of virtual numbers

If VN remains the same for a user, then abusers can keep track, and attack the user; breaching their privacy.

## Constraints

Hence, the virtual numbers we assign to the users should be

- assigned on demand
- bound to a transaction/order

Once the transaction is over, or the order is delivered, we assign the VN to some other user.

so, how do we assign?

## Fetching Virtual Numbers

Instead of trying to get Virtual Numbers on the fly from the telecom operators and providers, we fetch them periodically and keep them handy in our database.

Say, we call this service VN service.

### Assigning Numbers

When a delivery agent is assigned to an order,

- we hit the VN database,
- fetch a couple of unused VN,
- and make an entry into the orders DB.

we show the assigned numbers on the app to the customer and the delivery agent.

If a user (customer/delivery agent) has multiple active orders, he/she will be assigned one VN for each active transaction.

Hence, if a delivery agent is delivering two orders at the same time, he/she will be assigned two VNs, ensuring privacy.

## Flow

A user places an order and the event is sent to Kafka, to be consumed by the consumers which ensure we have enough VNs available.

If not, more VNs are fetched from the telecom operators and providers.

Once the delivery agent is assigned to the order, the Kafka consumers fetch the VNs from the database and update the mapping in Orders DB.

This entry is used to render the phone number of the other party on the app.

so, what happens when a user calls the delivery agent's VN?

### Calling a VN

Say customer A wants to call the delivery agent D. Say, DDD is the virtual number of D that A has.

When A makes a call on the number DDD, the telecom provider gets the call and it needs the actual number to connect to.

Hence, it makes a call to the VN service. The VN service then checks

- who is calling
- to whom the call is made
- the existence of a valid transaction between A and D

once everything is validated, the VN service responds with A's VN and actual number against DDD.

The telecom provider then bridges the call that was initiated from A to the actual phone number of D but it sets the source phone number to VN of A.

This way, when the D receives the call, it does not see A's actual number, instead, it sees the VN of A.

This is how the customer and the delivery agent can connect over the phone call, while neither gets the actual phone number of the other.

This is exactly what Gojek does. The link to their blog is in the description of the attached video.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Gojek masks and keeps users' phone numbers secure at scale?](https://i.ytimg.com/vi/nEEaSZZ8R4I/mqdefault.jpg)](https://www.youtube.com/watch?v=nEEaSZZ8R4I)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Do hyperlocal companies like Uber, Ola, Swiggy, Gojek, Zomato, etc share our phone numbers with the delivery people or theirs with us? If they do then that would be a massive breach of privacy. Hence, they have a system in place that instead of sharing the actual phone numbers, share a masked version of it.

In this video, we talk about how these hyper-local companies work with telecom operators to generate virtual phone numbers and keep our privacy intact.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1c5p7d7rT9Fi2qoedmtZx9zo0dqCPvbBc/view?usp=share_link)
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