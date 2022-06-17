We all love creating microservices, but there should be a standard way of creating them?

If we give complete autonomy to engineers to build their services then we will end up with the chaos of languages, frameworks, tools, and conventions. Hence standardization becomes essential to limit the chaos.

Standardization allows us to keep the entire system coherent and uniform and the 3 verticals that need standardization are:

## Monitoring

Monitoring one microservice is relatively a simpler problem, and with easy-to-integrate tools, it becomes a breeze. Few examples

- logging tools - ELK or EFK
- APM tools - NewRelic or DataDog
- status code monitoring on cloud consoles

Monitoring how a request originates from the user and goes through various services is important and this problem of Distributed Tracing can be solved through tools like Zipkin and AWS X-Ray.

Microservices need a standard way of reporting key metrics like CPU, Memory, Disk, and App Metrics into a central system like NewRelic or CloudWatch allowing everyone to get the necessary transparency.

## Interfaces

There are 100s of ways through which the microservices could talk to each other. This demands standardization and we need to consolidate on a few ways of interfacing.

Consolidating to REST for user-to-service communication and gRPC for service-to-service communication seems to be the most popular choices. But it is totally up to you to pick the ones.

We cannot allow the communication to happen over a variety of formats and hence we need to consolidate on a few like - JSON and ProtoBuf.

We also need to standardize the nomenclature and how REST endpoints are written. This would ensure that the entire engineering team feels familiar while writing any inter-service communication.

Other aspects that need standardization are Versioning, Timeouts, and Retries. Having this standardization would allow us to write common libraries to abstract out the implementation complexities and save redundant efforts.

## Tolerance

Every service needs to shield itself from getting bombarded. Standardizing the tolerance would save us redundant efforts and implementations. A common protection layer would not only prevent the service from getting overwhelmed but also ensure no cascading failures.

Some standard configurations could be

- limit the number of incoming calls from a service
- ability to cut off incoming and outgoing requests from/to a service

Such abilities would help us reduce outage times and prevent cascading failures as engineers would be aware of exactly what to do to cut off.