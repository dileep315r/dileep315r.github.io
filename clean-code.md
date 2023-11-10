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

### Form
1. Comments
   1. Best comment is the comment not written. Comments and code tends to go out of date. If you write the same info in multiple forms, they tend to diverge and become inconsistent.
   2. "The only reliable documentation of a computer "program is the code itself. "The reason is simple. "Whenever there are multiple representations "of a program, the chance for discrepancy exists. "If the code is in error, artistic flow charts "and detailed comments are to no avail. 
   3. Every comment is an aknowledgement of the failure to express well.
   4. No html in comments as the users can't understand them easily. Comments should only contain the information for the readaer of the code.
   5. Big banner comments are a big no. Since we almost always ignore them.
   6. Nothing can be quite so useful as a well documented public API. If you're using a tool, like Javadoc, or some other automated documentation tool, you should certainly write nice documents for your public APIs. Of course, you should also make sure that your function signatures are self-explanatory. And, keep in mind the best public API documentation is the documentation you don't have to write. 
   7. Comments should describe new information. No redundant information in comments.
   8. Comments also rot because they tend to be non-local. When you change a local line of code in some module in order to fix a bug, or add a new feature, how do you know that there's not some comment somewhere else in the code that you just invalidated?
   9. Code should document itself.
   10. No TODO comments. Use issue tracking systems instead.
   11. No mumbling in comments.
   12. Journal comments. You do have a source code control system, right? Well, then us it.
   13. When you see commented out code, you must delete it. Exponge it from the source code. Don't read it, don't touch it, don't try to understand it.
   14. Rather than using comments to describe what your code does, learn how to use explanatory variables and names. 
2. Dead code: Remove dead code, version control system tracks them anyway.
3. Line length: Remember, never make your readers scroll right. 120 chars at max.
4. Indentation, stick to one style with the team.
5. Space between if/while statements. Group the variables that are related. Variables that aren't related should be spaced. If the functions are four lines long, then you don't need very many of the spaces.
6. As in everything else in software, smaller is better. Keep your file sizes small.
7. Classes
   1. The methods of a class manipulate the variables of that class. The more variables within a class that a method manipulates, the more cohesive that method is. A maximally cohesive method manipulates every variable inside the class. A maximally cohesive class is composed of nothing but maximally cohesive methods. Getters and setters are not very cohesive because they only manipulate a single variable each. The more getters and setters a class has, the less cohesive that class is. So, does that mean that a class should never have getters and setters? Dogmatic rules like that seldom apply in engineering disciplines. I certainly write getters and setters from time to time, but I try to minimize them, because I try to maximize cohesion.
   2.  In those instances where I choose to have a getter, I don't simply expose the variable. I try to abstract out the information being retrieved.
   3.  To be more specific, polymorphism allows us to protect client code, like CarDriver, from changes to the implementation of server code, like Car. It's pretty easy to write a CarDriver that can drive any derivative of Car, without knowing our caring what that derivative is.
   4.  Maybe, you're wondering about classes like Employee, that clearly have methods like getName and getAddress that expose the data within them.
   5. A data structure is kind of the opposite of a class. A data structure has a whole bunch of data variables that are public, and virtually no functions. Do you see the difference here between a class and a data structure? Classes have private variables but public functions. Data structures have public variables and no functions. It might be going a bit too far to say that data structure have no methods. Data structures can have methods. But typically, they're simple things like getters, or setters, or little navigation aids. The methods of a data structure manipulate individual variables. They don't manipulate cohesive groups of variables the way the methods of a class do.
   6. We use classes and objects when it's types that are more likely to be added. We use data structures and Switch statements when it's methods that are more likely to be added. 
   7. For years and years, design experts have been telling us that we should design our applications so that they are separated from our databases by some kind of interface layer. This is very good advice. The last thing we want to see is a bunch of SQL code smeared through our application code.
   8. When getters are absolutely necessary, make sure you hide the implementation of the data by abstracting it. And, use classes to protect yourself from new types, but not new functions. Data structures are bags of data with no cohesive methods. Don't put business rules into data structures. Manipulate them with Switch statements if you must, and use them to protect yourself from new functions, but not new types. Boundaries crisscross our application, separating things that are concrete from things that are abstract. And, all source code dependencies cross those boundaries pointing away from the concrete stuff towards the abstract stuff. Remember that domain objects and database tables are not the same thing, and aren't even strongly related. Separate your domain objects from you database by putting a layer in between them. 
