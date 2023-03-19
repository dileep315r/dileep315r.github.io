Good interview questions 2023

1. Tail recursion implementation of the Fibonacci numbers
    ```
    fun myFunc(n: Int, first: Int = 0, second: Int = 1): Int {
       if(n == 0) {
           return first
       } else if (n == 1) {
           return second
       } else {
           return myFunc(n - 1, second, first + second)
       }
    }
    ```
2. Make a class immutable
      ```
        Class Person {


             Int age;


             Array&lt;String> places;


        }


        Hint: Use final keyword
      ```

3. Exactly once message processing
    1. Payment processor communicating with the payment service provider backend.
4. Improve the following code java
    ```
        Public SimpleCache {


            HashMap&lt;Long, UserStatistics> map = HashMap&lt;>()


             Fun getOrCreate(long id) {


                  UserStatistics result = map.get(New Long(id));


                  If (result == null) {


                       result = UserStatistics.calculate(id)


                       map.put(new Long(id), result)


                  }


         


                  Return result


             }


        }
    ```
   1. Id: variable name
   2. Long(id) is not required as Java has autoboxing feature
   3. Cache eviction strategy
   4. Cache more memory
   5. Concurrency with the cache
   6. Map modify  the type to Map
   7. Use ConcurrentHashMap computeIfAbsent function.
   8. Make the code generic
   9. Implement without using concurrentHashMap
      ```
                         Final code:

                         Public UserStatisticsCache&lt;K, V> {

                              Map&lt;K, V> map = ConcurrentHashMap&lt;K, V>

                              Function&lt;K, V> func

                              Public UserStatisticsCache(Function&lt;K, V> func) {

              This.func = func

                              }

                              Public V getOrCreate(K key) {

              Return map.computeIfAbsent(key, func)

              }

                         }
      ```

5. [https://softwareengineering.stackexchange.com/questions/280324/is-it-better-to-make-database-calls-or-external-api-calls-first-in-the-context-o](https://softwareengineering.stackexchange.com/questions/280324/is-it-better-to-make-database-calls-or-external-api-calls-first-in-the-context-o)
Similar scenario: Write to the cache first or write to the database first.
6. SubArray sum whose sum is equal to the given sum [https://www.geeksforgeeks.org/find-subarray-with-given-sum-in-array-of-integers/](https://www.geeksforgeeks.org/find-subarray-with-given-sum-in-array-of-integers/)
7. Given list of File(name, size, tag). Implement two operations
   1. Find the total size of the files
   2. Find top(k) tags by size of the file
8. O(1) operations data structure
   1. [https://stackoverflow.com/questions/5682218/data-structure-insert-remove-contains-get-random-element-all-at-o1](https://stackoverflow.com/questions/5682218/data-structure-insert-remove-contains-get-random-element-all-at-o1)



Own composition
1. Find a strategy to return the results in pagination from a datastore, such that you return the snapshot of the data rather than considering the updated values. [Inspired from Elastic search scroll implementation] Follow up, how would you tackle the case of client existing without reading through all the elements. How do you manage space efficiently.  Add compaction and deletion of old records to the mix.
2. Chunked updates or bulky updates to the database? from the database performance perspective and application performance perspective.
3. Chunked reads or bulk reads? from the database performance perspective and application performance perspective.
4. 