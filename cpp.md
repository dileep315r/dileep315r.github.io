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
18. The variable that stores the address of another variable (like foo in the previous example) is what in C++ is called a pointer.
19. Due to the ability of a pointer to directly refer to the value that it points to, a pointer has different properties when it points to a char than when it points to an int or a float. Once dereferenced, the type needs to be known. And for that, the declaration of a pointer needs to include the data type the pointer is going to point to.
20. the size in memory of a pointer depends on the platform where the program runs.
21. Note that the asterisk (*) used when declaring a pointer only means that it is a pointer (it is part of its type compound specifier), and should not be confused with the dereference operator seen a bit earlier, but which is also written with an asterisk (*). They are simply two different things represented with the same sign.
22. But anyway, simply remembering to put one asterisk per pointer is enough for most pointer users interested in declaring multiple pointers per statement.
23. After that, mypointer and myarray would be equivalent and would have very similar properties. The main difference being that mypointer can be assigned a different address, whereas myarray can never be assigned anything, and will always represent the same block of 20 elements of type int. Pointers and arrays support the same set of operations, with the same meaning for both. The main difference being that pointers can be assigned new addresses, while arrays cannot.
24. Well, in fact these brackets are a dereferencing operator known as offset operator. They dereference the variable they follow just as * does, but they also add the number between brackets to the address being dereferenced.
25. The reason is that, when adding one to a pointer, the pointer is made to point to the following element of the same type, and, therefore, the size in bytes of the type it points to is added to the pointer.
26. Remembering operator precedence rules, we can recall that postfix operators, such as increment and decrement, have higher precedence than prefix operators, such as the dereference operator (*).
27. Here p points to a variable, but points to it in a const-qualified manner, meaning that it can read the value pointed, but it cannot modify it. Note also, that the expression &y is of type int*, but this is assigned to a pointer of type const int*. This is allowed: a pointer to non-const can be implicitly converted to a pointer to const. But not the other way around! As a safety feature, pointers to const are not implicitly convertible to pointers to non-const. Pointers can be used to access a variable by its address, and this access may include modifying the value pointed. But it is also possible to declare pointers that can access the pointed value to read it, but not to modify it. These pointers point to constant content they cannot modify, but they are not constant themselves: i.e., the pointers can still be incremented or assigned different addresses, although they cannot modify the content they point to.
28. And this is where a second dimension to constness is added to pointers: Pointers can also be themselves const. And this is specified by appending const to the pointed type (after the asterisk)
29. To add a little bit more confusion to the syntax of const with pointers, the const qualifier can either precede or follow the pointed type, with the exact same meaning:
30. String literals are arrays of the proper array type to contain all its characters plus the terminating null-character, with each of the elements being of type const char (as literals, they can never be modified).
31. C++ allows the use of pointers that point to pointers, that these, in its turn, point to data (or even to other pointers). The syntax simply requires an asterisk (*) for each level of indirection in the declaration of the pointer:
32. The void type of pointer is a special type of pointer. In C++, void represents the absence of type. Therefore, void pointers are pointers that point to a value that has no type (and thus also an undetermined length and undetermined dereferencing properties).
33. This gives void pointers a great flexibility, by being able to point to any data type, from an integer value or a float to a string of characters. In exchange, they have a great limitation: the data pointed to by them cannot be directly dereferenced (which is logical, since we have no type to dereference to), and for that reason, any address in a void pointer needs to be transformed into some other pointer type that points to a concrete data type before being dereferenced. One of its possible uses may be to pass generic parameters to a function.
34. But pointers can actually point to any address, including addresses that do not refer to any valid element. Typical examples of this are uninitialized pointers and pointers to nonexistent elements of an array. Accessing such a pointer causes undefined behavior, ranging from an error during runtime to accessing some random value.
35. But, sometimes, a pointer really needs to explicitly point to nowhere, and not just an invalid address. For such cases, there exists a special value that any pointer type can take: the null pointer value. This value can be expressed in C++ in two ways: either with an integer value of zero, or with the nullptr keyword:
36. Here, both p and q are null pointers, meaning that they explicitly point to nowhere, and they both actually compare equal: all null pointers compare equal to other null pointers. It is also quite usual to see the defined constant NULL be used in older code to refer to the null pointer value:
37. NULL is defined in several headers of the standard library, and is defined as an alias of some null pointer constant value (such as 0 or nullptr)
C++ allows operations with pointers to functions. The typical use of this is for passing a function as an argument to another function. Pointers to functions are declared with the same syntax as a regular function declaration, except that the name of the function is enclosed between parentheses () and an asterisk (*) is inserted before the name.
    ```
    // pointer to functions
    #include <iostream>
    using namespace std;
    
    int addition (int a, int b)
    { return (a+b); }
    
    int subtraction (int a, int b)
    { return (a-b); }
    
    int operation (int x, int y, int (*functocall)(int,int))
    {
      int g;
      g = (*functocall)(x,y);
      return (g);
    }
    
    int main ()
    {
      int m,n;
      int (*minus)(int,int) = subtraction;
    
      m = operation (7, 5, addition);
      n = operation (20, m, minus);
      cout <<n;
      return 0;
    }
    ```
38. For example, when the memory needed depends on user input. On these cases, programs need to dynamically allocate memory, for which the C++ language integrates the operators new and delete.
39. ```pointer = new type [number_of_elements]``` allocates block of elemenmts.
40. There is a substantial difference between declaring a normal array and allocating dynamic memory for a block of memory using new. The most important difference is that the size of a regular array needs to be a constant expression, and thus its size has to be determined at the moment of designing the program, before it is run, whereas the dynamic memory allocation performed by new allows to assign memory during runtime using any variable value as size.
41. The other method is known as nothrow, and what happens when it is used is that when a memory allocation fails, instead of throwing a bad_alloc exception or terminating the program, the pointer returned by new is a null pointer, and the program continues its execution normally.
42. The value passed as argument to delete shall be either a pointer to a memory block previously allocated with new, or a null pointer (in the case of a null pointer, delete produces no effect).
43. Supports struct type. Syntax given below. Strcture is a value type unlike arrays which is a pointer type.
    ```
    struct type_name {
    member_type1 member_name1;
    member_type2 member_name2;
    member_type3 member_name3;
    .
    .
    } object_names;
    ```
45. The arrow operator (->) is a dereference operator that is used exclusively with pointers to objects that have members. This operator serves to access the member of an object directly from its address.
46. Both aliases defined with typedef and aliases defined with using are semantically equivalent. The only difference being that typedef has certain limitations in the realm of templates that using has not. Therefore, using is more generic, although typedef has a longer history and is probably more common in existing code.
47. Type aliases can be used to reduce the length of long or confusing type names, but they are most useful as tools to abstract programs from the underlying types they use. For example, by using an alias of int to refer to a particular kind of parameter instead of using int directly, it allows for the type to be easily replaced by long (or some other type) in a later version, without having to change every instance where it is used.
48. Unions allow one portion of memory to be accessed as different data types. Its declaration and use is similar to the one of structures, but its functionality is totally different. This creates a new union type, identified by type_name, in which all its member elements occupy the same physical space in memory. 
    ```
        union type_name {
          member_type1 member_name1;
          member_type2 member_name2;
          member_type3 member_name3;
          .
          .
        } object_names;
    ```
 49.  The size of this type is the one of the largest member element. Each of these members is of a different data type. But since all of them are referring to the same location in memory, the modification of one of the members will affect the value of all of them. It is not possible to store different values in them in a way that each is independent of the others. One of the uses of a union is to be able to access a value either in its entirety or as an array or structure of smaller elements.
    ```
         union mix_t {
          int l;
          struct {
            short hi;
            short lo;
            } s;
          char c[4];
        
        } mix;
   ```
 51.  The exact alignment and order of the members of a union in memory depends on the system, with the possibility of creating portability issues.
 52.  When unions are members of a class (or structure), they can be declared with no name. In this case, they become anonymous unions, and its members are directly accessible from objects by their member names. For example, see the differences between these two structure declarations:
53. Two different enums in C++. enum type and enum class(or struct) types. Later tyoe creates real enums.
54. But, in C++, it is possible to create real enum types that are neither implicitly convertible to int and that neither have enumerator values of type int, but of the enum type itself, thus preserving type safety.
54. Classes allow programming using object-oriented paradigms: Data and functions are both members of the object
55. In order to avoid that, a class can include a special function called its constructor, which is automatically called whenever a new object of this class is created, allowing the class to initialize member variables or allocate storage.
56. Constructors cannot be called explicitly as if they were regular member functions. They are only executed once, when a new object of that class is created.
57. The default constructor is the constructor that takes no parameters, and it is special because it is called when an object is declared but is not initialized with any arguments. In the example above, the default constructor is called for rectb. Note how rectb is not even constructed with an empty set of parentheses - in fact, empty parentheses cannot be used to call the default constructor:
58. First, constructors with a single parameter can be called using the variable initialization syntax (an equal sign followed by the argument). ```class_name object_name = initialization_value;```
59. More recently, C++ introduced the possibility of constructors to be called using uniform initialization, which essentially is the same as the functional form, but using braces ({}) instead of parentheses (())
60. An advantage of uniform initialization over functional form is that, unlike parentheses, braces cannot be confused with function declarations, and thus can be used to explicitly call default constructors:
61. When a constructor is used to initialize other members, these other members can be initialized directly, without resorting to statements in its body. This is done by inserting, before the constructor's body, a colon (:) and a list of initializations for class members. For example, consider a class with the following declaration:
    1. ```Rectangle::Rectangle (int x, int y) : width(x), height(y) { }```
    2. For members of fundamental types, it makes no difference which of the ways above the constructor is defined, because they are not initialized by default, but for member objects (those whose type is a class), if they are not initialized after the colon, they are default-constructed.
62. Default-constructing all members of a class may or may always not be convenient: in some cases, this is a waste (when the member is then reinitialized otherwise in the constructor), but in some other cases, default-construction is not even possible (when the class does not have a default constructor). In these cases, members shall be initialized in the member initialization list.
63. In this example, class Cylinder has a member object whose type is another class (base's type is Circle). Because objects of class Circle can only be constructed with a parameter, Cylinder's constructor needs to call base's constructor, and the only way to do this is in the member initializer list.
64. Classes can be defined not only with keyword class, but also with keywords struct and union.
65. The keyword struct, generally used to declare plain data structures, can also be used to declare classes that have member functions, with the same syntax as with keyword class. The only difference between both is that members of classes declared with the keyword struct have public access by default, while members of classes declared with the keyword class have private access by default. For all other purposes both keywords are equivalent in this context.
66. Conversely, the concept of unions is different from that of classes declared with struct and class, since unions only store one data member at a time, but nevertheless they are also classes and can thus also hold member functions. The default access in union classes is public.
67. Operators are overloaded by means of operator functions, which are regular functions with special names: their name begins by the operator keyword followed by the operator sign that is overloaded. The syntax is: ```type operator sign (parameters) { /*... body ...*/ }```
68. A reference type is a type that acts as an alias, or an alternative name, for another variable. It’s denoted by the & symbol. Once a reference is created, it cannot be later made to reference another object; it cannot be reseated. This is often done at the time of variable declaration.
69. Notice that some operators may be overloaded in two forms: either as a member function or as a non-member function
70. The keyword this represents a pointer to the object whose member function is being executed.
71. A static data member of a class is also known as a "class variable", because there is only one common variable for all the objects of that same class, sharing the same value: i.e., its value is not different from one object of this class to another.
72. In fact, static members have the same properties as non-member variables but they enjoy class scope. For that reason, and to avoid them to be declared several times, they cannot be initialized directly in the class, but need to be initialized somewhere outside it. As in the previous example: ```int Dummy::n=0;```
73. Because it is a common variable value for all the objects of the same class, it can be referred to as a member of any object of that class or even directly by the class name ```cout << a.n;cout << Dummy::n;```
74. Classes can also have static member functions. These represent the same: members of a class that are common to all object of that class, acting exactly as non-member functions but being accessed like members of the class. Because they are like non-member functions, they cannot access non-static members of the class (neither member variables nor member functions). They neither can use the keyword this.
75. Therefore, const references provide functionality similar to passing arguments by value, but with an increased efficiency for parameters of large types. That is why they are extremely popular in C++ for arguments of compound types. Note though, that for most fundamental types, there is no noticeable difference in efficiency, and in some cases, const references may even be less efficient!
76. Several string literals can be concatenated to form a single string literal simply by separating them by one or more blank spaces, including tabs, newlines, and other valid blank characters.
77. All the character literals and string literals described above are made of characters of type char. A different character type can be specified by using one of the following prefixes
78. In raw strings, backslashes and single and double quotes are all valid characters; the content of the literal is delimited by an initial R"sequence( and a final )sequence", where sequence is any sequence of characters (including an empty sequence). The content of the string is what lies inside the parenthesis, ignoring the delimiting sequence itself.  ```R"&%$(string with \backslash)&%$"```
79. On the flip side, functions with reference parameters are generally perceived as functions that modify the arguments passed, because that is why reference parameters are actually for.
80. Therefore, const references provide functionality similar to passing arguments by value, but with an increased efficiency for parameters of large types. That is why they are extremely popular in C++ for arguments of compound types. Note though, that for most fundamental types, there is no noticeable difference in efficiency, and in some cases, const references may even be less efficient!
81. But not the other way around! As a safety feature, pointers to const are not implicitly convertible to pointers to non-const.
82. The access to its data members from outside the class is restricted to read-only, as if all its data members were const for those accessing them from outside the class. Note though, that the constructor is still called and is allowed to initialize and modify these data members:
83. Member functions specified to be const cannot modify non-static data members nor call other non-const member functions. In essence, const members shall not modify the state of an object. ```int get() const {return x;}```
84. const objects are limited to access only member functions marked as const, but non-const objects are not restricted and thus can access both const and non-const member functions alike.
85. You may think that anyway you are seldom going to declare const objects, and thus marking all members that don't modify the object as const is not worth the effort, but const objects are actually very common. Most functions taking classes as parameters actually take them by const reference, and thus, these functions can only access their const members:
86. When an object of a class is qualified as a const object ```const MyClass myobject;``` The access to its data members from outside the class is restricted to read-only, as if all its data members were const for those accessing them from outside the class. Note though, that the constructor is still called and is allowed to initialize and modify these data members:
87. Member functions can be overloaded on their constness: i.e., a class may have two member functions with identical signatures except that one is const and the other is not: in this case, the const version is called only when the object is itself const, and the non-const version is called when the object is itself non-const.
88. Just like we can create function templates, we can also create class templates, allowing classes to have members that use template parameters as types. For example. Confused by so many T's? There are three T's in this declaration: The first one is the template parameter. The second T refers to the type returned by the function. And the third T (the one between angle brackets) is also a requirement: It specifies that this function's template parameter is also the class template parameter.
    ```
     // class templates
    #include <iostream>
    using namespace std;
    
    template <class T>
    class mypair {
        T a, b;
      public:
        mypair (T first, T second)
          {a=first; b=second;}
        T getmax ();
    };
    
    template <class T>
    T mypair<T>::getmax ()
    {
      T retval;
      retval = a>b? a : b;
      return retval;
    }
    
    int main () {
      mypair <int> myobject (100, 75);
      cout << myobject.getmax();
      return 0;
    }
```
89. Template specialization. For example, let's suppose that we have a very simple class called mycontainer that can store one element of any type and that has just one member function called increase, which increases its value. But we find that when it stores an element of type char it would be more convenient to have a completely different implementation with a function member uppercase, so we decide to declare a class template specialization for that type:
90. Special member functions are member functions that are implicitly defined as member of classes under certain circumstances.
    1. Default constructor
    2. Destructor
    3. Copy constructor
    4. Copy assignment
    5. Move constructor
    6. Move assignment
91. But as soon as a class has some constructor taking any number of parameters explicitly declared, the compiler no longer provides an implicit default constructor, and no longer allows the declaration of new objects of that class without arguments.
92. Destructors fulfill the opposite functionality of constructors: They are responsible for the necessary cleanup needed by a class when its lifetime ends. The classes we have defined in previous chapters did not allocate any resource and thus did not really require any clean up.
93. The destructor for an object is called at the end of its lifetime; in the case of foo and bar this happens at the end of function main.
94. A copy constructor is a constructor whose first parameter is of type reference to the class itself (possibly const qualified) and which can be invoked with a single argument of this type. This default copy constructor may suit the needs of many classes.
95. Copy assignment
    ```
     MyClass foo;
    MyClass bar (foo);       // object initialization: copy constructor called
    MyClass baz = foo;       // object initialization: copy constructor called
    foo = bar;               // object already initialized: copy assignment called 
    ```
96. The copy assignment operator is an overload of operator= which takes a value or reference of the class itself as parameter. The return value is generally a reference to *this (although this is not required). For example, for a class MyClass, the copy assignment may have the following signature: ```MyClass& operator= (const MyClass&);```
97. The copy assignment operator is also a special function and is also defined implicitly if a class has no custom copy nor move assignments (nor move constructor) defined.
98. Unnamed objects are objects that are temporary in nature, and thus haven't even been given a name. Typical examples of unnamed objects are return values of functions or type-casts.
99. Using the value of a temporary object such as these to initialize another object or to assign its value, does not really require a copy: the object is never going to be used for anything else, and thus, its value can be moved into the destination object. These cases trigger the move constructor and move assignments:
100. The move constructor is called when an object is initialized on construction using an unnamed temporary. Likewise, the move assignment is called when an object is assigned the value of an unnamed temporary:
101. The move constructor and move assignment are members that take a parameter of type rvalue reference to the class itself. An rvalue reference is specified by following the type with two ampersands (&&). As a parameter, an rvalue reference matches arguments of temporaries of this type.
102. The concept of moving is most useful for objects that manage the storage they use, such as objects that allocate storage with new and delete. In such objects, copying and moving are really different operations:
    - Copying from A to B means that new memory is allocated to B and then the entire content of A is copied to this new memory allocated for B.
    - Moving from A to B means that the memory already allocated to A is transferred to B without allocating any new storage. It involves simply copying the pointer.
103. Compilers already optimize many cases that formally require a move-construction call in what is known as Return Value Optimization. Most notably, when the value returned by a function is used to initialize an object. In these cases, the move constructor may actually never get called.
104. n principle, private and protected members of a class cannot be accessed from outside the same class in which they are declared. However, this rule does not apply to "friends".
105. Friends are functions or classes declared with the friend keyword.
106. The duplicate function is a friend of class Rectangle. Therefore, function duplicate is able to access the members width and height (which are private) of different objects of type Rectangle. Notice though that neither in the declaration of duplicate nor in its later use in main, function duplicate is considered a member of class Rectangle. It isn't! It simply has access to its private and protected members without being a member.
107. A non-member function can access the private and protected members of a class if it is declared a friend of that class. That is done by including a declaration of this external function within the class, and preceding it with the keyword friend:
108. Typical use cases of friend functions are operations that are conducted between two different classes accessing private or protected members of both.
109. Similar to friend functions, a friend class is a class whose members have access to the private or protected members of another class:
110. Friendships are never corresponded unless specified: In our example, Rectangle is considered a friend class by Square, but Square is not considered a friend by Rectangle. Therefore, the member functions of Rectangle can access the protected and private members of Square but not the other way around. Of course, Square could also be declared friend of Rectangle, if needed, granting such an access.
111. Another property of friendships is that they are not transitive: The friend of a friend is not considered a friend unless explicitly specified.
112. Classes in C++ can be extended, creating new classes which retain characteristics of the base class. This process, known as inheritance, involves a base class and a derived class: The derived class inherits the members of the base class, on top of which it can add its own members.
113. Classes that are derived from others inherit all the accessible members of the base class. That means that if a base class includes a member A and we derive a class from it with another member called B, the derived class will contain both member A and member B.
114. This public keyword after the colon (:) denotes the most accessible level the members inherited from the class that follows it (in this case Polygon) will have from the derived class (in this case Rectangle). Since public is the most accessible level, by specifying this keyword the derived class will inherit all the members with the same levels they had in the base class.
115. With protected, all public members of the base class are inherited as protected in the derived class. Conversely, if the most restricting access level is specified (private), all the base class members are inherited as private.
116. If no access level is specified for the inheritance, the compiler assumes private for classes declared with keyword class and public for those declared with struct.
117. Even though access to the constructors and destructor of the base class is not inherited as such, they are automatically called by the constructors and destructor of the derived class.
118. Unless otherwise specified, the constructors of a derived class calls the default constructor of its base classes (i.e., the constructor taking no arguments). Calling a different constructor of a base class is possible, using the same syntax used to initialize member variables in the initialization list: ```derived_constructor_name (parameters) : base_constructor_name (parameters) {...}```
119. Unless otherwise specified, the constructors of a derived class calls the default constructor of its base classes (i.e., the constructor taking no arguments). Calling a different constructor of a base class is possible, using the same syntax used to initialize member variables in the initialization list:
120. A class may inherit from more than one class by simply specifying more base classes, separated by commas, in the list of a class's base classes (i.e., after the colon).
121. Multiple inheritance is supported.
122. A virtual member is a member function that can be redefined in a derived class, while preserving its calling properties through references. The syntax for a function to become virtual is to precede its declaration with the virtual keyword:
123. The member function area has been declared as virtual in the base class because it is later redefined in each of the derived classes. Non-virtual members can also be redefined in derived classes, but non-virtual members of derived classes cannot be accessed through a reference of the base class: i.e., if virtual is removed from the declaration of area in the example above, all three calls to area would return zero, because in all cases, the version of the base class would have been called instead.
124. A class that declares or inherits a virtual function is called a polymorphic class.
125. Abstract base classes are something very similar to the Polygon class in the previous example. They are classes that can only be used as base classes, and thus are allowed to have virtual member functions without definition (known as pure virtual functions). The syntax is to replace their definition by =0 (an equal sign and a zero):
126. Notice that area has no definition; this has been replaced by =0, which makes it a pure virtual function. Classes that contain at least one pure virtual function are known as abstract base classes.
127. But an abstract base class is not totally useless. It can be used to create pointers to it, and take advantage of all its polymorphic abilities.
128. On a function call, C++ allows one implicit conversion to happen for each argument.
129. Some of these conversions may imply a loss of precision, which the compiler can signal with a warning. This warning can be avoided with an explicit conversion.
130. Unrestricted explicit type-casting allows to convert any pointer into any other pointer type, independently of the types they point to. The subsequent call to member result will produce either a run-time error or some other unexpected results.
131. If an ellipsis (...) is used as the parameter of catch, that handler will catch any exception no matter what the type of the exception thrown. This can be used as a default handler that catches all exceptions not caught by other handlers:
132. Preprocessor directives are lines included in the code of programs preceded by a hash sign (#). These lines are not program statements but directives for the preprocessor. The preprocessor examines the code before actual compilation of code begins and resolves all these directives before any code is actually generated by regular statements.
133. The preprocessor does not understand C++ proper, it simply replaces any occurrence of identifier by replacement.
134. #define can work also with parameters to define function macros: ```#define getmax(a,b) a>b?a:b ```
135. Defined macros are not affected by block structure. A macro lasts until it is undefined with the #undef preprocessor directive:
136. Conditional inclusions (#ifdef, #ifndef, #if, #endif, #else and #elif): These directives allow to include or discard part of the code of a program if a certain condition is met.
137. The syntax used in the second #include uses quotes, and includes a file. The file is searched for in an implementation-defined manner, which generally includes the current path. In the case that the file is not found, the compiler interprets the directive as a header inclusion, just as if the quotes ("") were replaced by angle-brackets (<>).
138. 



