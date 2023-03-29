Everything you need to know about REST
===


Is REST all about just exposing an HTTP endpoint?

REST is an abbreviation that stands for Representational State Transfer. A lot of complex words but stick with me.

REST is a specification that suggests how a client should demand/request information from the server and how the server should respond; it does not enforce anything.

## Everything is a Resource

In REST, everything is a resource. Any actionable entity in your application eg: book, student, customer, or order is a resource for REST. The client can demand action on a resource like get, create, delete, or update.

REST does not put any restriction on how the data is stored in your application, but it allows clients to specify how it wants the data from the server eg: XML, JSON, CSV, etc. So long as the server supports the representation the server would respond in the demanded format.

## Underlying Protocol for REST

REST does not enforce any restriction on the underlying protocol to be used. All it cares about is that we have a defined way to act on a resource. So, we can implement REST over HTTP or even hardware like USB.

## Why REST over HTTP?

The most common implementation of REST is over HTTP and it gels very well together. Why so?

HTTP has verbs like GET, POST, DELETE, and PUT and these become actions on our resource. The resource is specified by the URL of the HTTP request. For example, to get a student's details whose `id = 1` we fire

```
GET /students/1
```

We are representing the student with `id = 1` using the URL `/students/1` and are specifying action `GET` using the HTTP verb `GET`. Similarly to update the student with `id = 1` we could

```
POST /students/1
```

Here we see how REST is resource-oriented and we have a way to specify the action to be taken on it.

### Existing tooling

One very important reason why HTTP is so commonly used in implementation is the availability of existing tooling. We can reuse the existing set of tools to get the job done, which includes.

- using existing HTTP Clients like Postman, cURL, Requests
- use caches like Ngnix, HA Proxy, and Varnish to boost performance
- use monitoring tools like Distributed Tracing
- use load balancers to uniformly distribute the load
- use SSL to get out-of-the-box security

## Downsides of doing REST over HTTP

- all clients would have to serialize and deserialize the HTTP body
- all clients would have to repetitively handle failures and retries
- some web servers might not support verbs like PUT, DELETE
- HTTP payloads are JSON and hence huge
- HTTP would not support switching underlying protocols
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![Everything you need to know about REST](https://i.ytimg.com/vi/uFGJVQvR59A/mqdefault.jpg)](https://www.youtube.com/watch?v=uFGJVQvR59A)

System Design for Experienced Engineers: https://arpitbhayani.me/masterclass
Become a member for exclusive in-depth videos: https://www.youtube.com/c/ArpitBhayani/join
Redis Internals: https://arpitbhayani.me/redis

REST is how browsers talk to our servers. 99.99% of all your API requests that originates from your browser and go to your API servers are REST. So, what is REST? How is it different from HTTP? Is it a protocol or what? There are so many unanswered questions like this.

In this video, we in-depth talk about REST, understand the foundations of it, see how and why it gels so well with HTTP, find out why everyone is using it, and conclude by going through the downsides of using REST over HTTP.

Outline:

00:00 Agenda
02:38 Introduction to REST
03:14 Everything is a Resource
07:20 Representation in REST
09:07 Underlying protocol in REST
09:20 REST and HTTP
17:32 Downsides of using REST over HTTP

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/18edhW0hhSUp-7Vn3-Mz8Xfge8xRBmJ6W/view?usp=sharing)
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