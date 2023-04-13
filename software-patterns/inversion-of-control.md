#### Inversion of control
### Definition    
```
1. High level modules should not depend on low level modules; both should depend on abstractions.
2. Abstractions should not depend on details. Details should depend upon abstraction.
```

### Benefits of IoC containers
1. It makes it easy to switch between different implementations of a particular class at runtime.
2. Easy to write unit and integration test cases.
3. IoC manages the lifecycle of objects and their configuration. 
   1. Imagine managing hundreds of instances of objects in the application.
   2. Might create duplicate objects if objects are not properly managed. Objects might stay in memory even if they are not needed if IoC is not used.
