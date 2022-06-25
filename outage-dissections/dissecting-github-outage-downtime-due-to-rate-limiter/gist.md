Rate Limiters are supposed to avoid downtimes, but what if they turn out to be the root cause of a major outage?

A large chunk of GitHub users saw elevated error rates and this happened after deploying their A/B Experimentation service. So, what went wrong? but before that let's understand what is A/B experimentation

## What is A/B Experimentation?

It is hard to decide which UI is better and hence before rolling out any critical UI change to all the users, a company tests it through an A/B experiment.

A set of users are chosen at random and a fraction of them are shown the new variation while others are shown the old one. Key vitals and metrics of the features are measured and compared to decide if the variation is indeed an improvement.

If the metrics are positive and significantly better then the new variation is rolled out to 100% of the users. This way companies ensure that the features that are rolled out are genuine improvements in the product.

## A/B Testing at GitHub

Every server that needs to participate in any A/B experiment fetches a configuration file that is dynamically generated using, say, Config Generator service.

The configuration allows granular controls for the A/B experiment and holds critical information that shapes experimentation. When any server requests for a config file, the request hits the config service and it, in turn, generates the file and sends it back to the user.

## What failed?

Because a lot of requests were made to the Configuration Service, the rate limiting module of the service started throttling and it prevented the configuration file to be generated and sent to the servers.

This affected the users who were part of this experiment and they saw elevated error rates as the frontend did not have the necessary information it required to power the experiment.

## Mitigation and Long-term Fix

As quick mitigation, the GitHub team disabled the dependency on the dynamically generated file and it restored the services to normal.

To ensure the outage would not happen due to the same reason, the Config Generator service would generate and cache the configuration files so that when a request comes, the file could be served directly from the cache instead of generating on the fly which was time consuming.

## Key Takeaways

- avoid sync dependencies between services and prefer async
- classify the services by severity tiers and run periodic audits of tier-1 services to ensure they are architected well and there are no blindspots