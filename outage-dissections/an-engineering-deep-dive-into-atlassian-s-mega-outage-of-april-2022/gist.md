In April 2022, Atlassian suffered a major outage where they "permanently" deleted the data for 400 of their paying cloud customers, and will take them weeks to recover the data. Let's dissect the outage and understand its nuances of it.

Disclaimer: I do not have any insider information and the views are pure speculation.

## Insight 1: Data loss up to 5 minutes

Because some customers reported a data loss of up to 5 minutes before the incident, it shows that the persistent backup incrementally every 5 minutes. The backup typically happens through Change Data Capture which operates right over the database.

## Insight 2: Rolling release of products

Atlassian rolls out features to a subset of the users and then incrementally rolls them to others. This strategy of incremental rollout gives companies and teams a chance to test the waters on a subset and then roll out to the rest.

## Insight 3: Mark vs Permanent Deletion

The script that Atlassian ran to delete had both the options - Mark of Deletion and Permanent deletion.

Mark for deletion: is soft delete i.e. marking is_deleted to true.
Permanent deletion: hard delete i.e. firing DELETE query

Why do companies need permanent deletion? for compliance because GDPR gives users a Right to be Forgotten

## Insight 4: Synchronous Replication

To maintain high availability they have synchronous standby replicas which means that the writes happening needs to succeed on both the databases before it is acknowledged back to the user. This ensures that the data is crash-proof.

## Insight 5: Immutable Backups

The backup is made immutable and stored on S3 in some serialized format. This immutable backup allows Atlassian to recover data at any point in time while being super cost-efficient at the same time.

## Insight 6: Their architecture is not truly a Multi-tenant Architecture

In a true multi-tenant architecture, every customer gets its fragment of infra - right from DB, to brokers, to servers. But at Atlassian, multiple customers share the same infra components. Companies typically do this to cut down on their infrastructure cost.

## Why is it taking a long time to restore?

Because data of multiple customers reside in the same database when the DB was backed up the data (rows and tables) were backed up as is; implying that the backup also had data from multiple customers.

Now to restore the intermingled rows of a customer, the entire backup needs to be loaded into a database and then the rows of specific customers need to be restored. This process is extremely time-consuming.