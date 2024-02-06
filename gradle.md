1. In Gradle, Builds consist of one or more projects and each project consists of one or more tasks.
2. doFirst and doLast add actions at the top and bottom of the action list, respectively, and can be defined multiple times in a single task.
3. Here, we’re setting “theValue” as theProperty of the ourTask task.
4. There’re two types of plugins in Gradle – script, and binary. To benefit from additional functionality, every plugin needs to go through two phases: resolving and applying.
5. Resolving means finding the correct version of the plugin jar and adding that to the classpath of the project. Applying plugins is executing Plugin.apply(T) on the project.
6. Script Plugins: ```apply from: 'aplugin.gradle'``` Now, executing gradle tasks command should display the fromPlugin task in the task list.
7. Binary Plugins Using Plugins DSL: ```plugins {id 'application' }``` In the case of adding a core binary plugin, we can add short names or a plugin id. To apply a community plugin, we have to mention a fully qualified plugin id
   1. Plugins DSL cannot be written in scripts plugin, settings.gradle file or in init scripts
   2. plugins block needs to be the top level statement in project’s build scripts (only buildscripts{} block is allowed before it)
8. Legacy ```apply plugin: 'war'```
    1. If we need to add a community plugin, we must add the external jar to the build classpath using the buildscript{} block.
    2. Then, we can apply the plugin in the build scripts but only after any existing plugins{} block:
9. Gradle supports a very flexible dependency management system, it’s compatible with the wide variety of available approaches. Best practices for dependency management in Gradle are versioning, dynamic versioning, resolving version conflicts, and managing transitive dependencies.
   1. Dependencies are grouped into different configurations. A configuration has a name and they can extend each other.
   2. The default configuration extends “runtimeOnly”.
   3. Sometimes we need dependencies that have multiple artifacts. In such cases, we can add an artifact-only notations @extensionName (or ext in the expanded form) to download the desired artifact
      1. ```runtimeOnly group: 'org.codehaus.groovy', name: 'groovy-all', version: '2.4.11', ext: 'jar'```
   4. When we want to avoid transitive dependencies, we can do it on the configuration level or on the dependency level:
      ```
      configurations {
          testImplementation.exclude module: 'junit'
      }
       
      testImplementation("org.springframework.batch:spring-batch-test:3.0.7.RELEASE"){
          exclude module: 'junit'
      }
      ```
10. In the initialization phase, Gradle determines which projects are going to take part in a multi-project build. This is usually mentioned in settings.gradle file, which is located in the project root. Gradle also creates instances of the participating projects.
11. In the configuration phase, all created project instances are configured based on Gradle feature configuration on demand.
12. Init phase, Configuration phase, Execution phase
13. Source sets partition the sources. Tasks operate on source sets. Attributes can be attached to the sourcesets. Set of dependencies are configured using configuration blocks. Tasks utilize the dependency config 

### References
1. https://docs.gradle.org/current/javadoc/org/gradle/api/Project.html
2. https://www.baeldung.com/gradle
