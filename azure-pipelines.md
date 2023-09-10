#### Pipelines
1. Build stage and deploy stage
   1. Build stage is used for compiling, testing and building artifact.
   2. Deply stage is used for deploying an artifact to an environment.
   3. Environment represents a deployment target. i.e kubernetes cluster, virtual machines, app service etc..
2. Stage may contain multiple jobs. Job may contain multiple steps. Each step is a task.
3. Release pipeline is different from the build pipeline.
4. Release pipeline can only be defined and/or edited with GUI. Build pipeline can be defined with yaml files.
5. Build and deployment can be performed in the build pipeline similar to Jenkins pipelines.
6. Pipeline file(s) needs to be configured for the repository.
7. Pipeline yml definition supports templates for reusability and modularity.
8. Pipelines are used for Continuous Integration.
9. Release are used for the Continuous deployment.
10. Stages in Azure Pipelines are the major divisions in a pipeline, such as “build this app”, “run these tests”, and "deploy to pre-production"2. They’re logical boundaries in your pipeline where you can pause the pipeline and perform various checks
11. 
