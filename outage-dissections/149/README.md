Dissecting GitHub Outage - Repository Creation Failed
===


Just imagine you trying to create a repository on GitHub and it is not working, and this happened to GitHub in April 2021 when their users were not able to create a new repository.

The root cause for this outage was something that seems unrelated - Scanning Secrets. The root cause makes this outage super interesting to dissect.

## What is Secret Scanning?

Our API servers need to talk to peripheral components like Databases, Cache, SaaS services, etc. This communication involves some sort of authentication and authorization through auth tokens, passwords, or secret keys.

Developers tend to commit the secrets in the settings/constant files and push them to GitHub. What if the repository content gets leaked? What if GitHub itself has a data breach and the attacker gets access to the private repositories?

If the secrets like AWS access keys, auth tokens, and DB passwords are leaked and the attacker can then get the dump of the data and ask for a ransom. Or they may even abuse the infrastructure to perform some illegal activities or mine cryptocurrencies.

Hence, GitHub periodically runs a job that checks all the repositories for any secrets that are committed and warns the user about it.

## Repository Creation Flow

When a repository is created an entry is made into the Secret Scanning table which is then used by a job that scans for potential secrets and notifies the owner.

## What led to the outage?

The GitHub team ran a data migration in which they moved the Secret Scanning table from a common database to its own cluster allowing it to scale independently.

GitHub team was unaware of this dependency! and hence after the migration of the table happened to a different database the creation of a new repository started failing to lead to this outage. It is interesting to see such mature products having blindspots.

## How did GitHub mitigate it?

The mitigation strategy of GitHub was to roll back the migration. Although it is unclear from the incident report on what exactly they did but there are a few speculations

1. they could have recopied the table quickly to the old database
2. whitelisted the database so that applications could connect
3. old table would have been intact and hence they would have just renamed and made it active again.

Again, it is pure speculation given we do not have any insider information nor they specified in the report. It would have been fun to have gone through their actual mitigation steps. We could have learned so much, but nonetheless, we did learn a few interesting insights from this outage.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Dissecting GitHub Outage - Repository Creation Failed](https://i.ytimg.com/vi/48YZzGi7QMk/mqdefault.jpg)](https://www.youtube.com/watch?v=48YZzGi7QMk)

Imagine you trying to create a new GitHub repository and it call is failing, failing for 53 minutes. This happened with GitHub in April 2021 when for 53 minutes people were unable to create any new repositories. Upon investigation, they found out that the root was scanning secrets. Two seemingly different usecases took down one of the most important APIs.

This has to be one of the most amusing outages that I have seen in recent times.  In this video, we dissect this outage, understand the root cause of it, look at the importance of secret scanning, and conclude with an understanding of their mitigation process.

Outline:

00:00 Agenda
02:49 What happened?
03:20 Secret scanning and its importance
08:28 Repository Creation Flow
09:15 What lead to an outage?
17:26 Outage mitigation

Check out the free course covering all GitHub outages →  https://courses.arpitbhayani.me/github-outage-dissections/

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1KtNWAH5YHC9-qVxvbxLTXF3u5yGV7l-t/view?usp=sharing)
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