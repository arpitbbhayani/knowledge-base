How do indexes make databases read faster?
===


# Gist

How do indexes make databases read faster?
  
The database is just a collection of records. These records are serialized and stored on the disk. The way the records are serialized and stored on the disk depends on the database engine.  
  
✨ How does the database read from the disk?  
A disk is always read in Blocks, and a block is typically 8kb big. When any disk IO happens, even requesting one byte, the entire block is read in memory, and the byte is returned from it.  
  
Say we have a "users" table with 100 rows, with each row being 200B long. If the block size is 600B, we can read 600/200 = 3 rows in one disk read.  
  
To find all users with age = 23, we will have to read the entire table row by row and filter out the relevant documents; we will have to read the entire table. In one shot, we read 3 rows so that it would take 100/3 = 34 disk/block reads to answer the query.  
  
✨ Let's see how indexes make this faster.  
  
An index is a small referential table with two columns: the indexed value and the row ID. So an index on the age column will have two columns age (4 bytes) and row ID (4 bytes).  
  
Each entry in the index is 8 bytes long, and the total size of the index will be 100 * 8 = 800 bytes. When stored on the disk, the index will require 2 disk blocks.  
  
When we want to get users with age == 23, we will first read the entire index, taking 2 disk IOs and filtering out relevant row IDs. Then make disk reads for the relevant rows from the main table. Thus we read 2 blocks to load the index and only relevant blocks having the actual data.  
  
In our example, it comes out to be 2 + 2 = 4 block reads. So, we get an 8x boost in performance using indexes.  
  
Note: This is a very crude example of how fetch happens with indexes; there are a lot of optimizations that I have not talked about.  


In this video, we discuss how indexes make a database operate faster. While discussing that, we dive deep into how the data is read from the disk, how indexes are structured, serialized, and stored on the disk, and finally, how exactly data is quickly read using the right set of indexes.

Outline:

00:00 How is a table stored on the disk?
03:14 Reading bytes from the disk
05:21 Reading the entire table from the disk
08:33 Evaluating a simple query without an index
10:00 Basics of Database Indexes
13:24 Evaluating a simple query with index

[![How do indexes make databases read faster?](https://i.ytimg.com/vi/3G293is403I/mqdefault.jpg)](https://www.youtube.com/watch?v=3G293is403I)


# Notes

The notes used in the video is can be found in the current folder and on [Google Drive](https://drive.google.com/file/d/1wDDOc3rdsZIdZEEe50E_61wi-1iMHu2G/view).


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