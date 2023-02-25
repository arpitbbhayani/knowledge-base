Kademlia - a Distributed Hash Table implementation to power the overlay network of BitTorrent
===


Kademlia is a P2P Distributed Hash Table implementation that distributes the KV stores across nodes in a network and retrieves them without any central authority/database.

## Representation

Every node in the Kademlia network is identified by a unique 20-byte SHA-1 hash. The hash function is also used in reducing the key to be distributed to 20 byte unique id.

## Ownership

The node closest to the key is the one that owns the key and is responsible for holding it. But to define which is the closest one, we need to define a distance metric that could quantify the distance between two entities.

## Requirements from a distance metric

1. distance between the node to itself should be 0
2. distance between two nodes should be a positive number
3. d(a, b) + d(b, c) >= d(a, c)

any function that satisfies the above 3 can be used as a distance function.

## XOR as a Distance Metric

Kademlia uses XOR as a distance metric and defines it as a simple XOR between the ID of the entities

```
d(a, b) = a XOR b
```

XOR can be used as a distance metric because

1. a XOR a = 0
2. a XOR b > 0
3. d(a, b) + d(b, c) = a XOR b XOR b XOR c = a XOR c = d(a, c)

### Visualizing distance

XOR is not a usual distance we can measure, and hence it requires a special way to visualize. XOR tends to turn like bits to 0, so when we XOR two 160 bits numbers, the like bits will turn to 0.

Hence, the more common the prefix between the two 160-bit IDs, the smaller the resultant value, hence the shorter the distance. Thus we can visualize the distance between nodes by placing them in a complete binary tree.

In this complete binary tree, the nodes having shorter distances will be placed closer to each other. Instead of creating a tree with a depth of 160, the tree is constructed only to the point it minimally disambiguates the entity.

## Routing

Because there is no central entity, nodes must know how to route requests among themselves such that they always converge to the right node.

To ensure this, every node in the network keeps track of a few nodes in its routing table. These are not random, but very strategic.

Every node knows at least one node in each subtree that it is not part of. This means that the routing table may not have the address of the desired node, but it can lead us to one of the nodes present in its subtree.

By following a greedy approach, the nodes can route us, step-by-step, to the desired node. This is a classic Overlay network with its own routing.

### Updating routes

When a node receives a message from any other node, it makes an entry in its routing table thus ensuring the table is auto-updated without any explicit intervention.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Kademlia - a Distributed Hash Table implementation to power the overlay network of BitTorrent](https://i.ytimg.com/vi/_kCHOpINA5g/mqdefault.jpg)](https://www.youtube.com/watch?v=_kCHOpINA5g)

Kademlia is a Distributed Hash Table implementation and it is used as an overlay network for BitTorrent. Instead of talking about micro-details and how it is used in BitTorrent, today we spend time understanding Kademlia in depth.

In this video, we take a super detailed look into Distributed Hash Table implementation and we would see how it can power the routing of requests without having any central authority. We look at how data and nodes are represented, how it leverages XOR as a distance function, and how it always converges to the node we are looking for.

Outline:

00:00 Agenda
02:38 Introduction to Kademlia
05:22 Representation
06:36 Ownership
08:04 XOR Distance Metric
12:33 Visualizing XOR Distance
19:38 Routing and k-buckets
31:41 Updating the Routing Table
35:36 Communication Interface
41:52 Performance Optimization

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1eNFBNbcsieL9eVThOVhN9Piu29PI6i7n/view?usp=sharing)
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