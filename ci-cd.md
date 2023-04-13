#### CI/CD
CI makes software development easier, faster, and less risky for developers. By automating builds and tests, developers can make smaller changes and commit them with confidence. Software developers get feedback on their code sooner, increasing the overall pace of innovation.

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

Building an executable jar makes it easy to ship, version, and deploy the service as an application throughout the development lifecycle, across different environments, and so forth.

#### Backward compatibility
1. The previous example demonstrated that the seemingly trivial changes to the software are more complicated when they need to perform in a distributed system safely. As a consequence, maintaining backward compatibility imposes a tradeoff between agility and safety.
2. The simplest way to deploy new versions of the software with zero downtime is to perform rolling deployments instead of deploying in lockstep the software to all the servers at the same time.
3. Semantic versioning
   1.  the clients of the software can easily understand the compatibility characteristics of new software and the associated implications.
   2. When providing software as a binary artifact, the version is usually embedded in the artifact. The consumers of the artifact then need to take the necessary actions if it includes a backwards incompatible change, e.g., adjusting their application’s code.
   3. Protocol negotiation is another technique for maintaining backward compatibility through the use of explicitly versioned software.
   4. Semantic versioning is implemented slightly differently in live applications. The major version needs to be embedded in the address of the application’s endpoint, while the minor and patch versions can be included in the application’s responses. For an example, see this. This is needed so that clients can automatically upgrade to newer versions of the software if desired, but only if these are backward compatible
   5. In some cases, an application might not be aware of the other applications consuming its data. An example of this is the publish-subscribe model.
   6. However, it’s still very important to ensure that the consumers can deserialize and process any produced data successfully as its format changes.
   7. One pattern used here is defining a schema for the data used by both producers and consumers. This schema can be embedded in the message itself. Otherwise, to avoid duplication of the schema data, a reference to the schema can be put inside the message, and the schema can be stored in a separate store. For example, this pattern is commonly used in Kafka via the Schema Registry.
   8. So, producers need to preserve compatibility either by ensuring consumers can read data of the new schema using an older schema or by ensuring all consumers have started using the new schema before producing messages with it.
   9. This technique of splitting a change into two parts to make it backward compatible is commonly used and it’s also known as two-phase deployment.
