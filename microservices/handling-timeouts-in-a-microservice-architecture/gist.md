How to handle timeouts in a microservice architecture? [ in a gist ]

Microservices give us the flexibility to pick the best tech stack to solve the problem optimally. But one thing that ruins the real thrill is Timeouts.

Say we have a blogging website where a user can search for blogs. The request comes to the Search service, and it finds the most relevant blogs for the query.

In the response, a field called "total_views" should hold the total number of views the blog received in its lifetime. The search services should talk to the Analytics service synchronously to get the data. This synchronous dependency is the root of all evil.

The core problem: Delays can be arbitrarily large

Because the delay from depending on service can be arbitrarily large, we know how long to wait for the response. We for sure cannot wait forever, and hence we introduce Timeout. Every time the Search service invokes the Analytics service, it starts a timer, and if it does not get a response in the stipulated time, it timeout and moves on.

There are 5 approaches to handling timeouts.

Approach 1: Ignore the timeout and move on
Approach 2: Use some default value if you timed out
Approach 3: Retry the request
Approach 4: Retry only when needed
Approach 5: Re-architect and make synchronous dependency an async one