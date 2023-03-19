Hack lang learning notes:
1. Hack is statically typed, object oriented and has great supportfordeveloping websites.
2. Hack arrays: vec, dict, keyset  Hack Collections: Vector, Map, Set
3. PHP arrays: array, varray, darray
4. https://fburl.com/hack-arrays-cheat-sheet
5. Hack arrays have value semantics. Means what?
6. Async feature similar to kotlin coroutines


PHP learning notes(https://www.php.net/manual/en/langref.php)
7. To check the type and value of an expression, use the var_dump() function. To get a human-readable representation of a type for debugging, use the gettype() function. To check for a certain type, do not use gettype(), but rather the is_type functions.
8. To forcibly convert a variable to a certain type, either cast the variable or use the settype() function on it.
9. PHP requires instructions to be terminated with a semicolon at the end of each statement.
10. PHP treats objects in the same way as references or handles, meaning that each variable contains an object reference rather than a copy of the entire object. See Objects and References
11. An array in PHP is actually an ordered map. A map is a type that associates values to keys. This type is optimized for several different uses; it can be treated as an array, list (vector), hash table (an implementation of a map), dictionary, collection, stack, queue, and probably more. As array values can be other arrays, trees and multidimensional arrays are also possible.
1. The key can either be an int or a string. The value can be of any type.
2. Additionally the following key casts will occur
3. If multiple elements in the array declaration use the same key, only the last one will be used as all others are overwritten.
4. Arrays can be destructured using the [] (as of PHP 7.1.0) or list() language constructs. These constructs can be used to destructure an array into distinct variables.
5. More examples at https://www.php.net/manual/en/language.types.array.php
12. Variable without $ sign at the beginning represents a constant
13. Iterable is very similar to ruby enumerable type.  Traversable is the interface. Iterable is a pseudo-type introduced in PHP 7.1. It accepts any array or object implementing the Traversable interface. Both of these types are iterable using foreach and can be used with yield from within a generator.
14.  Enumerations are a restricting layer on top of classes and class constants, intended to provide a way to define a closed set of possible values for a type.
15. A resource is a special variable, holding a reference to an external resource. Resources are created and used by special functions.
16. The special null value represents a variable with no value.
17. Type declarations can be added to function arguments, return values, and, as of PHP 7.4.0, class properties. They ensure that the value is of the specified type at call time, otherwise a TypeError is thrown.
18. Variables in PHP are represented by a dollar sign followed by the name of the variable. The variable name is case-sensitive.
1. By default, variables are always assigned by value. That is to say, when you assign an expression to a variable, the entire value of the original expression is copied into the destination variable.
2. To assign by reference, simply prepend an ampersand (&) to the beginning of the variable which is being assigned (the source variable).
3. PHP provides a large number of predefined variables to any script which it runs.
4. The scope of a variable is the context within which it is defined. For the most part all PHP variables only have a single scope. This single scope spans included and required files as well.
5. However, within user-defined functions a local function scope is introduced. Any variable used inside a function is by default limited to the local function scope.
6. Another important feature of variable scoping is the static variable. A static variable exists only in a local function scope, but it does not lose its value when program execution leaves this scope.
7. Sometimes it is convenient to be able to have variable variable names. That is, a variable name which can be set and used dynamically.
    1. At this point two variables have been defined and stored in the PHP symbol tree: $a with contents "hello" and $hello with contents "world".
19.  Constants predefined constants like __FILE__ similar to ruby predefined
20. Operators are very similar to ruby operators. Examples
1. ** exponentiation
2. -= type assignment expressions
3. === comparison operator
4. ^, & bitwise operator
5. `` command line execution operator
6. ++ and – operators are available
7. There are two string operators. The first is the concatenation operator ('.'), which returns the concatenation of its right and left arguments. The second is the concatenating assignment operator ('.='), which appends the argument on the right side to the argument on the left side.
8. Instanceof type operator
9. Ternary operator
21. A statement can be an assignment, a function call, a loop, a conditional statement or even a statement that does nothing (an empty statement). Statements usually end with a semicolon. In addition, statements can be grouped into a statement-group by encapsulating a group of statements with curly braces. A statement-group is a statement by itself as well. The various statement types are described in this chapter.
1. The following are also considered language constructs even though they are referenced under functions in the manual.
    1. list() array() echo eval() print
2. Elseif similar to ruby syntax
3. Alternative control structures syntax similar to python control structures syntax
4. The foreach construct provides an easy way to iterate over arrays. foreach works only on arrays and objects, and will issue an error when you try to use it on a variable with a different data type or an uninitialized variable.
5. require is identical to include except upon failure it will also produce a fatal E_COMPILE_ERROR level error.
6. The include expression includes and evaluates the specified file.
22.  Functions
1. All functions and classes in PHP have the global scope - they can be called outside a function even if they were defined inside and vice versa.
2. PHP does not support function overloading, nor is it possible to undefine or redefine previously-declared functions.
3. PHP supports the concept of variable functions. This means that if a variable name has parentheses appended to it, PHP will look for a function with the same name as whatever the variable evaluates to, and will attempt to execute it. Among other things, this can be used to implement callbacks, function tables, and so forth.
4. Anonymous functions, also known as closures, allow the creation of functions which have no specified name. They are most useful as the value of callable parameters, but they have many other uses. `function () use ($message)` syntax for closure variables. Anonymous functions may be declared statically. This prevents them from having the current class automatically bound to them. Objects may also not be bound to them at runtime.
5. Arrow functions were introduced in PHP 7.4 as a more concise syntax for anonymous functions. Arrow functions have the basic form fn (argument_list) => expr. Arrow functions support the same features as anonymous functions, except that using variables from the parent scope is always automatic.
6.  The first class callable syntax is introduced as of PHP 8.1.0, as a way of creating anonymous functions from callable. It supersedes existing callable syntax using strings and arrays. The advantage of this syntax is that it is accessible to static analysis, and uses the scope at the point where the callable is acquired.
23. Name spaces
1. In the PHP world, namespaces are designed to solve two problems that authors of libraries and applications encounter when creating re-usable code elements such as classes or functions. Namespaces are similar to modules in ruby.
2. \ is used to separate namespaces much like unix directory separator
3. https://www.php.net/manual/en/language.namespaces.basics.php
4. Can refer using fully qualified name like \A\b\c()
5. Note that to access any global class, function or constant, a fully qualified name can be used, such as \strlen() or \Exception or \INI_ALL.
24. Classes and objects(https://www.php.net/manual/en/language.oop5.php)




1. Basic class definitions begin with the keyword class, followed by a class name, followed by a pair of curly braces which enclose the definitions of the properties and methods belonging to the class.
2. Null safe expression $a?->b?->c
3. ClassName::class to get FQ class name
4. Extends keyword for inheritance
5. Class contains members and functions declared inside the braces of the class.
6. New keyword for class instantiation
7. Within class methods non-static properties may be accessed by using -> (Object Operator): $this->property (where property is the name of the property). Static properties are accessed by using the :: (Double Colon): self::$property. See Static Keyword for more information on the difference between static and non-static properties.
8. The pseudo-variable $this is available inside any class method when that method is called from within an object context. $this is the value of the calling object.
9. It is possible to define constants on a per-class basis remaining the same and unchangeable. The default visibility of class constants is public. Access them using self::CONST
10. Many developers writing object-oriented applications create one PHP source file per class definition. One of the biggest annoyances is having to write a long list of needed includes at the beginning of each script (one for each class).
11. The spl_autoload_register() function registers any number of autoloaders, enabling for classes and interfaces to be automatically loaded if they are currently not defined. By registering autoloaders, PHP is given a last chance to load the class or interface before it fails with an error.
12. PHP allows developers to declare constructor methods for classes. Classes which have a constructor method call this method on each newly-created object, so it is suitable for any initialization that the object may need before it is used.
1. __construct and __destruct methods
13. The Scope Resolution Operator (also called Paamayim Nekudotayim) or in simpler terms, the double colon, is a token that allows access to static, constant, and overridden properties or methods of a class.
1. Self::, ClassName::, parent:: based on the context
14. Object interfaces allow you to create code which specifies which methods a class must implement, without having to define how these methods are implemented. Interfaces share a namespace with classes and traits, so they may not use the same name.
1. Interface and implements are the keywords
15. Abstract functions are supported
16. PHP implements a way to reuse code called Traits. Similar to module mixins in ruby.
1. Use and Trait are the keywords
17. Anon classes similar to Java


Hack language learning notes:
1.