Database transactions
1. Read committed 
   1. No dirty read
   2. Non repeatable read problem and write conflict problem(or skewed read/skewed write problem)
   3. Write requires exclusive lock
2. Repeatable read
   - Maintain multiple versions of the data items
   - Rollback the transaction if later transactions have committed
   - Optimistic concurrency control
   - Cleanup the unused write items in the background
   - Snapshot isolation
3. Skewed write problem
4. Phantom read
   1. Meeting room booking problem 
   2. Solutions
      1. Materialize the conflicts
      2. Explicit locking → select for update
      3. Predicate locks
      4. Index locks
      5. Table level locking
      6. Index locks, predicate locking
5. Strict serializable isolation level
   - Pessimistic control locks
   - Optimistic control, MVCC
