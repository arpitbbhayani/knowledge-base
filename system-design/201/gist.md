DynamoDB does not support aggregation queries, but we need it for a use case; let's build a real-time DDB aggregation today...

Deliveroo, a food delivery startup had a similar problem. On their app, people can mark a restaurant as "favorite" and now they wanted to render restaurants ordered by most favorite first.

## Data Model

We have a `favorites` table in which we store users and their favorite restaurants. The table has `restaurant_id_user_id` as their primary key and `created_at`, and `user_id`, as other attributes.

With the above data model, getting if a user marked a restaurant as a favorite is an O(1) lookup and so are the marking and unmarking activites.

## Getting restaurants ordered by favorite count

With this data model, it becomes near impossible to get restaurants ordered by their favorite count, purely because DynamoDB does not support aggregations.

### Core idea

Maintain a separate table having aggregated favorite count as one of the attributes and use it to get tables ordered by favorite count.

### Data Model

Introducing a new table `aggregated_favourites` having the following schema

- `rastaurant_id` as the primary key
- `time_window` as the sort key
- `favourite_count`, `updated_at` as other attributes.

### Data Flow

We set up a DynamoDB stream that would contain all the events happening on the `favorites` table. This stream will be consumed by an AWS lambda function.

The lambda function will transactional do `count++` upon every creation and `count--` on deletion.

This way, we maintain the aggregated favorite count for each restaurant in near-realtime without doing any fancy code changes.

### Advantages

- extremely cost coefficient for Deliveroo scale
- count updation is asynchronous, hence API response time unaffected
- better than running a daily cron job or doing a sync write to the aggregated table.