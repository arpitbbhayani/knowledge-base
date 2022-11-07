Building a central, robust, extensible and highly available authorization service is no joke

and @Airbnb does it beautifully

here's a thread about its architecture and key design decisions... 🧵👇

## What is authorization?

It is all about managing fine-grained control over different entities, example:

- can user A edit comment C?
- can user B access hotels in region R?
- can user C read a file in folder F shared with group G?

why do we need a service for this?

## Why a central service?

If each microservice handles its own authorization, then there would be

- duplication of auth logic
- inter-service calls to check for auth

hence, it is beneficial to create a central auth service. Let's see how it is modeled.

## Auth model

- Principal: user or service that needs to be tested
- Entity: on which we are checking the access
- Relation: between entity and principal

can user A edit comment C?

A - is the principal,
C - is the entity, and
edit - is the relation

The tuple is represented and (optionally stored) in the database as

```
<entity> # <relation> @ <principal>
```

if user A has owner privileges on comment C, it will be represented (and optionally stored) as

```
C # OWNER @ A
```

Storing one entry for each entity and relation will make the data explode, For example:

if A owns a comment C, then he/she can read and write to it as well. This would make us have 3 entries in the database

- `C # READ @ A`
- `C # WRITE @ A`
- `C # OWNER @ A`

hence...

we need a way to define relations between relations and entities to reduce the size of the data.

A simple YAML-based config would look like this

```
LISTING:

  # WRITE:
    union:
      - # WRITE
      - # OWNER

  # READ:
    union:
      - # READ
      - # WRITE
```

The above configuration imples,

1. WRITE relation is a union of WRITE and OWNER
2. READ relation is a union of READ and WRITE

Anyone with the write and owner relation can write and anyone with read and write (and transitively owner) relations can read the listing on Airbnb.

To check if user A can read listing L, we hit

```
check (listing:L, READ, user:A)
```

It evaluates as

- LISTING:L # READ @ user:A
- LISTING:L # WRITE @ user:A
- LISTING:L # OWNER @ user:A

because of `union`, if anyone of these exists in DB, `check` evaluates to True.

## Architecture

Himeji (authorization) service is consist of 3 layers

1. Data Layer
2. Caching Layer
3. Orchestration Layer

Let's take a detailed look at each in detail.

### Data Layer

The data layer of the Himeji service consists of

- persistent relational database
- data is logically shared within the same instance
- any mutation in the data is read through CDC, streamed through Kafka, and used in invalidating the cache

### Caching Layer

The caching layer of the Himeji service is super-critical for performance as it ensures low response time at scale.

- ensures 98% hit ratio
- cache cluster is sharded
- consistent hashing determines the data ownership across the cluster

### Orchestration Layer

The orchestration layer is used by clients and internal jobs to interact with the service. The layer

- forwards reads to caching
- forwards the writes to the data layer
- computes response as per the config

This design is taken from @Airbnb's Engineering Blog and it is linked in the description of the video attached.