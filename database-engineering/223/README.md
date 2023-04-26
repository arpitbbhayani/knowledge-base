Datetime vs Timestamp datatype in databases - Which one is better and when?
===


Most databases provide three types of temporal data types to store dates and times: `DATE`, `DATETIME`, and `TIMESTAMP`. While all three data types store date and time information, there are significant differences among them, which we will explore in this article.

The exploration of these types is MySQL-specific, but other databases closely follow the semantics. Do refer to the documentation of the database you are using to get an accurate picture.

## Range of values

The `DATE` data type stores only the date information, excluding the time information, and it can store dates ranging from `1000-01-01` to `9999-12-31`.

The `DATETIME` data type stores both date and time information, and it can store dates ranging from `1000-01-01 00:00:00` to `9999-12-31 23:59:59`. On the other hand, the `TIMESTAMP` data type also stores date and time information, but it is limited to a range from `1970-01-01 00:00:01 UTC` to `2038-01-19 03:14:07 UTC`, holding the number of seconds/microseconds elapsed since UNIX Epoch.

## Storage Requirements

DATETIME takes up 5 bytes to store date and time, but depending on how precise you want seconds to be, it stores it in additional 3 bytes to hold up seconds precise up to 6 decimal places.

- 0 precision requires 0 bytes
- 1,2 digit second precision requires 1 byte
- 3,4 digit second precision requires 2 bytes
- 5,6 digit second precision requires 3 bytes

In contrast, the `TIMESTAMP` data type supports fractional seconds up to six decimal places, with a fixed size of 4 bytes plus the fractional seconds represented in up to 3 bytes as described above.

## Which one should you use?

### `DATETIME`

The DATETIME data type is useful when you need to store an application-specific static timestamp, such as appointment schedules or event schedules.

Most databases have in-built functions to operate on `DATETIME` data, so if your usecase requires datetime operations, like `ADD`, `SUB`, `DIFF`, etc., then prefer going for `DATETIME`.

### `TIMESTAMP`

The `TIMESTAMP` data type is ideal for recording timestamps related to events that happen on your system, such as transaction times, which require efficient storage but no specific timezone specific operation.

`TIMESTAMP` is 1 byte lighter than datetime, making it faster to process. In addition, `TIMESTAMP` also have an extra advantage when it comes to time zone handling, as MySQL, or any database, automatically converts timestamps to the UTC timezone and converts them back to the client's time zone on retrieval, whereas `DATETIME` data type does not support automatic timezone conversion unless specified.

## Conclusion

In conclusion, while both the `DATETIME` and `TIMESTAMP` data types store date and time information, they differ in their range, precision, storage requirements, and use cases.

It's essential to consider these differences when choosing which data type to use in your MySQL database to ensure the accuracy and efficiency of your temporal data storage.

<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Datetime vs Timestamp datatype in databases - Which one is better and when?](https://i.ytimg.com/vi/zrl_odkY5tI/mqdefault.jpg)](https://www.youtube.com/watch?v=zrl_odkY5tI)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Datetime and Timestamps are the two most common ways to store data time in any database, but which one should we use and when? In this video, we answer this question, understand some of its internals, and cover the pointers that make it easy for us to decide.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1C_0_RVztiRfRkE8WXwFzYbdGjX2MLkaV/view?usp=share_link)
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