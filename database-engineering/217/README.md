Why do databases store data in B+ trees?
===


Relational Databases and some non-relational databases use B+ trees to hold the data but why?

One of the main reasons why SQL databases use B+ trees to hold the data is because of their efficiency in performing operations such as insert, update, find, and delete.

## Limitations of Sequential Files

Before we delve into the details of why SQL databases use B+ trees, let's first understand the limitations of storing data in a sequential file.

When records of a table are stored in one file sequentially, performing operations such as insert, update, and delete becomes complicated, with a complexity of O(n). The linear scan in the middle of the file for insertion or overriding can take up a lot of time and resources, making it inefficient.

## Where B+ Trees thrive

In B+ trees, rows or documents of a table are clubbed in B+ tree nodes, and each node holds a maximum of some `n` rows. For example, if one B+ tree node is 4KB big (same as a disk block size) and the row size is 40B, then each node will hold a maximum of 100 rows. This makes disk reads efficient since reading one node from a disk means reading 100 rows at once.

Non-leaf nodes in a B+ tree hold routing information, while leaf nodes hold the actual rows. The leaf nodes are linked so that linear traversal of the actual rows is possible. The B+ tree structure thus ensures that the table is always logically and physically arranged by its primary key

## CRUD Operations with B+ Trees

### Finding row by ID

Finding a row by ID involves

1. traversing from the root node,
2. reaching the leaf node that holds the row,
3. reading the node and disk blocks in the main memory, and
4. extracting the row from the node and returning

### Inserting a new row

Inserting a new row involves

1. finding the leaf node where the row should be placed
2. reading the node in the main memory
3. inserting the node
4. rebalancing the tree, if needed
5. flushing a leaf node where the value is updated

### Updating a row

Updating a row involves

1. finding the leaf node that holds the row
2. reading the node (disk blocks) in the main memory
3. updating the row in memory, and
4. flushing the blocks to the disk.

### Deleting a row

Deleting a row involves

1. finding the leaf node that holds the row,
2. reading the node (disk blocks) in main memory,
3. removing the row from the node, and
4. flushing the blocks to the disk
5. re-balance the tree, if required

## Range Queries with B+ Trees

Range queries such as finding rows with IDs in the range of 100 to 600 involve finding the leaf node that holds the first row, traversing linearly to reach the row with ID 600, and extracting the data until then.

The B+ tree structure ensures that the time complexity of these operations is O(log n), which is much more efficient than the O(n) complexity of sequential file storage.

## Conclusion

In conclusion, SQL databases use B+ trees to store data efficiently and perform operations such as insert, update, find, and delete with a time complexity of O(log n). This makes managing and storing large volumes of data more manageable and efficient.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Why do databases store data in B+ trees?](https://i.ytimg.com/vi/09E-tVAUqQw/mqdefault.jpg)](https://www.youtube.com/watch?v=09E-tVAUqQw)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

Join this channel to get access to the perks:
https://www.youtube.com/channel/UC_b1GUJv_2QiMP4BxC9-Dxg/join

We all know databases store their data in B+ trees, but why and how?

In this video, we answer this very question and go through the evolution of storage from a naive way to an optimized B+ tree. We will talk about why there was a need to use B+ trees, how table data is stored in B+ trees, and how is this tree serialized and stored on the disk.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1nKf6byk05d_PtHcMNOa9YtbC0-C72RMj/view?usp=share_link)
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