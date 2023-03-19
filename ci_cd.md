### Deployment types
1. Rolling deployment
2. Blue Green deployment -- Switch to standby cluster once the deployment is finished. Current active cluster will become the new standby after deployment.
3. Canary deployment -- New version is deployed to canary servers first and the change will be rolled out to all the servers if the canary deployment is successful.

### CI/CD
1. Goal: Ship high quality software faster to production.
2. CI -- Jenkins, Github actions
   1. Code -- github
   2. Build -- Maven, Gradle, Bazel
   3. Test -- Junit, Jest
   4. Release -- Jenkins
3. CD(continuous deployment)
   1. Deploy -- docker, argo, lambda
   2. Operate -- Kubernetes, Terraform
   3. Monitor -- Prometheus, datadog
   4. Plan -- JIRA, confluence
