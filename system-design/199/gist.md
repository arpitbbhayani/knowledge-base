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