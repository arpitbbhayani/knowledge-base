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