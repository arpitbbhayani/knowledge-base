Pinterest built their own time-series database named Goku because existing databases did not fit their requirements, here is the architecture of it.

## Existing OpenTSDB setup

Pinterest used OpenTSDB to hold their time-series data but it didn't work very well at scale. The two key aspects that hurt them were

- Long GC Pauses
- Frequent process crash

## Challenges

1. OpenTSDB disk-based scans are inefficient
2. The data stored in OpenTSDB does not have a good compression
3. OpenTSDB is JSON based and hence very inefficient
4. OpenTSDB is distributed and for a query that spans multiple shards, it first collects the data in one node and then evaluates the query.

## Key Decisions

1. To make the scan efficient, Goku stores data in-memory
2. Goku uses Gorilla engine which gives 12x compression
3. Goku computes a partial response at each shard and then sends it to the proxy; thus doing a minimal data transfer.
4. Goku uses Thrift Binary protocol, much more efficient than JSON

## Architecture

Goku stores 24 hours' worth of data in-memory with a configured periodic flush to the disk. The most recent query is fired to this in-memory store for quick evaluation.

Goku is a shared time-series database and each shard may contain data from multiple time series. Each Goku instance holds Bucket Map within which the time-series data resides. Each bucket holds data for a 2-hour window.

The writes on each time-series data go to the bucket map, within which it writes to a mutable buffer. Once the window is done, the buffer becomes immutable.

During a query, the request comes to a Goku Proxy which, if required, fans it out to all the involved shards. Each shard does the computation on its share of data and sends the response back to the coordinator/proxy node.

The coordinator/proxy node aggregates the response and sends it back to the client, thus completing the operation.