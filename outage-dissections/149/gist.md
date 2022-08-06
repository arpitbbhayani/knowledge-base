Just imagine you trying to create a repository on GitHub and it is not working, and this happened to GitHub in April 2021 when their users were not able to create a new repository.

The root cause for this outage was something that seems unrelated - Scanning Secrets. The root cause makes this outage super interesting to dissect.

## What is Secret Scanning?

Our API servers need to talk to peripheral components like Databases, Cache, SaaS services, etc. This communication involves some sort of authentication and authorization through auth tokens, passwords, or secret keys.

Developers tend to commit the secrets in the settings/constant files and push them to GitHub. What if the repository content gets leaked? What if GitHub itself has a data breach and the attacker gets access to the private repositories?

If the secrets like AWS access keys, auth tokens, and DB passwords are leaked and the attacker can then get the dump of the data and ask for a ransom. Or they may even abuse the infrastructure to perform some illegal activities or mine cryptocurrencies.

Hence, GitHub periodically runs a job that checks all the repositories for any secrets that are committed and warns the user about it.

## Repository Creation Flow

When a repository is created an entry is made into the Secret Scanning table which is then used by a job that scans for potential secrets and notifies the owner.

## What led to the outage?

The GitHub team ran a data migration in which they moved the Secret Scanning table from a common database to its own cluster allowing it to scale independently.

GitHub team was unaware of this dependency! and hence after the migration of the table happened to a different database the creation of a new repository started failing to lead to this outage. It is interesting to see such mature products having blindspots.

## How did GitHub mitigate it?

The mitigation strategy of GitHub was to roll back the migration. Although it is unclear from the incident report on what exactly they did but there are a few speculations

1. they could have recopied the table quickly to the old database
2. whitelisted the database so that applications could connect
3. old table would have been intact and hence they would have just renamed and made it active again.

Again, it is pure speculation given we do not have any insider information nor they specified in the report. It would have been fun to have gone through their actual mitigation steps. We could have learned so much, but nonetheless, we did learn a few interesting insights from this outage.