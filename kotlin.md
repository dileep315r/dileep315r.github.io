#### Kotlin
1. [Arrays](https://kotlinlang.org/docs/arrays.html#primitive-type-arrays) in Kotlin are represented by the Array class. It has get() and set() functions that turn into [] by operator overloading conventions, and the size property
2. Kotlin also has classes that represent arrays of primitive types without boxing overhead: ByteArray, ShortArray, IntArray, and so on. 
   1. Use intArrayOf() helper method to create primitive array. Use arrayOf() function to create an array.
3. Kotlin numbers
   1. Kotlin has Byte, Short, Int, Long primitive types for integers. 
   2. No boxing overhead for primitive integers. 
   3. By default, compiler assigns the smallest type for an integer literal assignment. 
   4. Integer is a boxed type. UByte, UShort, UInt, ULong are unassigned primitive integers.
   5. Float and Double are primitive floating point types.
   6. Nullable primitive types like Int? are boxed types.
4. Boolean, String, Char are primitive types.
5. when for switch cases.
6. Smart cast in kotlin.
7. [Higher order functions, function types and lambda expressions](https://kotlinlang.org/docs/lambdas.html#function-types)
   1. Kotlin functions are first-class, which means they can be stored in variables and data structures, and can be passed as arguments to and returned from other higher-order functions. You can perform any operations on functions that are possible for other non-function values.
   2. All function types have a parenthesized list of parameter types and a return type: (A, B) -> C denotes a type that represents functions that take two arguments of types A and B and return a value of type C. The list of parameter types may be empty, as in () -> A. The Unit return type cannot be omitted.
   3. Function types can optionally have an additional receiver type, which is specified before the dot in the notation: the type A.(B) -> C represents functions that can be called on a receiver object A with a parameter B and return a value C. Function literals with receiver are often used along with these types.
   4. The arrow notation is right-associative, (Int) -> (Int) -> Unit is equivalent to the previous example, but not to ((Int) -> (Int)) -> Unit.
   5. You can also give a function type an alternative name by using a type alias
   6. Lambda expressions and anonymous functions are function literals. Function literals are functions that are not declared but are passed immediately as an expression.
   7. There are several ways to obtain an instance of a function type:
      1. Use a code block within a function literal, in one of the following forms
         1. a lambda expression: ```{ a, b -> a + b }```
         2. an [anonymous function](https://kotlinlang.org/docs/lambdas.html#anonymous-functions): ```fun(s: String): Int { return s.toIntOrNull() ?: 0 }```
      2. Use a callable reference to an existing declaration:
         1. ::isOdd, String::toInt or List<Int>::size or ::Regex or foo::toString
      3. Use instances of a custom class that implements a function type as an interface:
         1. ```val intFunction: (Int) -> Int = IntTransformer()```
      4. A value of type (A, B) -> C can be passed or assigned where a value of type A.(B) -> C is expected, and the other way around
   8. A value of a function type can be invoked by using its invoke(...) operator: f.invoke(x) or just f(x).
   9. Passing trailing lambdas i.e ```items.fold(1) { acc, e -> acc * e }```
   10. it: implicit name of a single parameter ```ints.filter { it > 0 }```
   11. Returning a value from a lambda expression
       1. Qualified return syntax ```return@lambdaName```
       2. Value of last expression is returned automatically
   12. Underscore for unused variables
   13. Destructuring in lambdas ```map.mapValues { (key, value) -> "$value!" }```
   14. Closures. Lambda can access outer scope(lexical scope??) variables.
8. Kotlin ranges
   1. ```1..4 // equivalent of i >= 1 && i <= 4```
   2. ```4 downTo 1``` reverse order of (1)
   3. ```1 until 10``` excludes 10
9. Kotlin collections
   ![collections](https://kotlinlang.org/docs/images/collections-diagram.png)
10. 
   
