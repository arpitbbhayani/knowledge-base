Canary Deployments is a deployment pattern that rolls out the changes to a limited set of users before doing it for 100%.

We compare the vitals side-by-side from the old setup and the canary servers to ensure everything is as expected. If all is okay, then we incrementally roll out to a wider audience. If not, we immediately roll back our changes from the canaries.

Canary Deployment thus acts as an Early Warning Indicator to prevent a potential outage.

## Why canary deployment is named canary deployment?

In 1920, coal miners used to carry caged canaries with them. If the gases in the mines were highly toxic the canaries would die and that alerted the miners to evacuate immediately, thus saving their lives.

In canary deployment, the canary servers are the caged canaries that alert us when anything goes wrong.

## Implementing canary deployment

Canary deployments are implemented through a setup where a few servers serve the newer version while the reset serves the old version.

A router (load balancer / API gateway) is placed in front of the setup and it routes some traffic to the new fleet while the other requests continue to go to the old one.

## Pros of Canary Deployment

- we test our changes on real traffic
- rollbacks are much faster
- if something's wrong only a fraction of users are affected
- zero downtime deployments
- we can gradually roll out the changes to users
- we can power A/B Testing

## Cons of Canary Deployment

- engineers will get habituated to testing things in production
- a little complex setup
- a parallel monitoring setup is required to compare vitals side-by-side

## Selecting users/servers for canary deployment?

The selection is use-case specific, but the common strategies are:

- geographical selection to power regional roll-out
- create specific user cohorts eg: beta users
- random selection

## When we absolutely need Canary Deployments

Say you own the Auth service that is written in Java and you chose to re-write it in - Golang. When taking it to production, you would NOT want to make a direct 100% roll-out given that the new codebase might have a lot of bugs.

This is where canary is super-helpful when we a fraction of servers serving requests from Golang server while others from the existing setup. We now forward 5% traffic to the new ones and observe how it reacts.

Once we have enough confidence in the newer setup, we increase the roll-out fraction to 15%, 50%, 75%, and eventually 100%. Canary setup thus gives us a seamless transition from our old server to a newer one.