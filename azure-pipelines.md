#### Pipelines
![img](https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/media/key-concepts-overview.svg?view=azure-devops)
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
11. Azure pipelines yml syntax
    1. Strategy: For each occurrence of string1 in the matrix, a copy of the job is generated. The name string1 is the copy's name and is appended to the name of the job. For each occurrence of string2, a variable called string2 with the value string3 is available to the job.
      ```
       strategy:
           matrix: { string1: { string2: string3 } }
           maxParallel: number
       ```
    2. Parameters are only available at template parsing time. Parameters are expanded just before the pipeline runs so that values surrounded by ${{ }} are replaced with parameter values. Use variables if you need your values to be more widely available during your pipeline run.
    3. Variables are different from runtime parameters. Runtime parameters are typed and available during template parsing.
    4. Variables give you a convenient way to get key bits of data into various parts of the pipeline. The most common use of variables is to define a value that you can then use in your pipeline.
    5. When you define the same variable in multiple places with the same name, the most locally scoped variable wins. So, a variable defined at the job level can override a variable set at the stage level. A variable defined at the stage level overrides a variable set at the pipeline root level. A variable set in the pipeline root level overrides a variable set in the Pipeline settings UI.
    6. In a pipeline, template expression variables (${{ variables.var }}) get processed at compile time, before runtime starts. Macro syntax variables ($(var)) get processed during runtime before a task runs. Runtime expressions ($[variables.var]) also get processed during runtime but are intended to be used with conditions and expressions. When you use a runtime expression, it must take up the entire right side of a definition.
    7. In YAML pipelines, you can set variables at the root, stage, and job level. You can also specify variables outside of a YAML pipeline in the UI. When you set a variable in the UI, that variable can be encrypted and set as secret.
    8. Use templates to define variables in one file that are used in multiple pipelines.
    9. For YAML pipelines, a deployment typically refers to a deployment job. A deployment job is a collection of steps that are run sequentially against an environment. You can use strategies like run once, rolling, and canary for deployment jobs.
    10. For YAML pipelines, the build and release stages are in one, multi-stage pipeline.
    12. References
       1. https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#understand-variable-syntax
       2. https://learn.microsoft.com/en-us/azure/devops/pipelines/yaml-schema/jobs-job-strategy?view=azure-pipelines
       3. https://learn.microsoft.com/en-us/azure/devops/pipelines/process/runs?view=azure-devops#process-the-pipeline
       4. https://learn.microsoft.com/en-us/azure/devops/pipelines/process/variables?view=azure-devops&tabs=yaml%2Cbatch#understand-variable-syntax
       5. https://learn.microsoft.com/en-us/azure/devops/pipelines/get-started/key-pipelines-concepts?view=azure-devops
       6. https://learn.microsoft.com/en-us/azure/devops/pipelines/scripts/cross-platform-scripting?view=azure-devops&tabs=yaml
   
      
       
