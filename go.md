### Go quickstart guide
1. Good quick start guide https://learnxinyminutes.com/docs/go/
    ```
    // Arrays have value semantics.
    a4_cpy := a4            // a4_cpy is a copy of a4, two separate instances.
    a4_cpy[0] = 25          // Only a4_cpy is changed, a4 stays the same.
    fmt.Println(a4_cpy[0] == a4[0]) // false
    // The type [n]T is an array of n values of type T.
    primes := [6]int{2, 3, 5, 7, 11, 13}
    fmt.Println(primes)
    
    // An array has a fixed size. A slice, on the other hand, is a dynamically-sized. Slices are like references to arrays.
    // The type []T is a slice with elements of type T.
    // A slice is formed by specifying two indices, a low and high bound, separated by a colon:
    var s []int = a[low : high] // This selects a half-open range which includes the first element, but excludes the last one.
    // A slice does not store any data, it just describes a section of an underlying array.
    // Changing the elements of a slice modifies the corresponding elements of its underlying array.
    // Other slices that share the same underlying array will see those changes.
    q := []int{2, 3, 5, 7, 11, 13} // shortcut creation of implicit array and a slice pointing to it.
    // When slicing, you may omit the high or low bounds to use their defaults instead.
    // The length and capacity of a slice s can be obtained using the expressions len(s) and cap(s).
    // The capacity of a slice is the number of elements in the underlying array
    // You can extend a slice's length by re-slicing it, provided it has sufficient capacity.
    s = s[:4]
    s = s[2:]
    // The zero value of a slice is nil.
    // Slices can be created with the built-in make function
    s4 := make([]int, 4)    // Allocates slice of 4 ints, initialized to all 0.
    //  Slices (as well as maps and channels) have reference semantics.
    s3 := []int{4, 5, 9}    // Compare to a5. No ellipsis here.
    var d2 [][]float64      // Declaration only, nothing allocated here.
    bs := []byte("a slice") // Type conversion syntax.
    // Because they are dynamic, slices can be appended to on-demand.
    s = append(s, 4, 5, 6)  // Added 3 elements. Slice now has length of 6.
    // trailing ellipsis, meaning take a slice and unpack its elements
    s = append(s, []int{7, 8, 9}...)
    
    
    
    // Go is fully garbage collected. It has pointers but no pointer arithmetic.
    // You can make a mistake with a nil pointer, but not by incrementing a pointer.
    // Unlike in C/Cpp taking and returning an address of a local variable is also safe. 
    func learnMemory() (p, q *int) {
        // Named return values p and q have type pointer to int.
        p = new(int) // Built-in function new allocates memory.
        // The allocated int slice is initialized to 0, p is no longer nil.
        s := make([]int, 20) // Allocate 20 ints as a single block of memory.
        s[3] = 7             // Assign one of them.
        r := -2              // Declare another local variable.
        return &s[3], &r     // & takes the address of an object.
    }
    p, q := learnMemory() // Declares p, q to be type pointer to int.
    fmt.Println(*p, *q)   // * follows a pointer. This prints two ints.
       
    // Maps are a dynamically growable associative array type, like the
    // hash or dictionary types of some other languages.
    m := map[string]int{"three": 3, "four": 4}
    m["one"] = 1
    
    
   // Function literals are closures.
    xBig := func() bool {
        return x > 10000 // References x declared above switch statement.
    }
   
   // inline function creation and calling is supported
   fmt.Println("Add + double two numbers: ",
        func(a, b int) int {
            return (a + b) * 2
        }(10, 2)) // Called with args 10 and 2
   // functions are first class citizens. Returning function literals are supported
   
   func learnDefer() (ok bool) {
    // A defer statement pushes a function call onto a list. The list of saved
    // calls is executed AFTER the surrounding function returns.
    defer fmt.Println("deferred statements execute in reverse (LIFO) order.")
    defer fmt.Println("\nThis line is being printed first because")
    // Defer is commonly used to close a file, so the function closing the
    // file stays close to the function opening the file.
    return true
    }
   
    // Define Stringer as an interface type with one method, String.
   // Duck typing
   type Stringer interface {
   String() string
   }
   
   // Define pair as a struct with two fields, ints named x and y.
   type pair struct {
   x, y int
   }
   
   // Define a method on type pair. Pair now implements Stringer because Pair has defined all the methods in the interface.
   // Duck typing
   func (p pair) String() string { // p is called the "receiver"
   // Sprintf is another public function in package fmt.
   // Dot syntax references fields of p.
   return fmt.Sprintf("(%d, %d)", p.x, p.y)
   }
   
    // concise expression for error handling 
   // An error value communicates not just "ok" but more about the problem.
    if _, err := strconv.Atoi("non-int"); err != nil { // _ discards value
        // prints 'strconv.ParseInt: parsing "non-int": invalid syntax'
        fmt.Println(err)
    }
   
   // c is a channel, a concurrency-safe communication object.
   func inc(i int, c chan int) {
   c <- i + 1 // <- is the "send" operator when a channel appears on the left.
   }
   
   // Same make function used earlier to make a slice. Make allocates and
    // initializes slices, maps, and channels.
    c := make(chan int)
   // Start three concurrent goroutines. Numbers will be incremented
    // concurrently, perhaps in parallel if the machine is capable and
    // properly configured. All three send to the same channel.
    go inc(0, c) // go is a statement that starts a new goroutine.
    go inc(10, c)
    go inc(-805, c)
     // Select has syntax like a switch statement but each case involves
    // a channel operation. It selects a case at random out of the cases
    // that are ready to communicate.
    select {
    case i := <-c: // The value received can be assigned to a variable,
        fmt.Printf("it's a %T", i)
    case <-cs: // or the value received can be discarded.
        fmt.Println("it's a string")
    case <-ccs: // Empty channel, not ready for communication.
        fmt.Println("didn't happen.")
    }
   
   
    ```

   1. Additional concepts to learn
      1. Packages
         1. By convention, the package name is the same as the last element of the import path. For instance, the "math/rand" package comprises files that begin with the statement package rand.
         2. In Go, a name is exported if it begins with a capital letter. For example, Pizza is an exported name, as is Pi, which is exported from the math package.
      2. A var statement can be at package or function level. We see both in this example.
      3. A method is a function with a special receiver argument.
         1. The receiver appears in its own argument list between the func keyword and the method name.
         2. You can only declare a method with a receiver whose type is defined in the same package as the method. You cannot declare a method with a receiver whose type is defined in another package (which includes the built-in types such as int)
         3. Methods with pointer receivers can modify the value to which the receiver points (as Scale does here). Since methods often need to modify their receiver, pointer receivers are more common than value receivers.
         4. With a value receiver, the Scale method operates on a copy of the original Vertex value. (This is the same behavior as for any other function argument.) The Scale method must have a pointer receiver to change the Vertex value declared in the main function.
         5. while methods with pointer receivers take either a value or a pointer as the receiver when they are called:
         6. For the statement v.Scale(5), even though v is a value and not a pointer, the method with the pointer receiver is called automatically. That is, as a convenience, Go interprets the statement v.Scale(5) as (&v).Scale(5) since the Scale method has a pointer receiver.
         7. In general, all methods on a given type should have either value or pointer receivers, but not a mixture of both. (We'll see why over the next few pages.)
      4. A function can return any number of results.
      5. Types are given below
         ```
         bool

         string
      
         int  int8  int16  int32  int64
         uint uint8 uint16 uint32 uint64 uintptr
      
         byte // alias for uint8
      
         rune // alias for int32
         // represents a Unicode code point
      
         float32 float64
      
         complex64 complex128
         ```
      6. Generics
         1. ```func Index[T comparable](s []T, x T) int```
         2. ```type List[T any] struct {
                next *List[T]
                val  T
                }
            ```
      7. Pass by value and reference confusion https://david-yappeter.medium.com/golang-pass-by-value-vs-pass-by-reference-e48aac8b2716
         1. Go passes by value always (i.e. it creates a copy of the value in the function); if you pass something to a function, and that function modifies that value, the caller won't see those changes. If you want changes to propogate outside the function, you must pass a pointer. https://stackoverflow.com/questions/47296325/passing-by-reference-and-value-in-go-to-functions
         2. https://dave.cheney.net/2017/04/30/if-a-map-isnt-a-reference-variable-what-is-it
         3. C uses call by value by default. This means that when a function is called, the values of the arguments are copied into the formal parameters of the function. Any changes made to the formal parameters inside the function do not affect the original arguments.
         4. C++ has both references and pointers. In C++, a reference is a way to refer to an existing variable. It is similar to a pointer, but it is not an object in itself. A reference is simply an alias for another variable.
            1. References are declared using the & operator.
         5. Pointers in Java are often referred to as References in Java. When working with Java, the variable is a type of object that stores the reference of the object. And this reference is nothing but a pointer that provides the address of the object in the memory.
         6. Key ideas
            1. Variable is an address in the executable binary file.
            2. Assignment of variable 'a' to variable 'b', moves data at address 'b' to address 'a'. Think of it as a move instruction.
            3. Reference variable address location contains the address of the complex datatype/object. Primitive types are stored directly at the address location.
            4. Pointer variable address location contains the address of the actual object.
            5. ANSI C supports a minimum of 12 levels of pointers i.e ********a
         7. Map types are reference types, like pointers or slices, and so the value of m above is nil; it doesn’t point to an initialized map. A nil map behaves like an empty map when reading, but attempts to write to a nil map will cause a runtime panic; don’t do that. To initialize a map, use the built in make function:
         8. On the other hand, Go can be also viewed as a C language framework. This is mainly reflected from the fact that Go supports several kinds of types whose value memory structures are not totally transparent, whereas the main characteristic of C types is the memory structures of C values are transparent. Each C value in memory occupies one memory block (one continuous memory segment). However, a value of some kinds of Go types may often be hosted on ***more than one memory block***.
         9. Later, we call the parts (being distributed on different memory blocks) of a value as value parts. A value hosting on more than one memory blocks is composed of one direct value part and several underlying indirect parts which are referenced by that direct value part.
         10. https://go101.org/article/value-part.html
   2. The html/template package is part of the Go standard library. We can use html/template to keep the HTML in a separate file, allowing us to change the layout of our edit page without modifying the underlying Go code.
   3. Template caching: A better approach would be to call ParseFiles once at program initialization, parsing all templates into a single *Template. Then we can use the ExecuteTemplate method to render a specific template.
   4. The function template.Must is a convenience wrapper that panics when passed a non-nil error value, and otherwise returns the *Template unaltered. A panic is appropriate here; if the templates can't be loaded the only sensible thing to do is exit the program.
   5. The go run command will automatically recompile a Go program if the source code file is changed. This is because the go run command uses a watch file to track the modification time of the source code files. 
   6. The go build command will compile the project's code and create an executable binary.
   7. It is considered common practice that the primary or entry point file in a package is named after the name of the directory.
   8. Go does not have the concept of public, private, or protected modifiers like other languages do. External visibility is controlled by capitalization. Types, variables, functions, and so on, that start with a capital letter are available, publicly, outside the current package. A symbol that is visible outside its package is considered to be exported
   9. When Go sees that a package is named main it knows the package should be considered a binary, and should be compiled into an executable file, instead of a library designed to be used in another program.
   10. Go get: When you run this command, the go tool will look up the Cobra repository from the path you specified and determine which version of Cobra is the latest by looking at the repository’s branches and tags. It will then download that version and keep track of the one it chose by adding the module name and the version to the go.mod file for future reference.
   11. This directive tells Go which module you want, such as github.com/spf13/cobra, and the version of the module you added. Sometimes require directives will also include an // indirect comment. This comment says that, at the time the require directive was added, the module is not referenced directly in any of the module’s source files. A few additional require lines were also added to the file. These lines are other modules Cobra depends on that the Go tool determined should be referenced as well.
   12. Since Go modules are distributed from a version control repository, they can use version control features such as tags, branches, and even commits.
   13. Go module path confusion discussed here https://groups.google.com/g/golang-nuts/c/hLkhogyFLWI
       1. Go uses Minimal version selection algorithm for dependency resolution https://research.swtch.com/vgo-mvs
       2. Conceptually, MVS operates on a directed graph of modules, specified with go.mod files. Each vertex in the graph represents a module version. Each edge represents a minimum required version of a dependency, specified using a require directive. The graph may be modified by exclude and replace directives in the go.mod file(s) of the main module(s) and by replace directives in the go.work file.
       3. Go module import resolution algorithm
          1. The go command starts by searching the build list for modules with paths that are prefixes of the package path. For example, if the package example.com/a/b is imported, and the module example.com/a is in the build list, the go command will check whether example.com/a contains the package, in the directory b. At least one file with the .go extension must be present in a directory for it to be considered a package. Build constraints are not applied for this purpose. If exactly one module in the build list provides the package, that module is used. If no modules provide the package or if two or more modules provide the package, the go command reports an error. The -mod=mod flag instructs the go command to attempt to find new modules providing missing packages and to update go.mod and go.sum. The go get and go mod tidy commands do this automatically.
   14. Generics
       1. To support values of either type, that single function will need a way to declare what types it supports. Calling code, on the other hand, will need a way to specify whether it is calling with an integer or float map.
       2. To support this, you’ll write a function that declares type parameters in addition to its ordinary function parameters. These type parameters make the function generic, enabling it to work with arguments of different types. You’ll call the function with type arguments and ordinary function arguments.
       3. Each type parameter has a type constraint that acts as a kind of meta-type for the type parameter. Each type constraint specifies the permissible type arguments that calling code can use for the respective type parameter.
       4. While a type parameter’s constraint typically represents a set of types, at compile time the type parameter stands for a single type – the type provided as a type argument by the calling code. If the type argument’s type isn’t allowed by the type parameter’s constraint, the code won’t compile.
       5. Example
          ```agsl
            // SumIntsOrFloats sums the values of map m. It supports both int64 and float64
             // as types for map values.
             func SumIntsOrFloats[K comparable, V int64 | float64](m map[K]V) V {
             var s V
             for _, v := range m {
             s += v
             }
             return s
             }
          
             // Specify for the K type parameter the type constraint comparable. Intended specifically for cases like these, the comparable constraint is predeclared in Go. It allows any type whose values may be used as an operand of the comparison operators == and !=. Go requires that map keys be comparable. So declaring K as comparable is necessary so you can use K as the key in the map variable. It also ensures that calling code uses an allowable type for map keys.
             // SumIntsOrFloats[string, int64](ints)
          ```
       6. In calling the generic function you wrote, you specified type arguments that told the compiler what types to use in place of the function’s type parameters. As you’ll see in the next section, in many cases you can omit these type arguments because the compiler can infer them.
       7. In this last section, you’ll move the constraint you defined earlier into its own interface so that you can reuse it in multiple places. Declaring constraints in this way helps streamline code, such as when a constraint is more complex.
          ```
             type Number interface {
             int64 | float64
              }
          ```
       8. https://stackoverflow.com/questions/61247864/what-is-the-difference-between-type-alias-and-type-definition-in-go for types difference.   
       9. For an expression x of interface type and a type T, the primary expression x.(T) asserts that x is not nil and that the value stored in x is of type T. The notation x.(T) is called a type assertion. More precisely, if T is not an interface type, x.(T) asserts that the dynamic type of x is identical to the type T.
       10. Named and unnamed types and assignability https://stackoverflow.com/questions/19334542/why-can-i-type-alias-functions-and-use-them-without-casting/19334952#19334952
       11. When compiling a single main package, build writes the resulting executable to an output file named after the first source file ('go build ed.go rx.go' writes 'ed' or 'ed.exe') or the source code directory ('go build unix/sam' writes 'sam' or 'sam.exe'). The '.exe' suffix is added when writing a Windows executable.
   15. Go doc supports links, headings, lists. https://go.dev/doc/comment
   16. Go interfaces generally belong in the package that uses values of the interface type, not the package that implements those values. The implementing package should return concrete (usually pointer or struct) types: that way, new methods can be added to implementations without requiring extensive refactoring. See https://stackoverflow.com/questions/44346572/how-to-implement-interface-from-a-different-package-in-golang
   17. Being part of a module doesn't mean much: Modules are just sets of packages versioned together and doesn't add any additional relation between these packages. https://stackoverflow.com/questions/57806081/how-to-access-nested-modules-submodules-in-go
   18. Go program lifecycle https://stackoverflow.com/questions/52370420/go-global-variable-initialisation
       1. Package initialization—variable initialization and the invocation of init functions—happens in a single goroutine, sequentially, one package at a time. An init function may launch other goroutines, which can run concurrently with the initialization code. However, initialization always sequences the init functions: it will not invoke the next one until the previous one has returned. 
       2. Program execution begins by initializing the main package and then invoking the function main. When that function invocation returns, the program exits. It does not wait for other (non-main) goroutines to complete.
       3. Meaning the order is roughly:
          1. Global variables get initialized 
          2. init() functions run 
          3. main() runs
       4. More precisely, a package-level variable is considered ready for initialization if it is not yet initialized and either has no initialization expression or its initialization expression has no dependencies on uninitialized variables. Initialization proceeds by repeatedly initializing the next package-level variable that is earliest in declaration order and ready for initialization, until there are no variables ready for initialization.
       5. https://go.dev/ref/spec#Program_initialization_and_execution contains more details about initialisation.
       6. Dependency analysis is performed per package; only references referring to variables, functions, and (non-interface) methods declared in the current package are considered.
       7. The declaration order of variables declared in multiple files is determined by the order in which the files are presented to the compiler: Variables declared in the first file are declared before any of the variables declared in the second file, and so on.
       8. A package with no imports is initialized by assigning initial values to all its package-level variables followed by calling all init functions in the order they appear in the source, possibly in multiple files, as presented to the compiler. 
       9. If a package has imports, the imported packages are initialized before initializing the package itself. If multiple packages import a package, the imported package will be initialized only once. The importing of packages, by construction, guarantees that there can be no cyclic initialization dependencies.
       10. Package initialization—variable initialization and the invocation of init functions—happens in a single goroutine, sequentially, one package at a time. An init function may launch other goroutines, which can run concurrently with the initialization code. However, initialization always sequences the init functions: it will not invoke the next one until the previous one has returned.
       11. To ensure reproducible initialization behavior, build systems are encouraged to present multiple files belonging to the same package in lexical file name order to a compiler.
       12. A complete program is created by linking a single, unimported package called the main package with all the packages it imports, transitively. The main package must have package name main and declare a function main that takes no arguments and returns no value.
       13. Program execution begins by initializing the main package and then invoking the function main. When that function invocation returns, the program exits. It does not wait for other (non-main) goroutines to complete.
   14. See https://go.dev/ref/spec#Comparison_operators for comparison operator semantics.