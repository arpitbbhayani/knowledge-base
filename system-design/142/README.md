An in-depth introduction to Blue Green Deployments
===


Blue Green Deployment is a deployment pattern that reduces the downtime during deployment by running two identical production setups called - Blue and Green.

During deployment when we reboot the API servers there are chances that the incoming request fail because the server is unresponsive for a short period. Also, it might happen that the release had a major bug and we need a quick rollback.

How can we achieve both of them in one shot? The answer is Blue Green Deployment.

## Implemention

Blue Green deployment is implemented by having a separate fleet of infrastructure for the old version - Blue and the new version - Green. The new infrastructure is identical to the old one.

The deployment flow

1. the new deployment artifact is tested and kept ready to be deployed
2. a parallel infrastructure is set up identical to the existing
3. the new version is deployed on the new fleet - Green
4. the correctness of the setup is validated
5. the proxy is re-configured to now forward 100% of traffic from the Blue (old) setup to the Green (new) setup
6. a final sanity test is run on the new fleet
7. the blue fleet is now shut down

## Pros of Blue Green Deployment

1. rollbacks are just a config change and hence quick
2. downtime during deployment is minimal
3. deployment is just a flip of a switch
4. disaster recovery is simple given we already have the automation to build a parallel setup
5. deployments can now happen during the working hours
6. debugging a failed deployment is simple as we have the infrastructure with the debug information handy

## Possible challenges

1. during the deployment the infrastructure cost shoots 2x
2. the stateful application would need to rebuild the state on new servers
3. the database would have to be shared between the fleets
4. any schema migration on the database needs to be backward and forward compatible
5. the API responses have to be forward and backward compatible
6. setting up this deployment strategy for the first time is difficult

## When to use Blue Green Deployment?

- when you need zero downtime deployment
- your infrastructure can tolerate 100% traffic switch
- you can bear the 2x cost of infrastructure during deployment

## Points to remember

- have a solid automation test suite to validate the correctness
- ensure forward and backward compatibility of API and schema changes
- infra cost will shoot up hence minimizing the time for which you are running 2x infra
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![An in-depth introduction to Blue Green Deployments](https://i.ytimg.com/vi/W6HANd8c9t4/mqdefault.jpg)](https://www.youtube.com/watch?v=W6HANd8c9t4)

Deployments are a pain if we are unsure about our release changes. But sometimes even if we know our changes well, something weird could happen in the infra that would fail your deployment and put your infra in an inconsistent state.

So, is there a way to address this? What if we have a place to deploy our changes and validate them before they hit production; and have a quick way to roll back if something goes wrong?

This is the core idea behind a Blue-Green Deployment

In this video, we take an in-depth look into a blue-green deployment pattern, understand why we need them, what problem it addresses, learn how they are implemented, talk about its benefits and challenges, and conclude with some points to remember when you adopt this deployment pattern.

Outline:

00:00 Agenda
03:13 An introduction to Blue-Green Deployments
06:36 Why do we need Blue-Green Deployments
09:12 How Blue-Green Deployment is implemented?
13:26 Pros of having a Blue-Green Deployment
19:49 Challenges in having a Blue-Green Deployment
25:36 When to use Blue Green Deployments
26:39 Key points to remember while adopting Blue Green Deployment

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1jSowz0IW8kD4Fjrv2fsE-ygHVTaZto1d/view?usp=sharing)
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