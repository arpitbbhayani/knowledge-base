### Why a database goes down?
An unexpected heavy load on your database can lead to a process crash or a massive slowdown.

Before jumping to the potential short-term and long-term solutions, ensure you monitor the database well. CPU, Memory, Disk, and Connections are being closely monitored.

## Short term solutions

- Kill the queries that have been running for a long time
- Quickly scale up your database if you have been seeing a consistent heavy usage
- Check if the recent deployment is the culprit; if so, revert asap
- Reboot the database will calm the storm and buy you some time

## Long term solutions

- Ensure the right set of indexes is in place
- Tune your database default parameters to gain optimal performance
- Check for the notorious N+1 Queries
- Upgrade the database version to get the best that DB can offer
- Evaluate the need for Horizontal scaling using Replicas and Sharding