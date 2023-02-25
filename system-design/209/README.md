Designing Uber's highly available Emergency SOS Service
===


The emergency button on the Uber app is life-saving; and the service powering it needs to be available 24 x 7, no matter what!

So, how did Uber design such a service? How did they make it highly available; here's a quick gist about its system design 👇‍

## Information Gathering

When the emergency button is pressed, we first need to gather all the critical information and send it to the server. The critical information could be

- Current Location
- Vehicle and Trip Details
- Rider and Driver Details

## Capturing Location

When the emergency button is pressed, we do not just need to fetch the location at that moment, instead we continuously capture the location and keep sending it to the backend.

This would help us notify the nearby police and help them keep an eye on the movement.

### Lat-long are not enough

To make tracing effective, we cannot just share the lat and long because they are incomprehensible; hence we try to deduce the address from the lat-long.

This process of deducing address from lat-long is called Reverse Geocoding.

## Notifying the police

Uber uses a 3rd party service named RapidSOS to notify nearby local authorities.

RapidSOS provides APIs to register an emergency and send live updates about the emergency. It takes care of notifying the local authorities and providing them with the necessary information.

## Notifying others

Uber not only notifies the police through RapidSOS, but it also notifies

- emergency contacts
- internal support staff for close follow-ups

The notification to all channels happens in parallel to increase the probability of someone getting notified.

## Reliability and Availability

Given that the emergency service deals with events that are urgent, important, and critical; it is extremely crucial that the service is reliable and highly available; which means

- no events loss
- persistence and retries
- fallback to every single component 

## Key Decisions

1. Location getting ingested in Kafka
2. Kafka guarantees persistence and reprocessing if required
3. RapidSOS can be down and hence apply retries on consumers
4. Emergency service notifies emergency and internal staff async
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Designing Uber's highly available Emergency SOS Service](https://i.ytimg.com/vi/gpzGpPiRoCo/mqdefault.jpg)](https://www.youtube.com/watch?v=gpzGpPiRoCo)

An emergency button in a ride-hailing app like Uber can be life-saving but what happens when you click it? What kind of information does it capture? how does it notify the nearest police station?

In this video, we dive deep into the architecture of Uber's emergency SOS service and look at key design decisions that make it so reliable and highly available.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1RMjNyqQoDK0z3OmzhICOg7WHRhAEIMG1/view?usp=share_link)
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