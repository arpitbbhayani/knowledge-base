How Flipkart made their type ahead search hyper personalized
===


To help us search quicker and better, Flipkart suggests queries as we type. These suggestions are not only popular suggestions, instead, but they are also hyper-personalized. Let's take a look at how they designed this system.

For a given prefix, say "sh", we should rank the query suggestions - "shoes", "shirts", and "shorts" - in the context of the user.

## Parameters of ranking

1. Quality of the suggestion

- popularity: how popular the search term is?
- performance: does this term has enough results?
- grammar quality: is the term grammatically correct?

2. User-actions

- past few search terms of the user
- past purchase history of the user

## Personalizing the suggestions

A naive way of doing this would be to create cohorts of the users and show all of them the same suggestions for the given prefix. But we wanted to show the suggestions that are relevant as per the recently fired queries.

For example: if a user searched - shoes, red shoes, Nike shoes and then typed "a" - we should be showing "Adidas shoes" and not "apple iPhone".

### Understanding the intent

Flipkart has a taxonomy of the product categories they sell and lists on the platform. The taxonomy holds categories like Fashion and Electronics, and within Fashion, we have Clothing and Footwear, etc.

We first associate the given search query with this taxonomy. If two terms are mapped to close nodes in the taxonomy, they would be contextually relevant and similar.

### Evaluate Category Similarity

We need to determine the probability that the current search term/prefix would belong to the same category as the past search terms.

For example: "computer monitor", "mou" -> "computer mouse"

### Evaluate Reformulation

We need to determine the probability that the current search term/prefix is being written to reformulate the existing context.

For example: "shoes", "red shoes", "n..." -> "Nike Shoes"

## Traning the model

A machine learning model needs to be trained on all viewed items on suggestions, all clicked suggestions, and all unclicked suggestions.

Our model should try to maximize the likelihood of the person clicking the suggestion.

The feature relationships were modeled and ingested in Xgboost ( decision trees ) and the importance of each feature needs to be quantified and evaluated.

## Architecture

There will be an "autosuggestion" service whose job is to serve the suggestions to the user, given the search term.

This service will have a small cache that would hold the data for the most popular search term prefix to serve non-personalized suggestions.

The autosuggestion service will talk to Solr to serve the ML-ranked query suggestions for the given term. The relevance model to be configured in Solr will be "Learning to Rank"

A huge amount of data, through the data pipelines, will be ingested into Solr and the ML model will be explicitly trained on xgboost and ingested through a different component.
<hr />


<p>Here's the video of my explaining this in-depth 👇‍ do check it out</p>

[![How Flipkart made their type ahead search hyper personalized](https://i.ytimg.com/vi/NcNCty7_3kc/mqdefault.jpg)](https://www.youtube.com/watch?v=NcNCty7_3kc)

Search is one of the most used features in any e-commerce and to give a better user experience it is almost customary to provide type-ahead search suggestions.

In this video, we will talk about how Flipkart made their type-ahead search hyper-personalized and dive deep into their high-level architecture and key design decisions that make it extra special.

Outline:

00:00 Agenda
02:28 Introduction and need for type-ahead search
04:23 Parameters of Ranking
07:52 Key design decisions
14:37 High-level Architecture

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1i6w0I8I1H0TxFRoT0Cs0IkcpL6MO6Rbb/view?usp=sharing)
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