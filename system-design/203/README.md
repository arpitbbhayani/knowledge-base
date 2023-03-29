How Giphy uses CDN to serve a billion GIFs every day
===


GIPHY serves 10 billion GIFs every day, here's how it beautifully uses different features of CDN.

## What is CDN

Think of CDN as a geographically distributed cache; and just like any regular cache, it sits between the user and the origin.

For any request, if it has the data, it serves the response. If not, it hits the origin to grab the data, cache it, and then responds.

### Geographical Nearness

A key highlight of using a CDN is geographical nearness. Because the CDN servers are distributed worldwide, the request from a user is served from the nearest edge server giving an excellent UX.

## CDN for media content

This is a no-brainer application of CDN. Giphy serves all the media content like images and videos through CDN that sits transparently between the user and the origin (eg: S3).

## CDN for API responses

Apart from the media content, Giphy uses CDN to cache API responses of Search and Discover APIs like

- /v1/gifs/trending
- /v1/search?q=funny

It serves these APIs from CDN because the responses of these APIs do not change often; hence using CDN for this reduces the load on API servers.

## Route-specific TTL

Not all APIs or media objects need to be cached on CDN for the same amount of time. Hence Giphy configures different expirations for different types of APIs.

Media object endpoints are cached longer while trending API is cached for a shorter duration.

## Response-driven TTL

Sometimes, it is the backend server that should dictate for how long the response should be cached.

Hence, Giphy, in the HTTP response from the origin server provides `max-age` headers that tell CDN the TTL for the specific response. This gives finer control over key expiration.

## Cache invalidation by grouping

Giphy uses Surrogate Keys (tags) while caching endpoints on CDN. It helps in smarter cache invalidation, eg:

- invalidate API responses that contain a specific GIF
- invalidate API responses from an API key
- invalidate API responses where the query contains a particular query
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Giphy uses CDN to serve a billion GIFs every day](https://i.ytimg.com/vi/-bo7oVejgRM/mqdefault.jpg)](https://www.youtube.com/watch?v=-bo7oVejgRM)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Giphy is the world's most popular GIF website and it serves 10 billion media content every single day, and we can guess it would be using CDN to do that, but is that it?

In this video, we dive deep into how Giphy uses different features of CDNs to solve different kinds of problems; and while going through it we will also look at a super-interesting internal implementation detail of CDN.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1M2Id3sJb9ABbMGSU2WFqpexDzbrd2FEH/view?usp=sharing)
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