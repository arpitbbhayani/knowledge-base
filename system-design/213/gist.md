Shopify is an e-commerce platform that enables individuals to create their online stores. Shopify uses MySQL database to hold their transactional data and each table has a column called `shop_id` that enables easy identification of rows belonging to a specific shop.

Shopify uses a distributed architecture to handle a large number of shops. A set of shops is grouped in a logical entity called Pod and all of them share the same database. Thus Shopify has multiple pods and each pod has multiple shops sharing the same database.

As the platform grows and more shops sign up, there arises a need to balance the load on different pods by moving the data across databases without downtime.

Let's discuss how they do it in detail.

## Routing Layer

The routing module uses NGINX and is the front-facing entity in the architecture. It routes requests to the pod that is supposed to handle them.

## Distribution of Shops in Shards

Distribution based on the number of shops is not a good idea because two 'heavy shops' may end up on one shard, risking failure due to over-utilization and inconsistent database utilization.

The decision of which shop lives in which shard depends on the 'heuristics' applied by the Shopify data science team. They consider historical database utilization, historical traffic on the shop, and forecasted load.

## Moving Shops Without Downtime

When moving a shop from one pod to another, Shopify ensures that there is no downtime or data loss. Shopify follows three high-level phases to move a shop from one pod to another.

### Phase 1: Batch Copy and Tail Binlog

In the first phase, Shopify uses an internal tool named ghostferry to batch and pick the rows with a particular shop id from multiple tables of the source database and write them to another database present in another pod.

While the batch copy is happening, the newer changes are consumed through `Binlog` and pushed into a queue after filtering out irrelevant events.

### Phase 2: Prepare for Cutover

Once the batch copy is complete, the newer changes are consumed from the queue and applied to the new database until the 'lag' is down to seconds.

When newer events are almost immediately consumed, the writes to the source database are stopped. The source DB's binlog coordinates are recorded, and as soon as the target DB reaches that point, we say replication is done.

### Phase 3: Cutover and Updating the Routing

At this stage, there are no new writes to the source DB, and the source DB is equal to the target DB.

The routing table is then updated and traffic is switched on. The requests for the shop now go to the new pod. After doing a few sanity checks, we mark the shop migration as complete.

## Conclusion

Shopify moves shops from one pod to another to balance shards. Shopify uses an internal tool named ghostferry to move a shop's data from one pod to another. Shopify ensures that there is no downtime or data loss while moving a shop from one pod to another. This article discussed how Shopify balances shards without downtime.