Rolling Deployment is a deployment strategy that slowly replaces the previous version of the application with the new one by replacing the underlying infrastructure.

Say we have 9 servers and each one is running version 1 of the code. With rolling deployment, we roll out our changes i.e. version 2 of the code to one server at a time eventually covering all 9 servers. This is the core idea of the rolling deployment, however, the implementation could vary a bit.

A key thing to note here is the fact that deployment is incremental in nature which means during the deployment there would be a few servers that are serving the old version of the code and the remaining servers serving the newer version. Hence the changes we push should be both backward and forward compatible.

## Implementing Rolling Deployment

Rolling deployments are always gradual and graceful, and we typically happen through the below steps

1. Pick a server for deployment
2. Stop the incoming traffic by removing it from the load balancer
3. Wait for the existing requests to be completed
4. if we are not replacing the infra, pull the latest code and reload
5. if we are replacing the infra, delete the server and launch a new one with the new code
6. attach the server behind the load balancer and start serving the requests

## Tuning Rolling Deployment

### Concurrent Servers

Instead of deploying to one server at a time, we can deploy changes to `n` servers concurrently. This would complete the entire deployment quicker.

Choosing the appropriate `n` is critical as a small value would mean the deployment takes ages to complete and a large one would affect the availability during deployment.

### Double-Half Deployment

An interesting way to implement rolling deployment is to double the infrastructure and then delete the older half.

Say, we have 4 servers with version 1 of our code so in order to deploy the changes we add 4 new servers with the new version of the code to the infra taking our total count to 8, and then delete the 4 older servers. This way, what remains are the 4 servers with the newer version of the code.

## Pros of Rolling Deployments

- Cost efficient
- Rollouts are gradual
- Rollbacks are simple
- Deployment incurs zero downtime
- Much faster than Blue-Green Deployment
- Any hiccup during deployment affects only a fraction of the users

## Cons of Rolling Deployments

- No environment isolation
- Naive deployment takes a long time to complete
- Stateful applications are affected during deployment
- Changes we rollout should be backward and forward compatible