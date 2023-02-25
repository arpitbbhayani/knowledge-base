An engineering deep-dive into Atlassian's Mega Outage of April 2022
===


In April 2022, Atlassian suffered a major outage where they "permanently" deleted the data for 400 of their paying cloud customers, and will take them weeks to recover the data. Let's dissect the outage and understand its nuances of it.

Disclaimer: I do not have any insider information and the views are pure speculation.

## Insight 1: Data loss up to 5 minutes

Because some customers reported a data loss of up to 5 minutes before the incident, it shows that the persistent backup incrementally every 5 minutes. The backup typically happens through Change Data Capture which operates right over the database.

## Insight 2: Rolling release of products

Atlassian rolls out features to a subset of the users and then incrementally rolls them to others. This strategy of incremental rollout gives companies and teams a chance to test the waters on a subset and then roll out to the rest.

## Insight 3: Mark vs Permanent Deletion

The script that Atlassian ran to delete had both the options- Mark of Deletion and Permanent deletion.

Mark for deletion: is soft delete i.e. marking is_deleted to true.
Permanent deletion: hard delete i.e. firing DELETE query

Why do companies need permanent deletion? for compliance because GDPR gives users a Right to be Forgotten

## Insight 4: Synchronous Replication

To maintain high availability they have synchronous standby replicas which means that the writes happening needs to succeed on both the databases before it is acknowledged back to the user. This ensures that the data is crash-proof.

## Insight 5: Immutable Backups

The backup is made immutable and stored on S3 in some serialized format. This immutable backup allows Atlassian to recover data at any point in time while being super cost-efficient at the same time.

## Insight 6: Their architecture is not truly a Multi-tenant Architecture

In a true multi-tenant architecture, every customer gets its fragment of infra- right from DB, to brokers, to servers. But at Atlassian, multiple customers share the same infra components. Companies typically do this to cut down on their infrastructure cost.

## Why is it taking a long time to restore?

Because data of multiple customers reside in the same database when the DB was backed up the data (rows and tables) were backed up as is; implying that the backup also had data from multiple customers.

Now to restore the intermingled rows of a customer, the entire backup needs to be loaded into a database and then the rows of specific customers need to be restored. This process is extremely time-consuming.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![An engineering deep-dive into Atlassian's Mega Outage of April 2022](https://i.ytimg.com/vi/xa-hMF8gku0/mqdefault.jpg)](https://www.youtube.com/watch?v=xa-hMF8gku0)

In April 2022, Atlassian suffered a major outage where they "permanently" deleted the data for 400 of their paying cloud customers, and will take them weeks to recover the data. In this video, we will do an engineering deep dive into this outage trying to understand their engineering systems and practices.

We extract 6 key insights into how their engineering systems are built, their backup and restoration strategies, and most importantly why is it taking them so long to recover the data.

Disclaimer: I do not have any insider information about this and the views are pure speculation.

Outline:

00:00 Impact of the outage
03:56 Insight 1: Incremental Backup Strategy
06:38 Why did the Atlassian outage happen?
07:30 Insight 2: Progressive Rollout Strategy
10:57 Insight 3: Soft Deletes vs Hard Deletes
14:28 Insight 4: Synchronous Replication for High Availability
17:47 Insight 5: Immutable backups for point-in-time recovery
21:04 Insight 6: Nearly multi-tenant architecture
23:30 Why is it taking time for Atlassian to recover the deleted data?

Outage Report: https://www.atlassian.com/engineering/april-2022-outage-update

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1Bp4huBCx-wkG6kCQ5raSujdKID4RLU_y/view?usp=sharing)
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