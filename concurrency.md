#### Double-checked locking pattern might not work
https://www.modernescpp.com/index.php/thread-safe-initialization-of-data
```
    var obj: MyClass = null
    
    fun getInstance() {
        if (obj == null) {
            mutex.lock()
            if (obj != null) obj = MyClass()
            mutex.unlock()
        }
        
        return obj
    }
```
Above code doesn't work since there are three steps in the object initialisation line
1. Allocate memory for MyClass 
2. Create the MyClass object in the memory 
3. Let instance refer to the MyClass object

Compiler might execute in 1,3,2 order. The other thread might get/use partially initialized object.
