Designing Idempotent API Endpoints for Payments at Stripe
===


In the world of payments, reliability and consistency are crucial. Customers expect their transactions to be processed accurately and efficiently, without any errors or duplicates. However, in a distributed system, failures can occur, and the same request can be sent multiple times.

For example, consider a payment service API that transfers money from one user to another. No matter where the failure occurs, the system needs to ensure that one request is processed exactly once; leading us to build idempotent APIs.

## Idempotent APIs

An idempotent API is an API that can be called multiple times, but the result will always be the same. If a request is made twice or more, the API will only perform the operation once, ensuring that there are no duplicates or errors.

However, designing an idempotent API is not a trivial task. There are many things to consider, such as handling errors, passing idempotency keys, and maintaining consistency.

## Core idea implementation

The core idea behind item potency keys is straightforward. Before making an API call, the client talks to the server to generate a random ID, which serves as the idempotency key.

The client then passes this key in all future requests to the server. The server stores the key and the purpose of the request in a backend database.

When the server receives a request, it extracts the idempotency key and checks if it has already processed the request. If it has, the server ignores the request. If it hasn't, the server processes the request and deletes the idempotency key.

This gives us the much-needed exactly-once processing.

### Handling Errors

When designing an idempotent API, we need to consider what to do in case of failure. Depending on the application usecase and the transaction state, we can choose to

- ignore the failure,
- pass the error to the user, or
- retry the request.

Retrying the request is often preferred because it provides a better user experience. However, we need to be careful when retrying requests, as we could end up processing the same payment multiple times.


## Passing the keys

There are several ways to pass the idempotency key to the server, such as using request headers or query parameters. Stripe, a popular payment processing company, requires clients to pass idempotency keys in request headers named `Idempotency-Key`.

## Database decisions

It is recommended to use a separate database or table to store idempotency keys to ensure that the server can quickly validate the processing status and load isolation.

## Conclusion

In conclusion, designing an idempotent API for payments is crucial for ensuring reliability and consistency. By using idempotency keys, we can avoid processing the same payment multiple times.

This approach can significantly improve the reliability and user experience of your API, making it a must-have for any critical API that needs to be executed exactly once, no matter what.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Designing Idempotent API Endpoints for Payments at Stripe](https://i.ytimg.com/vi/J2IcD9FZvZU/mqdefault.jpg)](https://www.youtube.com/watch?v=J2IcD9FZvZU)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Say, you are writing a payment service and you wrote an API that transfers money from one account to another. Because of a network glitch, the client retried the API call, and this led to the deduction of money twice. To handle this situation we need our APIs to be Idempotent.

In this video, we take a look at what idempotent APIs are, how to write them, and how they form the heart and crux of any payment service.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/12mM4QJvkgVdFn7CKSLshQuzBlbEn0kQU/view?usp=share_link)
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