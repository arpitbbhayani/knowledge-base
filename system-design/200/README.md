How Razorpay scaled their notification system
===


Delivery of notifications is critical for a FinTech company like Razorpay because it is a way to notify customers about their transactions and connect with external systems through Webhooks.

So, how did they design their notification system? let's find out

## Key requirement

1. maintaining an SLA is very important
2. guaranteed delivery via SMS, Email, Push, and Webhooks

## Existing Setup

Upon every transaction, an event/message was sent to SQS (message broker) which was consumed by a worker that then fanned out the notification through different channels.

Because we want to guarantee delivery, a state was maintained in the database that tells if the notification was successfully sent or not (esp via Webhook).

Hence, there is a component called Scheduler that pulls the unsent notifications from this database and re-queues it in SQS; thus guaranteeing the delivery.

### Challenges at scale

1. huge load on this database
2. scaling workers were limited by the IPOS on the database
3. surges, during festive seasons, affected transactional notifications

## New architecture

1. Prioritising incoming load

In order to ensure that one type of notification does not affect others, every notification type is classified with some priority and depending on which they are pushed to the corresponding SQS queue.

This ensures that a huge marketing campaign does not affect transactional messages.

2. Rate Limiting

To ensure mass notification from one customer does not affect others, we add Rate Limiter that would limit the notifications per customer and per type ensuring that critical notifications always meet the SLA.

3. Reducing DB bottleneck

We could not scale workers because of high DB load, and hence instead of doing a sync write to the database, the notifications that are unsent and need to be retried are pushed in a sync way to the database.

Because of this async write, we ensure that we write to the database in a staggered way and not put unnecessary load on it.

### Observability

To ensure we are maintaining our SLA, we have to exhaustively monitor the entire infra for any anomaly; the metrics like - health of the infra, success rate of delivery, and SLA.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How Razorpay scaled their notification system](https://i.ytimg.com/vi/DQwlmTvs6xA/mqdefault.jpg)](https://www.youtube.com/watch?v=DQwlmTvs6xA)

Notifications are extremely crucial for Fintech companies as it is a way to notify a user about an incoming transaction. Hence it becomes extremely important for companies like Razorpay to ensure that notification is delivered to a user within a certain amount of time.

In this video, we take a detailed look into how Razorpay scaled their notifications systems, and look at their high-level architecture and key design decisions they made along the way to ensure they always meet the SLA.

Outline:

00:00 Agenda
02:37 Existing notification system
08:54 Re-architecting notification system

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1423Wn1CrO0goeiYuQo8DpUhrWbfR6KDs/view?usp=sharing)
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