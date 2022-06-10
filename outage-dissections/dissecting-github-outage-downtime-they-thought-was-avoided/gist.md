GitHub thought they avoided an outage by fixing a possible root cause 6 months in advance, but fate had different plans.

## Check Suites and Workflows

When we push any changes to any GitHub repository there are some checks that run. We can see them on our Pull Request and it basically prevents us from merging the PR until all checks are successful. We can also add custom checks on our own to the workflow.

An entry is made in the database for every execution of the check suite. This is a high frequency that would lead to heavy ingestion in the database table. A side effect it would be that the auto-incrementing ID column, which is typically a 32-bit integer would exhaust leading to the writes getting failed.

## GitHub's Anticipation

GitHub anticipated this situation 6 months in advance and they altered the column from 32-bit integers to 64-bit integers ensuring that even when the ID range exhausts the 32-bit limit it would lead to downtime.

But still, the team faced an outage, how? what happened?

## What exactly happened?

The service was able to create entries in the database about the check suite execution as the database supported 64-bit integers, but there was one external dependency that unmarshalled JSON strings to native objects which only supported 32-bit integers.

The service was responsible for pulling the jobs from the database and putting it in the queue to be picked up by executors. This service depended on the library and hence it was unable to execute the checks. This led to all the checks remaining in the pending state during the course of this outage.

## Impact on the Search service

The search service was also impacted by this as the indexing used queue as the source. Since the newer jobs were not put in the queue, they were not indexed in the search cluster (eg: ElasticSearch), and hence when the user searched, they could not find the latest checks and workflows.

## Mitigation

In order to mitigate the issue, the GitHub team released a code fix. Speculation: they would have updated the library version that would support 64-bit integers, or they might have quickly forked and patched it with the changes, or they might have written some ad-hoc job that temporarily pulled the jobs and put them in the queue.

This incident shows that no matter how big the company gets and how prepared are you for an extreme event, there would always be some blind spots in the system that would bite us back.