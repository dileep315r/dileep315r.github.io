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
12. 
