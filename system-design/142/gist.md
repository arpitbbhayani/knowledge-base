Blue Green Deployment is a deployment pattern that reduces the downtime during deployment by running two identical production setups called - Blue and Green.

During deployment when we reboot the API servers there are chances that the incoming request fail because the server is unresponsive for a short period. Also, it might happen that the release had a major bug and we need a quick rollback.

How can we achieve both of them in one shot? The answer is Blue Green Deployment.

## Implemention

Blue Green deployment is implemented by having a separate fleet of infrastructure for the old version - Blue and the new version - Green. The new infrastructure is identical to the old one.

The deployment flow

1. the new deployment artifact is tested and kept ready to be deployed
2. a parallel infrastructure is set up identical to the existing
3. the new version is deployed on the new fleet - Green
4. the correctness of the setup is validated
5. the proxy is re-configured to now forward 100% of traffic from the Blue (old) setup to the Green (new) setup
6. a final sanity test is run on the new fleet
7. the blue fleet is now shut down

## Pros of Blue Green Deployment

1. rollbacks are just a config change and hence quick
2. downtime during deployment is minimal
3. deployment is just a flip of a switch
4. disaster recovery is simple given we already have the automation to build a parallel setup
5. deployments can now happen during the working hours
6. debugging a failed deployment is simple as we have the infrastructure with the debug information handy

## Possible challenges

1. during the deployment the infrastructure cost shoots 2x
2. the stateful application would need to rebuild the state on new servers
3. the database would have to be shared between the fleets
4. any schema migration on the database needs to be backward and forward compatible
5. the API responses have to be forward and backward compatible
6. setting up this deployment strategy for the first time is difficult

## When to use Blue Green Deployment?

- when you need zero downtime deployment
- your infrastructure can tolerate 100% traffic switch
- you can bear the 2x cost of infrastructure during deployment

## Points to remember

- have a solid automation test suite to validate the correctness
- ensure forward and backward compatibility of API and schema changes
- infra cost will shoot up hence minimizing the time for which you are running 2x infra