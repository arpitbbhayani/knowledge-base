The Architecture of Airbnb's Knowledge Graph
===


Google and Facebook are known to have humungous knowledge graphs; and so does Airbnb. So, what are they? and how are they designed?

Knowledge Graphs are just super-structured information collated from all different data sources. At Airbnb, they power Search, Discovery, and Trip Planner products.

Knowledge Graphs power sophisticated queries like

- find cities that host football matches in July and August and are known for para-gliding
- find a neighborhood in LA where Huts or Private Islands are available in the upcoming summer.

## Key Components

The knowledge graph system has three critical components: Storage, API, and Storage Mutator.

### Graph Storage

Airbnb collates all the structured information and stores it in a relational database having one table to store all the nodes and another table to store all the edges.

Each node in the graph could have a different schema. For example, the location could have a name and GPS coordinates, while the Event would have a title, data, and venue.

Each edge in the graph will hold the types of nodes it can connect to which ensures strong data integrity. For example, an edge "landmark-in-a-city" can connect a landmark and a city.

Airbnb chose to not use GraphDB because of its operational overhead. The team had much higher confidence in relational databases and their capability in managing them.

### Graph API

Query API layer exposes a JSON-based query structure that can be used by clients to interact with the Knowledge Graph.

The JSON query is converted to SQL and fired on the database to get the desired information.

### Storage Mutator

We may think the best way for the Knowledge Graph to remain updated with any changes happening in other systems is to expose an updated API. But that would be too slow and expensive.

Hence, a better way to design this is to ingest bulk updates through Kafka. Updates coming from other systems are put in the Kafka and then the mutator updates the knowledge graph by consuming the events.

## Offline Processing

Not every service wants to synchronously query the graph, for example, the search might want to run an offline ranking job. Querying the graph every time will be inefficient and hence there is a periodic job that exports the entire graph database.

This export is then consumed by the services for offline processing.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![The Architecture of Airbnb's Knowledge Graph](https://i.ytimg.com/vi/7xKgQmqkfD0/mqdefault.jpg)](https://www.youtube.com/watch?v=7xKgQmqkfD0)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

When a product is catering to a large audience, providing contextual information becomes important and at the scale of Airbnb, it becomes non-optional. Hence the engineering team at Airbnb collated all the data and structured it into a Knowledge Graph that today powers its Search, Discovery, and Trip Planner services.

In this video, we take a detailed look into how Airbnb designed its Knowledge Graph, some key components of it, and some key decisions it took while architecting it.

Outline:

00:00 Agenda
02:41 The need for a Knowledge Graph
05:49 Architecture of the Knowledge Graph

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/17Az1C3sESXA0jGPqmcJWjk2GOwSi12Kf/view?usp=sharing)
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