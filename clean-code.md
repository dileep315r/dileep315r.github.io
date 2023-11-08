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
7. 
