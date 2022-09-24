How Swiggy designed and scaled its chatbot
===


Swiggy has automated its customer support with Chatbots; so what's their architecture? Let's find out today.

Chatbots are essentially a Decision Tree where nodes are the states the conversation could be in and the edges are conditional statements. Depending on which statement (edge) meets the criteria, the conversation moves forward in that direction.

At each step, Swiggy shows the customer the options which are the child nodes of the current node until all the information is gathered; and the flow stops upon reaching the terminal state.

## Key components and architecture

The decision tree is stored in a relational database. It can be generated using historical customer support data and can be updated by product and business teams.

The core chatbot service needs to access data from other services/databases like Payments, Orders, and Notifications. Accessing peripheral information will provide a rich experience to the users.

The most important part chatbot is to interact with the Fraud Detection system. Given that the entire flow is automated and needs no manual intervention, the chances of Fraud shoot up.

Fraud Detection System, in real-time, would see if the customer is trying to commit fraud. This system would interact with historical information about the customer, past refunds, image processing, and much more.

There may be a possibility that the customer still needs to talk to an executive hence the customer support executive needs to get all of this information, including fraud probability, in an easy-to-use dashboard.

Hence, a real-time pipeline would be needed to ingest and move data across all of these systems. Apache Spark is an excellent candidate for building this.

## Business Continuity Plan

If the Chatbot is down, then Swiggy switches to a simple chat interface that connects directly to an executive, continuing to service the end users.

## Key Metric

A metric that Swiggy chases is Bot Efficacy which is nothing but the percentage of requests handled by the bot vs executive. Swiggy wants to handle as many requests as possible through the bots as it would help them remain efficient at scale.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How Swiggy designed and scaled its chatbot](https://i.ytimg.com/vi/W8LDyEOPaPY/mqdefault.jpg)](https://www.youtube.com/watch?v=W8LDyEOPaPY)

We all love food but are lazy to go to a restaurant and pick it ourselves and this gave rise to Food Delivery Startups like Swiggy and Zomato. Chatbots are essential for them as they resolve most of the complaints that customers have without spending a lot of money on customer service representatives.

In this video, we take a look at how Swiggy designed their chatbots to achieve business efficiency at scale; and dive deep into their tech architecture and key components that we need to consider while designing it.

Outline:

00:00 Agenda
02:36 What are Chatbots
03:30 Designing Chatbots
07:00 Architecture of a chatbot

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1_C7mUXohjvTR1OAfYL0UWov7-w9B_8zJ/view?usp=sharing)
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