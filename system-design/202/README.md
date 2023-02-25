How Dropbox efficiently serves and renders a large number of thumbnails
===


Dropbox has to render a lot of thumbnails when we browse a folder containing a bunch of images. Here's how they serve them efficiently at scale.

## Simple approach

Thumbnail is created for each image present in a Dropbox folder and uploaded to a blob store like s3 or hdfs. Each thumbnail thus has a path using which it can be fetched on the client and shown to the end user.

A simple approach to serve thumbnails is to send thumbnail URLs in an API response to the client and as the user scrolls through them, we keep fetching the images and render them.

This sounds good in theory but gives a very sluggish experience in practice; because of the browser limitation. Every browser caps the maximum number of concurrent connections it can make to a domain.

This limit is 6 for chrome and 8 for firefox, which means at max the browser will be able to fetch 6 images at a time (at best). When there are many photos to render, the experience becomes sluggish as the user will need to scroll and wait for the photos to load.

## Dropbox's Solution

> Note: This is HTTP/1.1 based solution; you can do a lot more if you are using HTTP/2

### Batching Requests

Expose an endpoint (GET) that accepts multiple thumbnail paths as query parameters. 

```
GET https://photos.dropbox.com/tbatch?paths=1.png,2.png
```

The server upon receiving this request goes to the blob store and grabs the thumbnails. It then converts the thumbnails in Base64 and puts them in a text response.

The server then sends this response, containing base64 encoded image data of multiple images, back to the client. The client then identifies the image and its base64 data and renders it.

### Chunked Transfer Encoding

The server need not wait to get image data of all the requested images before it can send the response; instead, it uses chunked transfer encoding to stream a partial response to the client.

The server gets the request and it initiates the fetching of thumbnails in parallel. As and when it receives image data, it creates a chunked response and sends it to the client.

A chunked response is a text file that looks like this

```
0: data:image/jpeg;base64, <image data>
2: data:image/jpeg;base64, <image data>
11: data:image/png;base64, <image data>
```

Once it has completed sending the response for all the images, it sends the terminating response informing the client that the entire response is sent, and closes the connection.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Dropbox efficiently serves and renders a large number of thumbnails](https://i.ytimg.com/vi/FczWm6kx0Kg/mqdefault.jpg)](https://www.youtube.com/watch?v=FczWm6kx0Kg)

A classic challenge that comes while building Instagram or Google Photos is about quickly and efficiently serving and rendering a large number of thumbnails.

In this video, we take a look at an ultimate hack that Dropbox used to very efficiently serve a large number of preview thumbnails by streaming the response from the servers using Chunked Transfer Encoding.

Outline:

00:00 Agenda
02:28 Design of the Photos App
04:39 Why is this even a problem?
07:11 Drobox's Solution: Batching
11:00 Chunked Transfer Encoding

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1l8gl197gxPaCh0mama3LjtiRxNaWgt3v/view?usp=sharing)
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