#### Spring boot
1. Configuring Spring is hard. Spring boot is the solution.
2. Spring boot is opinionated, customizable.
   1. Example opinion. Inclusion of spring-boot-starter-web in dependencies
      1. Tomcat embedded web server container
      2. Hibernate for Object-Relational Mapping (ORM)
      3. Apache Jackson for JSON binding
      4. Spring MVC for the REST framework
3. Starters
   1. A starter is essentially a set of dependencies (such as a Maven POM) that are specific to the type of application the starter represents.
   2. Limit the amount of manual dependency configuration that you have to do.
   3. Examples: spring-boot-starter-web, spring-boot-starter-jdbc
4. Auto-configuration
    1. Auto-configuration is based on the JARS in your classpath and how you've defined your beans.
       1. For example, if you have the H2 database JAR in your classpath and have configured no other DataSource beans, then your application will be automatically configured with an in-memory database.
       2. For example, if you annotate your JPA beans with @Entity, then Spring Boot will automatically configure JPA such that you do not need a persistence.xml file.
    2. Fire up your Spring Boot application with the --debug option and an auto-configuration report will be generated to the console.
5. Packages application and its dependencies into a single, executable JAR.
   ```
   java ‑jar PATH_TO_EXECUTABLE_JAR/executableJar.jar
   ```
   1. Spring tool support (for example, the spring-boot-maven plugin) then builds the executable Uber JAR to follow that layout (not just unpacking and repackaging .class files, as with a shaded JAR).

#### Details
1. It's important to note that the <parent> element does a lot of cool Maven magic, so if you have a good reason for not using it, proceed with caution. Make sure to add a repackage goal execution to the spring-boot-maven-plugin (see Spring Boot Maven Plugin Documentation).
2. Spring Framework also offers built-in support for typical tasks that an application needs to perform, such as data binding, type conversion, validation, exception handling, resource and event management, internationalization, and more.
3. Use https://start.spring.io/ project to initialize the project
4. Because Jackson 2 is on the classpath, Spring’s MappingJackson2HttpMessageConverter is automatically chosen to convert the Greeting instance to JSON.
5. RestTemplate makes interacting with most RESTful services a one-line incantation. And it can even bind that data to custom domain types.
   1. Following code to access external REST services
      ```
      @Bean
       public RestTemplate restTemplate(RestTemplateBuilder builder) {
           return builder.build();
       }

       @Bean
       public CommandLineRunner run(RestTemplate restTemplate) throws Exception {
           return args -> {
               Quote quote = restTemplate.getForObject(
                       "http://localhost:8080/api/random", Quote.class);
               log.info(quote.toString());
           };
       }
       ```
6. Data access
   1. CustomerRepository extends the CrudRepository interface. The type of entity and ID that it works with, Customer and Long, are specified in the generic parameters on CrudRepository. By extending CrudRepository, CustomerRepository inherits several methods for working with Customer persistence, including methods for saving, deleting, and finding Customer entities. 
   2. Spring Data JPA also lets you define other query methods by declaring their method signature. For example, CustomerRepository includes the findByLastName() method.
   3. In a typical Java application, you might expect to write a class that implements CustomerRepository. However, that is what makes Spring Data JPA so powerful: You need not write an implementation of the repository interface. Spring Data JPA creates an implementation when you run the application.
#### Definitions
In the Spring framework, the interface ApplicationContext represents the IoC container.

The Spring framework provides several implementations of the ApplicationContext interface: ClassPathXmlApplicationContext and FileSystemXmlApplicationContext for standalone applications, and WebApplicationContext for web applications.

Dependency Injection in Spring can be done through constructors, setters or fields.

For a bean with the default singleton scope, Spring first checks if a cached instance of the bean already exists, and only creates a new one if it doesn't. If we're using the prototype scope, the container returns a new bean instance for each method call.

Class annotated with @Configuration contains configuration for constructing beans. Alternative to XML configuration in some cases. [See](https://www.baeldung.com/inversion-control-and-dependency-injection-in-spring) for more info.
Spring resolves each argument primarily by type, followed by name of the attribute, and index for disambiguation.

***Manual wiring XML declaration***: For setter-based DI, the container will call setter methods of our class after invoking a no-argument constructor or no-argument static factory method to instantiate the bean.
Field injection for private properties in class. Fields are annotated with @Autowirted. Try to not use it as spring uses reflection to insert objects, and it's costly.
The Spring documentation recommends using constructor-based injection for mandatory dependencies, and setter-based injection for optional ones.

Store class with Item property. While constructing the Store object, if there's no constructor or setter method to inject the Item bean, the container will use reflection to inject Item to store.

Wiring types:
1. Manual wiring
   1. Explicitly construct the objects in methods annotated with @Bean in @Configuration class. Similar to @Provides method in Guice.
2. Auto-wiring
   1. Annotate classes with Autowire annotations, spring will construct the annotations automatically. Similar to @Inject methods in Guice.

Lazy initialization of the beans is supported. Similar to by lazy<T> in other dependency injection frameworks.

#### Annotations
1. @EnableAutoConfiguration : enable Spring Boot's auto-configuration mechanism.
2. @Configuration : Allow to register extra beans in the context or import additional configuration classes.
3. @Bean: Spring annotation, method annotation with @Bean produces an object. Used in classes with @Configuration annotation.
4. @Autowired: Spring annotation. Used to instruct spring to set the value of property while constructing an object of a class.
5. @ComponentScan: Scan for the bean definitions in the package of the class that's annotated with @ComponentScan.
   1. we can tell Spring where to search for these annotated classes, as not all of them must become beans in this particular run.
   2. we can also customize the packages for search.
   3. we use the @ComponentScan annotation along with the @Configuration annotation to specify the packages that we want to be scanned.
   4. @ComponentScan without arguments tells Spring to scan the current package and all of its sub-packages.
   5. Only the location of the configuration class matters, as component scanning starts from its package by default.
   6. 

*** Definitions ***
1. Spring bean: A bean is an object that is instantiated, assembled, and otherwise managed by a Spring IoC container.

#### References
1. [REST application](https://spring.io/guides/gs/rest-service/)
2. [Accessing REST apps](https://spring.io/guides/gs/consuming-rest/)
3. [Accessing data with JPA](https://spring.io/guides/gs/accessing-data-jpa/)
4. https://spring.io/guides/tutorials/rest/