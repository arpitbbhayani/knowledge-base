How Slack efficiently classifies emails at scale with an eventually consistent system
===


One of the features of Slack is the ability to invite people to join a workspace by email. However, not all email addresses belong to the same organization, and it is a challenge to distinguish between internal and external invites.

In this article, we will discuss the technical details of how Slack classifies emails to provide a smoother product onboarding experience.

## Need for classification

Onboarding employees and external vendors into a Slack workspace can be a tedious process. Depending on who is being invited, an internal or an external onboarding flow will be triggered. This can be as simple as showing a different dialogue.

A solution to this problem is an email classification service that classifies every email into an internal, or external category. This service kicks in when a user types in an email address during the invitation process.

## Heuristics

Slack's email classification service attempts to classify emails by using heuristics. For example,

- if the user's domain is one of the allowed ones, then the user is internal
- if the domain of the inviter matches the domain of the invitee, the invitee is classified as per the inviter's class.

###But heuristics fail

The above two approaches are simple and effective for Slack workspaces that are homogeneous (having one or few email domains). But, things become interesting when the number of email domains is many and there is no one rule that will fit.

Slack solves this classification problem by keeping track of all domains part of a workspace and using that aggregated count to determine the class.

## Implementation Details

To implement this classification, Slack maintains a table called `domains` which stores the aggregation (count) per `(team, domain, role)`. This table effectively answers how many users of a workspace have a particular domain and a specific role.

For example workspace, `A` has `68` members having the role `member`, while `6` members with the role `admin`.

The count is maintained with eventual consistency. User-created, updated, and deleted events are sent to Kafka, and consumed by a set of consumers to update the `domains` table.

### Classifying Threshold

Slack operates with a threshold of 10%, which implies that a domain is considered internal if there are at least 10% or more employees in the organization with a given domain, otherwise, it is classified as external.

### Adding a new user

While processing the `user_created` event, Slack does `upsert` instead of an `update` as upserts allow us to not check for the existence of the row with matching constraints.

```
UPSERT count = count + 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "member";
```

### Changing the role

If a user's role changes from `member` to `admin`, the count for the member role is decremented, and the count for the admin role is incremented transactional.

```
UPSERT count = count + 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "admin";

UPSERT count = count - 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "member";
```

### Reprocessing the message

One challenge is that user events can be processed twice causing the numbers to drift. To overcome this challenge, Slack uses a healing mechanism that automatically corrects drifts.

The healer process goes through all the users, until a certain timestamp, and extracts their email domains to perform the count in memory. It then computes the drift from numbers stored in the `domains` table.

Instead of updating the database with the observed count, it pushes the drift as a separate message `+N / -N`. This ensures that numbers in the `domain` table always converge to the correct value and are eventually consistent.

## Conclusion

Slack's email classification service is a critical feature that helps give a smoother invitation experience to users. Classifying emails accurately is a challenging problem, but Slack has implemented an effective solution by using a table to maintain counts and eventual consistency.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Slack efficiently classifies emails at scale with an eventually consistent system](https://i.ytimg.com/vi/BwxU9EnCFXA/mqdefault.jpg)](https://www.youtube.com/watch?v=BwxU9EnCFXA)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Almost all engineers start working on a feature thinking it is a simple and a no-brainer but when we start thinking of the implementation details we realize how complicated things actually are.

In this video, we go deep into Email Classification Service at Slack whose sole job is to classify an email as internal or external. The feature seems a cakewalk but when we start jotting down the implementation specifics, things turn out a little more complicated than what we anticipated.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1Mbz40vZdj5Cet-qFwOBlLQUnSnqfRGGX/view?usp=share_link)
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