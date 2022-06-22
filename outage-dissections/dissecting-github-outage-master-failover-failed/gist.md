Master failover failed for GitHub leading to a 5-hour long incident, let's see what happened.

## Incident Summary

For five hours, GitHub users observed delays in data being visible on the interface and API after it was written on the database. This happened during the maintenance when they were switching the Master DB.

## Planned Maintenance

Planned maintenance is a popular way for companies to take a small downtime and execute all the maintenance activities. Some activities for which we do plan database maintenance are

- applying security patches
- apply version upgrades
- parameter tuning
- hardware replacement
- periodic reboots

A popular activity during database maintenance is to switch the Master node i.e. shift the traffic coming from the master node to a new node so that we could patch the old instance.

For a very short duration, when the config switch is happening, the database would be unavailable leading to a small outage; and this is expected behavior.

## Database Crash

During the failover, when the traffic was moved to the new database, the `mysqld` process crashed. This led to incoming writes failing. To quickly mitigate the issue, the team moved the traffic to the old database. This solved the issue and the site was up and running.

## Something interesting happened

The new database before crashing served the write traffic for 6 seconds. So, after the crash when the traffic was redirected to the old database, it did not have the data that was written in that 6 seconds window.

This is a huge concern, as it would lead to bad UX, and in the worst case consistency failures. So, how to remediate this issue?

## Remediating master failovers

In order to remediate this, we take the help of the Write Ahead Log or Commit log of the database. Whenever we do a failover, we always keep track of the `BINLOG` coordinates.

Once we moved the traffic to the old database, all we have to do is iterate through the BINLOG and apply all the changes that happened on the new database post the noted coordinate on the old database.

This would re-create or modify the exact data that was written to the new database on the old database, leading to zero data loss or consistency breach.

## Cleaning up the mess

Typically when we have such a failover, it is better that we restore the read replicas and hence GitHub team rotated all the replicas. Creating a read replica takes time, given the scale of GitHub.

It took them 4 hours to set up replicas and 1 hour to re-configure the cluster hence for over 5 hours the incident was affecting the users.