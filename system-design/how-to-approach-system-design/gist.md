System Design is tricky but it does not have to be difficult - be it a technical discussion at your workplace or your next big interview. Let's talk about how to approach System Design. Something I compiled from 10 years of my career.

## What is System Design?
System Design is all about translating and solving customer needs and business requirements into something tangible. The output system could be an application, a microservice, a library, or even hardware.

There are a couple of approaches that we can use to design any system out there. Picking one over the other depends on the company you work for and the flexibility it provides.

## The Spiral Approach

The Spiral Approach pans like a spiral in which you start with some core that you are comfortable with (database, communication protocol, queue. etc) and build your system around it. Every single component you add to the design is something that you are pretty confident about and can proceed with the added complexities.

For example:
 - start with the database
 - then add LB and more servers
 - then add a queue for async processing
 - then other services
 - then add synchronous HTTP based communication between them

## The Incremental MVP Approach

In the Incremental MVP-based approach we with a Day 0 design and then see how each component behaves at scale by dry-running it; after identifying the bottlenecks you fix them and re-iterate. You stop the iteration once you are happy with the final product. This kind of approach is typically seen in startups where they do not want to invest in architecture and quickly roll out features.

For example:
 - start with Day 0 architecture of users, API servers, and DB
 - then you add LB and more API servers
 - then you add Read Replica on DB to support more reads
 - then you split the service into a couple of microservices
 - then you partition the DB to handle more scale

## 3 key pointers while designing systems

 - Every system is infinitely buildable, hence fence it well
 - Seek clarifications from your seniors
 - Ask critical questions that challenge the design decisions