Canary deployments are implemented through a setup where a few servers serve newer version while the reset serves the old version.

A router (load balancer / API gateway) is placed in front of the servers and it routes the traffic to the new setup; the other requests continue to go to the old setup.

# Pros of Canary Deployments

- we test our changes on real traffic
- rollbacks are much faster
- if something's wrong only a small fraction of users are affected
- zero downtime deployments
- we can slowly and gradually roll-out the changes to users
- we can power A/B Testing

# Cons of Canary Deployment

- engineers will get habituated to test things in production
- a little complex setup
- a parallel monitoring setup is required to compare vitals side-by-side
  
# How should we select the users/servers for our canary setup?

The selection is use-case specific, but the common strategies are:

- geographical selection to power regional roll-out
- create specific user cohorts eg: beta users
- random selection

# When you absolutely need Canary Deployments

Say you own the Auth service that is written in Java and you chose to re-write it in - Golang. When taking it to production, you would NOT want to make a direct 100% roll-out given that the new codebase might have a lot of bugs.

This is where canary is super-helpful when we a fraction of servers serving requests from Golang server while others from the existing setup. We now forward 5% traffic to the new ones and observe how it reacts.

Once we have enough confidence in the newer setup, we increase the roll-out fraction to 15%, 50%, 75%, and eventually 100%. Canary setup thus gives us a seamless transition from our old server to a newer one.