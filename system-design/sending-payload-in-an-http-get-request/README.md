Sending payload in an HTTP GET request
===


Can we send the payload in an HTTP GET request?

It is a common myth that we could not pass the request body in the HTTP GET request. HTTP 1.1 specification neither enforces nor suggests this behavior.

This means it is up to implementing the application web servers - Flask, uWSGI, etc. - to see if it parses the request body in the HTTP GET request. To do this, just check the request object you would be getting in your favorite framework.

⚡ What can we do with this information?

Say you are modeling an analytics service like Google Analytics in which you are exposing an endpoint that returns you the data point depending on the requirements. The requirements specified here could be a large, complex JSON.

Passing this query in the URL of the GET request as a query param is not convenient as it would require you to serialize and escape the JSON string before passing.

This is a perfect use case where the complex JSON query can be passed as a request body in the HTTP GET request, giving a good user experience.

⚡ So, does any popular tool uses this convention?

Yes. ElasticSearch - one of the most popular search utilities, uses this convention.

The search endpoint of ElasticSearch is a GET endpoint where the complex search queries in JSON format are sent in the request payload.


Can we send data in an HTTP GET request? Most people think, No. The truth is, we can send the data in the request payload of an HTTP GET request so long as our webserver can understand it.

In this video, we go through the HTTP 1.1 specification and see what it says about the GET requests, write a simple Flask application to see that we can indeed process the payload of a GET request if we want to, and, more importantly, go through a real-world example where it was essential to send data in the request payload.

Outline:

 - 00:00 HTTP GET Request
 - 01:53 What does HTTP 1.1 specification say?
 - 05:38 Request payload in Python Flask
 - 07:18 ElasticSearch using request payload for search
 - 10:40 When to use HTTP request payload in a GET request

Watch the video 👇‍

[![Sending payload in an HTTP GET request](https://i.ytimg.com/vi/8S4k7k_f9Sk/mqdefault.jpg)](https://www.youtube.com/watch?v=8S4k7k_f9Sk)

If you find this amusing, do like the video and subscribe to my [YT channel](asliengineering.com). I post 3 in-depth engineering videos every week around System Design, Distributed Systems, Microservices, and all things tech.


## Notes

The notes used in the video is can be found in the current folder and on [Google Drive](https://drive.google.com/file/d/1JwVEh9EG0ZGts-VePXNlIE1e8kivdHbM/view).


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