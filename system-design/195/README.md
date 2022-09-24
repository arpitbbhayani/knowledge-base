How Instagram efficiently serves HashTags ordered by count
===


Instagram has millions of photos, and each has tens of hashtags, so how does Instagram efficiently serves hashtags for a search query?

Instagram uses Postgres as its primary transactions database. For each hashtag, it stores the `media_count` in a table. This allows us to render the Hashtag and some meta information on the search page.

Note: Instagram could also use a dedicated search engine for this usecase, but this usecase is trivial to use something as sophisticated as ElasticSearch. We take a look at how they do it with Postgres.

A naive query to get hashtags for a given prefix ordered by count would look something like this

```
SELECT * from hashtags
WHERE name LIKE 'snow%'
ORDER BY media_count
DESC LIMIT 10;
```

Executing this query would require the database engine to filter out the hashtags starting with `snow` and then sort. Sorting is an expensive operation and this query required the engine to sort 15000 rows.

Under high load, this sorting becomes a pain. So, what's the way out?

The key insight here is the fact that hashtags have a long-tail distribution i.e. most hashtags will have far fewer media counts and while serving we are always ordering by `media_count`.

Hence, instead of indexing everything, we can simply index the hashtags having `media_count > 100` because other hashtags are highly unlikely to be surfaced.

## Partial Indexes

Postgres database has this exact same capability and it is called Partial Indexing. With partial indexes, we can keep only a subset of data in the index.

We can create a partial index on our hashtags table like

```
CREATE INDEX CONCURRENTLY ON hashtags WHERE media_count > 100;
```

With this index, the query we fire would have to scan a very limited number of index entries to spit out the result.

The SQL query to get hashtags with the prefix `snow%` would look something like this

```
SELECT * from hashtags
WHERE name LIKE 'snow%'
AND media_count > 100
ORDER BY media_count
DESC LIMIT 10;
```

The above query required it to sort only 169 rows, completing its evaluation superfast. This is a classic usecase where we all can utilize Partial Indexes.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How Instagram efficiently serves HashTags ordered by count](https://i.ytimg.com/vi/CA2_0ZhVW2g/mqdefault.jpg)](https://www.youtube.com/watch?v=CA2_0ZhVW2g)

Instagram has millions of HashTags and millions of people tag their photos every single day. To discover, Instagram allows us to search for a Hash Tag.

In this video, we will take a detailed look into how Instagram efficiently searches for HashTags and serves them ordered by count; while doing so we will dive deep into a super-interesting Database optimization called Partial Indexes.

Outline:

00:00 Agenda
02:27 HashTag Ordering Problem and Instagram Database
05:41 Naive Query
07:17 Optimized Solution with Partial Indexes

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1C0uGvqYFcBCvqDfkDyJr1RJnTDOq2c6T/view?usp=sharing)
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