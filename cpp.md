### C++
1. When the variables in the example above are declared, they have an undetermined value until they are assigned a value for the first time.
2. Initialization types
    a. C-like: ```type identifier = initial_value;```
    b. constructor initialization: ```type identifier (initial_value);```
    c. uniform initialization: ```type identifier {initial_value};```
3. auto and decltype are powerful features recently added to the language. But the type deduction features they introduce are meant to be used either when the type cannot be obtained by other means or when using it improves code readability.
4. The string class is a compound type.
5. The types described above (characters, integers, floating-point, and boolean) are collectively known as arithmetic types. But two additional fundamental types exist: void, which identifies the lack of type; and the type nullptr, which is a special type of pointer.
6. Note that the #define lines are preprocessor directives, and as such are single-line instructions that -unlike C++ statements- do not require semicolons (;) at the end; the directive extends automatically until the end of the line.
7. The comma operator (,) is used to separate two or more expressions that are included where only one expression is expected. When the set of expressions has to be evaluated for a value, only the right-most expression is considered.
8. The value returned by sizeof operator is a compile-time constant, so it is always determined before program execution.
9. C++ uses a convenient abstraction called streams to perform input and output operations in sequential media such as the screen, the keyboard or a file. A stream is an entity where a program can either insert or extract characters to/from. There is no need to know details about the media associated to the stream or any of its internal specifications. All we need to know is that streams are a source/destination of characters, and that these characters are provided/accepted sequentially (i.e., one after another).
    1. Standard streams cin, cout, cerr, clog
    2. stringstream is useful
10. goto allows to make an absolute jump to another point in the program. This unconditional jump ignores nesting levels, and does not cause any automatic stack unwinding. Therefore, it is a feature to use with care, and preferably within the same block of statements, especially in the presence of local variables.
11. The for-loop has another syntax, which is used exclusively with ranges: ```for ( declaration : range ) statement;```
12. Scopes
    1. Local scope
    2. Global scope
    3. Namespace scope
       1. Namespaces can be split: Two segments of a code can be declared in the same namespace i.e namespace doesn't need to be defined at a single place. You can define partial namespace at one place and another part at another place.
       2. Namespaces can even extend across different translation units (i.e., across different files of source code).
       3. The keyword using introduces a name into the current declarative region (such as a block), thus avoiding the need to qualify the name.
       4. using and using namespace have validity only in the same block in which they are stated or in the entire source code file if they are used directly in the global scope.
       5. All the entities (variables, types, constants, and functions) of the standard C++ library are declared within the std namespace.
       6. Many programmers prefer to qualify each of the elements of the standard library used in their programs.
       7. The storage for variables with global or namespace scope is allocated for the entire duration of the program. This is known as static storage, and it contrasts with the storage for local variables (those declared within a block).
       8. The storage for variables with global or namespace scope is allocated for the entire duration of the program. This is known as static storage, and it contrasts with the storage for local variables (those declared within a block). These use what is known as automatic storage. The storage for local variables is only available during the block in which they are declared; after that, that same storage may be used for a local variable of some other function, or used otherwise.
13. In a way, passing an array as argument always loses a dimension. The reason behind is that, for historical reasons, arrays cannot be directly copied, and thus what is really passed is a pointer. Array in cpp is a pointer type. Int is a value type.
14. Containers are a library feature that falls out of the scope of this tutorial, and thus the class will not be explained in detail here. Suffice it to say that they operate in a similar way to built-in arrays, except that they allow being copied (an actually expensive operation that copies the entire block of memory, and thus to use with care) and decay into pointers only when explicitly told to do so (by means of its member data).
15. In fact, because string literals are regular arrays, they have the same restrictions as these, and cannot be assigned values.
16. In C++, even though the standard library defines a specific type for strings (class string), still, plain arrays with null-terminated sequences of characters (C-strings) are a natural way of representing strings in the language; in fact, string literals still always produce null-terminated character sequences, and not string objects.
17. This is due to the fact that strings have a dynamic size determined during runtime, while the size of arrays is determined on compilation, before the program runs.
18. 
