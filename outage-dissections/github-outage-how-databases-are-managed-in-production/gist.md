Managing databases in production is not easy and it does require a lot of tooling to keep it up and running. GitHub had an outage that gives us a glimpse of the toolings they use in production. So, here's what happened

## Incident Summary

The GitHub team updated the ProxySQL and a week later a master node in a critical database cluster crashed. A replica was promoted as the new master, and it also crashed. The team tried to manually recover, but the manually promoted replica also crashed.

Finally, the GitHub team did a full revert - reverted all the code changes, and also downgraded the ProxySQL version. Post this, things become normal and the master did not crash.

## ProxySQL

ProxySQL is a database proxy that sits between the servers and the database cluster. The server seamlessly connects to the ProxySQL and fires the usual SQL queries and the proxy forwards it to the data node as per the configuration.

### Why do we need ProxySQL

- better connection management
- as a cache for SQL query responses
- a gatekeeper to handle security and routing

## Orchestrator

Orchestrator is a MySQL topology management tool that helps us achieve High Availability on a MySQL cluster. It keeps an eye on all the nodes and takes corrective actions whenever something goes wrong.

We configure Orchestrator to keep an eye on the master node and as the node crashers, it promotes a replica to become the new master. Given that all of this happens automatically, it just takes a few seconds for the cluster to recover from the master crash.

### Anti-flapping policy

A very common cascading failure happens when the master fails and a replica is promoted to be the new master. Due to the high load, say the new master also crashed. The cycle thus continues until all nodes crash leading to a complete outage.

The anti-flapping policy of Orchestrator prevents this complete outage by not promoting replica to master until the cool-off period ends. Once the replica is promoted to be the new master, Orchestrator does not promote another replica until the cool-off period ends.

Although the master is down, this anti-flapping policy ensures that we are at least partially functional and can continue serving some reads. Along with this, we see only a small subset of nodes are thrown in the fire and hence have fewer data nodes to recover.

## Mitigation

To mitigate the issue, the GitHub team

- reverted the ProxySQL version
- reverted the code that required an upgraded version of ProxySQL

With this full revert, the master node stopped crashing and things become normal again.