Dissecting Google Maps Outage: Bad Rollout and Cascading Failures
===


<p>Google Maps Outage Dissection [ in a gist ]</p>
<p>On the 18th of March, 2022, Google Maps faced a major outage affecting millions of people for a couple of hours. The outage happened due to a bad deployment.</p>
<p>Although a bad deployment does not sound too bad, the situation worsens when there are cascading failures if 3 services have a synchronous dependency, forming a chain-like A -&gt; B -&gt; C.</p>
<p>If A goes down, it will have some impact on B, and if the impact is big enough, we might see B going down as well; and extending it, we might see C going down.</p>
<p>This is exactly what happened in this Google Outage. Some services had a bad deployment, and they started crashing. Tile Rendering service depended on it, and the Tile rendering service went down because of retries.</p>
<p>The Direction SDK, Navigation SDK directly invoked the Tile rendering service for rendering the maps, which didn't work, causing a big outage.</p>
<p>✨ How to remediate a bad deployment?</p>
<p>Rollback as soon as possible.</p>
<p>✨ Preventing cascading outages</p>
<p>- Reject requests when the server is exhausted
 - Tune the performance of the webserver and networking stack of the server
 - Monitor the server resource consumption and set alerts
 - Add circuit breakers wherever possible.</p>
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![Dissecting Google Maps Outage: Bad Rollout and Cascading Failures](https://i.ytimg.com/vi/6oJaZbQKnJE/mqdefault.jpg)](https://www.youtube.com/watch?v=6oJaZbQKnJE)

<p>Google Maps had a global outage on 18th March 2022, during which the end-users were not able to use Directions, Navigation, or Google Maps in general. The outage happened because of a bad rollout, and it lasted more than 2 hours 30 minutes. During the outage, users complained to have seen Gray tiles implying that the map/direction was neither getting initialized nor working.</p>
<p>In this video, we dissect the Google Maps outage and understand what actually happened, how they mitigated it, and, more importantly, understand ways to prevent such an outage and build a robust way of handling cascading failures.</p>
<p>Outline:</p>
<ul>
<li>00:00 Introducing the outage and impact</li>
<li>02:07 Root cause</li>
<li>08:36 Cascading Failures</li>
<li>12:22 Remediation</li>
<li>13:45 Preventive measures</li>
</ul>
<p>Incident Report: https://issuetracker.google.com/issues/225361510</p>

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/10yi5K2xluTA9d7RNrorDDKU_-Mi3uHKZ/view?usp=sharing)
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