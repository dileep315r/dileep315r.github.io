#### Build systems

### [Brazil amazon build system](https://blog.bytebytego.com/p/ep56-system-design-blueprint-the?utm_source=post-email-title&publication_id=817132&post_id=116544428&isFreemail=false&utm_medium=email)
1. Team manages it's own repos.
2. Build file contains the build configuration.
3. A version set is a collection of package versions that offers a private space for the package and its dependencies. When a new package dependency is introduced, it must also be merged into this private space. There is a default version set called "live," which serves as a public space where anyone can publish any version.
4. Get/Download/Use dependencies from versionSet of the service while building the service.
5. Add new dependencies to the version set manually
6. Facility to set version set locally as well as in production.
7. Version set modifications are controlled using internal permissions management system.
8. Facility to explicitly select versions in case of version conflicts.
9. Built artifact can be published to the global "live" set if we choose to publish the artifact.
10. 