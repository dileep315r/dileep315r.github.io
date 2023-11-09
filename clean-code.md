#### Naming
1. Prefixes before the class names, interface names, type names denoting their type are redundant and it's an old practice. You might have seen interface names like IInterface.
2. Variable names can abbreviated if it's used in a short scope. Variable names used in long scope should have long names that describe the intent of the variable.
3. Public clas names accessible in a long scope should have short names and the private class names used in a short scope should have long names describing the intent of the class. The same goes for public and private methods.
4. Using good names leads to well written pose.

#### Functions
1. Functions should only do one and only one thing.
2. Functions should be 10 lines at max. Ideally 3 or 4 lines.
3. Classes go hide in large functions that use local variables.
4. Functions should be extracted until you drop.
5. Body of if statements can also be another function.

#### Function structure
1. Three arguments at max to a function.
2. Boolean function declares to the world that it does two things. Function should do only one thing.
3. Don't use output arguments.
4. Don't use null as pseudo boolean. Don't pass nulls as arguments. Instead two functions to handle null(no arg function) and non null case.
5. Defensive programming is bad for internal use cases. Public facing APIs keep null checks. Internal code, rely on tech cases to make sure that the nulls are never passed.
6. Step down rule to order functions in a class: Public functions on the top, high level private function, lesser high level private functions, small private functions. Abstract to detailed. Scisors rule, public at top, private below, scissors cut the paper and give top paper to the user. Put public variables followed by private variables at the top of the class. No back references. No function below calls a function above.
7. Temporal coupling: Some functions should be called in the specified, documented order. For example close should be called after open. Functions that modify state introduce temporal coupling. Temporal coupling makes it hard to reason about the program. Functional programming encourage the use of pure functions that don't modify the state, they return always the same output for a given input.
8. Command query pattern: functions that return values don't modify the state and the functions that modify the state don't return the values.
9. Law of demeter: Tell don't ask. Don't ask for the state of the object, instead tell the object to perform an action. Train wreck(chained) pattern calls are bad, it packs so much information in a single line. My take: It also introduces the tight coupling since the high level component is directly depending on the low level component.
10. Switch statements are like a knot, they tighly bind dependencies. This introduces compile time dependencies of the modules. Checked exceptions also introduce compile time dependencies. Think of code as divided into two partitions main partition and the core partition. Main should depend on the core partition and the core should not depend on the main partition. Use switch statements in the main partition. Replace switch statements with base class and derived classes.
11. Avoid complex and multiple early returns from a function. They make it hard to understand code.
12. Function should do only one thing. Either handles exceptions or performs the core logic. Code should not be littered with exception handling logic. It's bad for readability.
13. Remember the stack implementation. Separate anonymous class objects are created for the exceptional cases.
14. Prefer to use the exceptions scoped to the class. Exception name and the context should give most of the information. Pass the message only if it is really necessary.
15. Return null values as output in extreme cases. Prefer to throw an exception instead. Suggested to avoid the functions returning error codes pattern.
16. Checked exceptions are bad. Changes to the overriden method exception in the signature leads to modification of the parent method signature which is an inverse dependency.
17. 
