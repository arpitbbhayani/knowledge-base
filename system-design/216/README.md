Thundering Herd Problem and How not to do API retries
===


When a user makes an API call to the backend and encounters a network issue causing the call to fail, one common solution is to retry the call assuming that the APIs are idempotent.

However, when multiple clients simultaneously retry their calls, it can cause a "Thundering Herd" problem, overwhelming the server and making it difficult to recover. In this article, we will discuss how to address this issue by implementing Exponential Backoff and Jitter.

## Retrying is brutal

The simplest way to retry failed API calls is to repeat the call immediately in a loop for a specified number of attempts. However, this approach can make the problem worse at scale.

Imagine the server is already overwhelmed with requests, and each client retries every single connected API call that has failed. This creates more pressure on the server and leaves no room for recovery.

## Exponential Backoff

Exponential Backoff is a retry strategy that introduces a delay between retries, increasing the delay exponentially with each retry attempt.

This approach gives servers a breathing space and allows them time to recover. Instead of repeating the API call back-to-back, we introduce a delay that increases with each retry attempt.

Adding exponential backoff reduces immediate retries but there is still a chance that the retries repeating at the same time will continue to bombard the server concurrently.

## Jitter to the rescue

To further improve this approach, we can add a jitter to the retry intervals. Jitter refers to adding some random delay to the retry interval to avoid retries coinciding.

This approach helps to distribute the retries and prevent them from adding to the problem. By introducing randomness, we can ensure that the retries are distributed across a wider time interval, reducing the chances of coincidences during retries.

### Caveats

When implementing Exponential Backoff and Jitter, there are two key things to keep in mind. First, it is essential to add random jitter to the retry interval to avoid coincidences during retries. Second, ensure that the retries are exponentially spaced, so that the time interval between retries increases with each attempt.

<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Thundering Herd Problem and How not to do API retries](https://i.ytimg.com/vi/8sTuCPh3s0s/mqdefault.jpg)](https://www.youtube.com/watch?v=8sTuCPh3s0s)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

When the network is unreliable the clients retry the APIs to ensure completion. This approach works when there are fewer clients; but what happens when there are millions of them?

They all will keep on bombarding the server with their requests and this problem is called the Thundering Herd problem and in this video, we understand what this problem is, why it occurs, and how to solve it.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1YeEfBgoVpFBVjVJqd2v9sRK3owBLaTpc/view?usp=share_link)
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