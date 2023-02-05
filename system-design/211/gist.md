Managing massive, talking hundreds of terabytes here, Search clusters is no joke, especially at @Twitter's scale.

To manage them efficiently, Twitter built a bunch of toolings, here's a quick gist about it 🧵👇

Twitter uses ES to power the search of tweets, users, and DMs. ES gives them the necessary speed, performance, and horizontal scalability.

Given massive adoption, they needed to ensure the efficiency, and stability of these clusters and provide some standardized way of access.

## Elasticsearch Proxy

The Twitter team built a simple proxy for Elasticsearch that transparently sits in front of the Elasticsearch cluster.

The proxy is an extremely simple and lightweight TCP and HTTP-based relay that...

in a standard way, captures all critical metrics like - cluster health, latency, success, and failure rates here; along with this we can also

- throttle when some client abuses
- apply security practices
- route to a specific node
- authenticate

## Ingestion Service

ES performance degrades when there is a massive surge in traffic. We typically see an

- increased indexing latencies
- increased query latencies

But it is a common usecase for Twitter to ingest massive data (tweets) every now and then, hence they tweaked the ingestion...

The write requests that come to the ES proxy are sent to Kafka. Consumers read from Kafka and relay them to the ES cluster.

Doing it asynchronously allows us to

- do batch writes
- and retry if the ES down
- consume at a comfortable pace
- slow down if ES is overwhelmed

## Backfill Service

Twitter has a constant need of ingesting 100s of TBs of data in the Elasticsearch clusters.

Doing massive ingestion through Map Reduce jobs directly on ES will take down the entire cluster and doing it through Kafka makes it unnecessarily granular;

hence a backfill service ...

The backfill indexing requests are dumped on an HDFS.

The requests are partitioned and read using distributed jobs and indexed in Elasticsearch.

A separate orchestrator computes the number of workers required to consume the indexing requests.