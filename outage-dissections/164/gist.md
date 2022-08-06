Getting the service up is P0 during the outage, but that is not all. There are a few other things that we need to take care of once the issue is mitigated.

## Resolve Inconcistencies

During the outage, the business logic or database must have crashed while handling in-flight requests; hence there is a very high chance of the data becoming inconsistent.

For example: if the process crashed while transferring money from one account to another; it is possible that money got deducted from one account but did not credit to another.

Hence once the outage is mitigated, the first thing to be done is to ensure that the data does not remain in an inconsistent state. Achieving this depends on the usecase at hand and the tech stack involved.

## Invalidate the Cache

Another place that needs attention is cache invalidation. If the outage sustains for a long time, there is a chance that some of the entries in the cache are not valid anymore.

Hence, depending on the usecase, it is advised to go through the cache entries and delete the invalid once ensuring the end-user sees a globally consistent view of the data.

## Audit alerting and monitoring

Once the outage is mitigated and the inconsistencies are resolved, it is better if we take a look into existing alerting and monitoring practices so that we ensure that we get alerted at the right time.

In most cases, you would find that a few things could always be improved when it comes to monitoring the right things, and hence an outage is an opportunity to get alerting and monitoring improvements prioritized.

## Take preventive measures

Every outage has a root cause, and it is super-important to fix the root cause to ensure that the over never happens again for the same reason. This requires us to go in-depth and take preventive measures to ensure complete closure.

For example, re-auditing all the INT32 columns and moving them to INT64 to ensure that we never repeat the outage due to integer overflow.