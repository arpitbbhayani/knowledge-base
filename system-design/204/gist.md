Elasticsearch is a great search engine, but Yelp was not happy with its performance, so they built their own HTTP layer on top of Lucene. Here's the architecture of it...

## Why not Elasticsearch?

1. ES replication is naive. The operations that happen on the master are re-done on replicas; hence scaling is not cheap.
2. ES suffers from the Hot Node problem and requires manual moving of the shards across nodes to balance the load.
3. ES autoscaling is time-consuming and hence we always provision it for the peak load.

## Key features of Lucene

### Near Realtime Indexes

In Lucene, the data of an index is stored in an immutable structure called Segment. Once the segment is written it can be quickly copied to a replica, in near-real-time. Thus, replication does not require the Replicas to re-index the documents, making it super-efficient to scale out.

### Concurrent Search on Segments

Search in Lucene is parallelized on segments. Hence for a given search query, Lucene can make parallel searches across segments using multiple threads and compute the most relevant results. It helps in leveraging all the cores of the underlying hardware.

Elasticsearch lacks the above features and is expensive in most cases, and hence Yelp thought of writing their own performant HTTP layer on top of Lucene, similar to Elasticsearch; and they call it nrtSearch.

## Implementation Details

### gRPC and Protobuf

Instead of using standard JSON-based endpoints for communication, nrtSearch uses gRPC/protobuf-based endpoints, saving a ton of time spent in serialization and de-serialization of the data.

To support existing systems that understand JSON, nrtSearch also provides a REST server built using gRPC-gateway. This gives clients an option to talk over gRPC or REST.

### Quick Failovers

Failovers are painful with Lucene. A standard flow is to backup the index segments on S3 and when a new node spins up, download the required segments and start serving the request.

To make failover quicker, Yelp used EBS by AWS which is like pluggable storage. The index segments are stored on these EBS volumes.

When a node goes down, and a new node spins up, instead of downloading the segments from S3, the unaffected EBS volume is attached to the new node. This makes the recovery happen in seconds instead of minutes.

### Replication

When the new segments are created on the master node, the master notifies all the replicas about it. The replicas then fetch the newly created segments from the Master over gRPC and maintain an eventual sync.

## Performance Improvements

### Virtual Sharding

Search in Lucene happens over segments, and the worst we can do is spin one thread for searching over each segment. This is sub-optimal and hence, the segments are virtually sharded.

Search Threads are capped and the segments are grouped greedily into slices. One search thread is allotted to each slice, thus searching over multiple segments in one go.

This logical abstraction helps in maintaining consistent utilization of search threads for a given search request.

### Other improvements

1. Fetching document fields in parallel
2. Segment-level search timeout to maintain consistent SLA

## Migration from ES to nrtSearch

### Dark Launch

Instead of directly launching the nrtSearch to the public, it is important to test the correctness of the response on production data. Hence, the first phase of the launch is a Dark launch.

The idea is to serve the entire 100% of requests from Elasticsearch, but send 5% of the requests to the new nrtSearch. The responses of this 5% of the request are compared with the legacy system.

Once the difference is analyzed and confidence is built on the correctness, the percentage is increased to 10, 15, 20, and 50%.

### Phased Rollout

Once there was 100% confidence in nrtSearch, the changes were rolled out to the general users in a phased manner and this time the requests we exclusively bifurcated across Elasticsearch and nrtSearch.

The initial percentage was 5%, eventually increasing it to 100% and then plugging out the legacy Elasticsearch.