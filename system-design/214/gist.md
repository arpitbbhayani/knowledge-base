One of the features of Slack is the ability to invite people to join a workspace by email. However, not all email addresses belong to the same organization, and it is a challenge to distinguish between internal and external invites.

In this article, we will discuss the technical details of how Slack classifies emails to provide a smoother product onboarding experience.

## Need for classification

Onboarding employees and external vendors into a Slack workspace can be a tedious process. Depending on who is being invited, an internal or an external onboarding flow will be triggered. This can be as simple as showing a different dialogue.

A solution to this problem is an email classification service that classifies every email into an internal, or external category. This service kicks in when a user types in an email address during the invitation process.

## Heuristics

Slack's email classification service attempts to classify emails by using heuristics. For example,

- if the user's domain is one of the allowed ones, then the user is internal
- if the domain of the inviter matches the domain of the invitee, the invitee is classified as per the inviter's class.

###But heuristics fail

The above two approaches are simple and effective for Slack workspaces that are homogeneous (having one or few email domains). But, things become interesting when the number of email domains is many and there is no one rule that will fit.

Slack solves this classification problem by keeping track of all domains part of a workspace and using that aggregated count to determine the class.

## Implementation Details

To implement this classification, Slack maintains a table called `domains` which stores the aggregation (count) per `(team, domain, role)`. This table effectively answers how many users of a workspace have a particular domain and a specific role.

For example workspace, `A` has `68` members having the role `member`, while `6` members with the role `admin`.

The count is maintained with eventual consistency. User-created, updated, and deleted events are sent to Kafka, and consumed by a set of consumers to update the `domains` table.

### Classifying Threshold

Slack operates with a threshold of 10%, which implies that a domain is considered internal if there are at least 10% or more employees in the organization with a given domain, otherwise, it is classified as external.

### Adding a new user

While processing the `user_created` event, Slack does `upsert` instead of an `update` as upserts allow us to not check for the existence of the row with matching constraints.

```
UPSERT count = count + 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "member";
```

### Changing the role

If a user's role changes from `member` to `admin`, the count for the member role is decremented, and the count for the admin role is incremented transactional.

```
UPSERT count = count + 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "admin";

UPSERT count = count - 1 WHERE
team_id = 1 AND domain = "bar.com" AND role = "member";
```

### Reprocessing the message

One challenge is that user events can be processed twice causing the numbers to drift. To overcome this challenge, Slack uses a healing mechanism that automatically corrects drifts.

The healer process goes through all the users, until a certain timestamp, and extracts their email domains to perform the count in memory. It then computes the drift from numbers stored in the `domains` table.

Instead of updating the database with the observed count, it pushes the drift as a separate message `+N / -N`. This ensures that numbers in the `domain` table always converge to the correct value and are eventually consistent.

## Conclusion

Slack's email classification service is a critical feature that helps give a smoother invitation experience to users. Classifying emails accurately is a challenging problem, but Slack has implemented an effective solution by using a table to maintain counts and eventual consistency.