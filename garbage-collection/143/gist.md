Mark and Sweep GC is one of the most common garbage collection algorithms that has seen a massive adoption. The algorithm has two phases:

- Mark Phase: we iterate through the object reference graph and mark all the reachable objects as live; and
- Sweep Phase: we iterate through all the objects in the main memory and delete all the objects that are not marked live; thus cleaning up the garbage

## We need Garbage Collectors to be fast

Garbage collectors need to be fast because we want the CPU cycles to be used in running the core business logic of the user program and not cleaning up unused variables.

## What is a Cache?

A cache is anything that stores the data so that future requests are served faster. The data we can cache can be

- results from the previous computation
- a copy of the data from a slower storage

## When does caching improve performance?

Caching improves the performance of an application only when the use case exhibits one of the following two behaviors

### Temporal Locality

A recently accessed memory location is likely to be accessed again.

By caching the data, we can thus serve the information from the cache instead of doing an expensive lookup or computation.

### Spatial Locality

If a location is recently accessed, the location adjacent to that is likely to be accessed soon.

By caching the data, we can thus serve the information from the cache instead of going through slower storage like disk or main memory.

## Hardware and Cache Prefetching

To leverage caching, modern hardware pre-fetches the data, likely to be accessed, from the slower storage and caches it. This boosts the performance of the application.

There are two ways to pre-fetch:

- hardware intelligently pre-fetches the data as per the access pattern
- hardware exposing "prefetch" instruction leaving to the business logic to prefetch

## Why caching would not improve GC performance?

As we established, for caching to improve the performance our use-case would need to exhibit either spatial or temporal locality. Do mark and sweep exhibit either of them?

### Mark n Sweep and Temporal Locality

Mark and Sweep GC does not exhibit temporal locality given that we mark all the reachable objects in one iteration and in other iteration we go through the unreachables one and free them.

### Mark n Sweep and Spatial Locality

Mark and Sweep GC does not exhibit spatial locality given we we do a DFS on object reference tree which hopes from one object too another in random order. So pre-fetching of memory locations would not help.