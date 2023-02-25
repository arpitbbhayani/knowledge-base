How Zomato improved its search by identifying intent through NLP
===


Search is one of the most interesting problems to attempt and Zomato has made their search understand natural language; here's a quick gist about this system 🧵

A simple search engine that just does a weighted search on name and description is easy to game. For example: "Best Coffee Cafe" would rank restaurants having the word "best" in their names higher.

But the actual intent of the user is to get the list of best coffee cafes near its current location.

Handling such queries requires natural language understanding. On Zomato, the search queries can be classified into 3 categories

1. Dish + Dish - chai and samosa
2. Restaurant + Dish - mcd burger
3. Restaurant/Dish + near me/best/some text - pizza near me

## Training the model

We train a Neural Network with domain data that helps us understand the different entities present in the search query; and for this, we leverage

- Word2Vec
- Byte-pair Encoding, and
- LSTMs.

### Word2Vec

Word2Vec helps in generating word embeddings i.e. vector representation of a word such that the weights in the vector mean something as per the corpus.

Documents are tokenized and passed as inputs to Word2Vec. So a restaurant name "Domino's Pizza" should be passed as tokens "Dominos" and "Pizza". But how do we tokenize?

### Byte-pair Encoding

Tokenizing the document on simple spaces won't work well because, in the Food domain, we see some words appear together more frequently than others. Ex: "Cheeze Pizza".

To train Word2Vec better, we would prefer, "Cheeze Pizza" to be considered as one token instead of "Cheese" and "pizza" as two; because in the end, these will be our entities.

This requires us to do a supervised tokenization and we leverage an algorithm called Byte-pair Encoding. It is a really simple supervised algorithm that does a great job at tokenizing the text as per the corpus.

The algorithm just works by merging the most frequent subtokens and creating new amalgamated tokens.

For example, BPE enables us to tokenize "Friedrice" as "Fried" and "Rice" which would not be possible if we just split by space.

### Sequence Tagging

The tokens extracted using Byte-pair Encoding are used as a vocabulary to generate word embeddings which are used to train a Neural Network to understand Named Entities using Bidirectional LSTM.

With this network, we could process the text "Jack's Aaloo Tikki Burger" and get

- Jack's is a Restaurant
- Aaloo Tikki Burger is a Dish

## Architecture

The data about Restaurants, Food, and Locations is ingested to train the model. The model is loaded in a lightweight API server and served through an API Gateway.

The Search service upon getting the search request makes a call to this API that responds with extracted - Dish, Restaurant, and Intent.

The information is then used to formulate an Elasticsearch Query to get the search results. These results are then streamed back to the user and rendered on their applications.
<hr />


<p>Here's the video of me explaining this in-depth 👇‍</p>

[![How Zomato improved its search by identifying intent through NLP](https://i.ytimg.com/vi/JL9x9N6YSUc/mqdefault.jpg)](https://www.youtube.com/watch?v=JL9x9N6YSUc)

Search is one of the most important services, especially for Food Aggregators like Zomato. An interesting challenge comes when the search query is not homogeneous, instead it contains multiple entities.

For example, "Best Dominos Pizza Near Me". This query contains a restaurant, a dish, and a location. Getting relevant information from the search engine from this query is an interesting problem to solve.

In this video, we dive deep into how Zomato identifies the intent of the search query to better its Search Experience and make it more conversational using NLP.

You can also
 - Subscribe to the YT Channel [Asli Engineering](https://youtube.com/c/ArpitBhayani)
 - [Download the notes](https://drive.google.com/file/d/1n688D9Wa6JgwbqmeRuxTAOOyyxAyYZo1/view?usp=share_link)
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