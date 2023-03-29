Introduction to Serverless Computing and Architecture
===


Serverless is a cost-efficient way to host your APIs and it forms the crux of systems like Chatbots and Online Judge.

Serverless does not mean that your code will not run on the server; it means that you do not manage, maintain, access, or scale the server your code is running on.

The traditional way to host APIs is by spinning up a server with some RAM, and CPU. Say the resources make your server handle 1000 RPS, but you are getting 1000 RPS only 1% of the time which means for the other 99% you are overprovisioned.

So, what if there was an Infrastructure that

- scales up and down as per the traffic
- is billed per execution
- is self-managed maintained and fault-tolerant

These requirements gave rise to Serverless Computing.

## Real-world applications

### Chatbot

Say, we build a Slack chatbot that responds with the Holiday list when someone messages `holidays` . The traffic for this utility is going to be insignificant, and keeping a server running the whole time is a waste. This is best modeled on Serverless which is invoked on receiving a message.

### Online Judge

Every submission can be evaluated on a serverless function and results can be updated in a database. Serverless gives you isolation out of the box and keeps the cost to a bare minimum. It would also seamlessly handle the surge in submissions.

### Vending Machine

Upon purchase, the Vending machine would need to update the main database, and the APIs for that could be hosted on Serverless. Given the traffic is low and bursty, Serverless would help us keep the cost down.

### Scheduled DB Backups

Schedule daily DB backups on the Serverless function instead of running a separate crontab server just to trigger the backup.

### Batch and Stream Processing

Use serverless and invoke the function every time a message is pushed on the broker making the system reactive instead of poll-based.

## Advantages

- No need to manage and scale the infra
- The cost is 0 when you do not get any traffic
- Scale is out of the box; so no capacity planning is needed

## Disadvantages

- Takes time to serve the first request as the underlying infra might boot up
- The execution has a max timeout, so your job should complete within the limit
- Debugging is a challenge
- You are locked in on the vendor you chose

## When NOT to use Serverless

- Load, usage, and traffic pattern is consistent
- Execution will go beyond the max timeout
- You need multi-tenancy

## When to use Serverless

- Quick build, prototype, and deploy the changes
- Usecase is lightweight
- Traffic is bursty
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Introduction to Serverless Computing and Architecture](https://i.ytimg.com/vi/oiZH5U_a0pg/mqdefault.jpg)](https://www.youtube.com/watch?v=oiZH5U_a0pg)

Serverless Computing is one of the hottest topics of discussion today, but the term "serverless" is slightly misleading and it does not mean that your code will not need a server to run. We have to be extremely cautious while deciding on adopting serverless for our use case, but it is not something that fits all the use cases.

In this video, we talk about what serverless computing is, see why it was built in the first place, learn about 5 real-world use-cases that become super-efficient with serverless architecture, understand the advantages and more importantly, the disadvantages of adopting it, and conclude with acknowledging when to use and when not to use this computation pattern.

Outline:

00:00 Agenda
03:01 Need and the idea of the Serverless Computing
11:16 Usecase 1: Chatbots
13:57 Usecase 2: Online Judge
16:27 Usecase 3: Vending Machines
18:00 Usecase 4: CRON Jobs
19:54 Usecase 5: Batch and Stream Processing
22:16 Advantages of Serverless Computing and Architecture
26:21 Disadvantages of Serverless Computing and Architecture
31:37 When NOT to use Serverless
34:00 When to use Serverless

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1sZShE0r41XcFa2gEPW1RS_YTaR3tC-zH/view?usp=sharing)
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