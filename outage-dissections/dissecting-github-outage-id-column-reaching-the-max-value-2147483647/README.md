Dissecting GitHub Outage: ID column reaching the max value 2147483647
===


# Gist

What happens when MySQL auto-incrementing ID hits its limit?

On the 5th of May, 2020, GitHub experienced an outage because of this very reason. One of their shared table having an auto-incrementing ID column hits its max limit. Let's see what could have been done in such a situation.

✨ What's the next value after MAX int?

GitHub used 4 bytes signed integer as their ID column, which means the value can go from -2147483648 to 2147483647. So, now when the ID column hits 2147483647 and tries to get the next value, it gets the same value again, i.e., 2147483647.

For MySQL, 2147483647 + 1 = 2147483647

So, when it tries to insert the row with ID 2147483647, it gets the Duplicate Key Error given that a row already exists with the same ID.

✨ How to mitigate the issue?

A situation like this is extremely critical given that the database is not allowing us to insert any row in the table. This typically results in a major downtime of a few hours, and it depends on the amount of data in the table. There are a couple of ways to mitigate the issue.

✨ Approach 1: Alter the table and increase the width of the column

Quickly fire the ALTER table and change the data type of the ID column to UNSIGNED INT or BIGINT. Depending on the data size, an ALTER query like this will take a few hours to a few days to execute. Hence this approach is suitable only when the table size is small.

✨ Approach 2: Swap the table

The idea here is to create an empty table with the same schema but a larger ID range that starts from 2147483648. Then rename this new table to the old one and start accepting writes. Then slowly migrate the data from the old table to this new one. This approach can be used when you can live without the data for a few days.

✨ Get warned before the storm

Although mitigation is great, it is better to place a monitoring system that raises an alert when the ID reaches 70% of its range. So, write a simple DB monitoring service that periodically checks this by firing a query on the database.


GitHub experience an outage on 5th May 2020 on a few of their internal services and it happened because a table had an auto-incrementing integer ID and the column reached its maximum value possible 2147483647. In this video, we dissect what happened, mimic the situation locally and see what could have happened, and look at possible ways to mitigate and prevent a situation like this.

Outline:

 - 00:00 Outage walkthrough
 - 02:48 Mimicking the situation locally
 - 10:13 MySQL AUTO_INCREMENT behavior
 - 12:37 Preventive measures
 - 14:25 Approach 1 for mitigating the issue
 - 18:40 Approach 2 for mitigating the issue

References:
 - https://github.com/arpitbbhayani/mysql-maxint
 - https://github.blog/2020-07-08-introducing-the-github-availability-report/
 - https://dev.mysql.com/doc/refman/8.0/en/integer-types.html
 - https://dev.mysql.com/doc/refman/8.0/en/example-auto-increment.html
 - https://www.linkedin.com/pulse/so-you-hit-2147483647-heath-dutton-/

[![Dissecting GitHub Outage: ID column reaching the max value 2147483647](https://i.ytimg.com/vi/ZFRAFTn0cQ0/mqdefault.jpg)](https://www.youtube.com/watch?v=ZFRAFTn0cQ0)


# Notes

The notes used in the video is can be found in the current folder and on [Google Drive](https://drive.google.com/file/d/13rNEWXwIdNkNcP2gSQQvBF8czUBpF47y/view).


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