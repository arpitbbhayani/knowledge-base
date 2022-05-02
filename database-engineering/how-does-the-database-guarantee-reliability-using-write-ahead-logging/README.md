How does the database guarantee reliability using write-ahead logging?
===


Any persistent database needs to guarantee the reliability, implying that any update/delete fired on the database is reliably stored on the disk. The alterations on the data should not be affected by power loss, OS failure, or hardware failure.

The changes to the data once committed should do to non-volatile storage like Disk making them outlive any outage or crash. Although the flows seem simple enough to say that- hey let's just flush the changes to the disk; it is a little more complicated than that.

## Disk writes are complicated

When we perform the disk write, the changes are not directly written to the disk sectors, instead, it goes through a variety of buffers like RAM, OS Cache, Disk Cache, and then finally to the Disk sectors. So, if the changes are in any of these intermediate caches and the process crashes, our changes are lost.

So, while guaranteeing reliability we have to skip all of these caches and flush our changes as quickly as possible on the disk sectors. But if we do that, we are impacting the throughput of the system given how expensive disk writes are.

# Write-ahead Logging

Write-ahead logging is a standard way to ensure data integrity and reliability. Any changes made on the database are first logged in an append-only file called write-ahead Log or Commit Log. Then the actual blocks having the data (row, document) on the disk are updated.

If we update any row or a document of a database, updating the data on disk is a much slower process because it would require on-disk data structures to rebalance, indexes to be updated, and so much more. So, if we skip the OS cache, and other buffers, and directly update the rows to the disk every time; it will hamper the overall throughput and performance of the database.

Hence, instead of synchronously flushing the row updates to the disk, we synchronously just flush the operation (PUT, DEL) in a write-ahead log file leading to just one extra disk write. The step will guarantee reliability and durability as although we do not have the row changes not flushed but at least the operation is flushed. This way if we need to replay the changes, in case of a crash, we can simply iterate through this simple file of operations and recover the database.

Once the operation is logged, the database can do its routine work and make the changes to the actual row or document data through the OS cache and other buffers. This way we guarantee reliability and durability in as minimal of a time as possible while not affecting the throughput much.

## Advantages of using WAL

The advantages of using WAL are

- we can skip flushing the data to the disk on every update
- significantly reduce the number of disk writes
- we can recover the data in case of a data loss
- we can have point-in-time snapshots

## Data integrity in WAL

WAL also needs to ensure that any operation flushed in the log is not corrupted and hence it maintains its integrity using a CRC-32 and flushes it on the disk with every entry. This CRC is checked during reading the entry from the disk, if it does not match the DB throws an error.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How does the database guarantee reliability using write-ahead logging?](https://i.ytimg.com/vi/wI4hKwl1Cn4/mqdefault.jpg)](https://www.youtube.com/watch?v=wI4hKwl1Cn4)

Any persistent database needs to guarantee reliability. No matter how big or small the changes are, they should survive any reboots, OS, or hardware crashes once they are committed. All the persistent databases use a write-ahead logging technique to guarantee such reliability while not affecting the performance.

In this video, we talk about write-ahead logging, how it ensures reliability, a few solid advantages of using it, one of them being a massive database performance boost, and how the log files are structured on the disk.

Outline:
00:00 What happens on Commit
05:57 Write-ahead Logging
08:44 Advantages of having a Write-ahead Logging
14:29 Data Integrity in WAL files
16:40 Write-ahead Logging Internals

Related Videos:
How indexes make a database read faster: https://www.youtube.com/watch?v=3G293is403I

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1VC77CEEYLvlFaXpKsb3Q_e0JvbbryyU0/view?usp=sharing)
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