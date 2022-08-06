Outages are inevitable; but we should design our architecture and ensure that if a component is down, it should not lead to a complete outage.

## What happened with GitHub?

GitHub saw a lot of failures with their Actions service and this led to delays in queued jobs from being processed. The root cause was some infrastructure error in the SQL layer.

## Insights about their architecture

A couple of insights about their architecture

### Synchronous dependency

Although GitHub Actions look like a single feature, internally it consists of multiple microservices. Some of these, have a synchronous dependency on the database. Because of this, when the DB had a hiccup, the entire Actions feature was hindered.

### Zero trust communication

The service that was most affected in this outage handled communication; why would services need authentication? they are all internal the infrastructure?

Microservices talk. The communication needs to be protected with auth so that any engineer/service gone rogue cannot abuse the system in any capacity. Only authenticated and authorized services are allowed to take action.

## What about automatic failover?

Given that the outage happened on the database layer, why did the database did not auto-recover? it is a standard procedure and configuration that would have just promoted a replica to be the new master.

Although it is a common config, during this outage the metrics did not show any issue with the database, and hence the auto-failover was never triggered. It took a long time to even understand the root cause and then start mitigation.

## Long-Term Fixes

### Update the automation scripts

The automation that reads the telemetry and decides to do a failover needs to be updated so that such failures are detected and action is taken.

### Localizing failures

An important long-term change that needs to be driven is to localize the failure. In this outage, we learned how a hiccup in one database/service causes downtime of all dependent Microservices. This shouldn't have happened as the Microservices are supposed to solve this very problem.

A good way to ensure that the blast radius of the outage is minima; is by ensuring the failures are localized, implying, that when a service is down, only the service is affected while everything else is functioning perfectly fine.

A common approach to getting this loose coupling is by powering inter-service communication through the asynchronous medium instead of synchronous API calls. Thus, if something breaks, we could fix it and continue to process the messages.