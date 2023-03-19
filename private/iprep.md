### One day before interview
1. Check glassdoor interview reviews before the interview. It teaches you how not to fail in the interview of a specific company.

### Ten minutes before interview
#### Things to talk about in interviews
Coding round
1. Always keep pen and paper nearby.
2. Testing using TDD for algorithmic interviews. Actively testing using the sample inputs and outputs even before the interviewer asks. Actively discuss the time and space complexity of the algorithm before the interviewer asks.
3. Identify input, output and come up with an example.
4. Identify edge cases. Clarifying questions cycles in a graph etc..
5. BigTech specific
    1. Identify input, output and come up with an example.
    2. Identify edge cases. Clarifying questions cycles in a graph etc..
    3. Ambiguous problems, variations of the problem.
    4. Design input as code
    5. Design class and solution method signature
    6. Above steps help me think clearly
    7. Solution, think out loud.
    8. Time and space complexity explanation.
    9. Code should almost compile
    10. Keep it modular and simple
    11. Demonstrate intermediate level of knowledge of the language
    12. Write unit tests if the time permits
    13. Understand, clarify, define interfaces, solution, implement and verify.
6. Small things are important in big tech companies interviews. Interviewers don’t have big data points to judge in a short span of time. Explain the smallest things with a  lot of enthusiasm. Trivial Implicit assumptions also clarify. The way of doing small things matters.
7. If you can’t find a solution. Iterate through the following data structures to solve the problem
   1. Stack
   2. Queues
   3. Heap
   4. Use hashing, binary search, merge sort/comparison for surprising optimizations.
8. Recommended to practice four to five questions before the interviews so that I do speed coding in the interviews.

#### Design round
1. Small things are important in big tech companies interviews. Interviewers don’t have big data points to judge in a short span of time. Explain the smallest things with a  lot of enthusiasm.
2. Ask for functional requirements.
3. Ask for non functional requirements. 
4. High level Object oriented design of the components. 
5. Implementation details using microservices and identifying bottlenecks and solving them. 
6. Actively discuss communication protocols like GRPC, REST. Actively discuss connections from mobile to backend and improving the response time ex. Bulk uploads parallelization in instagram. 
7. Actively discuss dashboards/monitoring/alerting infrastructure. 
8. Actively discuss fault tolerance i.e resilience framework, retry of events and fault tolerance of database components, multi region deployments. 
9. Actively discuss funnel analysis using tools like MixPanel. 
10. Discuss about data warehousing and analysis of the data. 
11. Discuss about load balancers.
12. Discuss about caching of the data. Also cost if possible. 
13. Rate limiting, blocking malicious actors. 
14. Discuss load testing, fault tolerance testing chaos monkey. 
15. Discuss consistent hashing, 2PL, proxies etc. 
16. RateLimiter in design

### Algo tips
1. Use a modulo operator for cyclic shifts.
2. Pairs are super helpful data structures to express certain algorithms compactly.
3. HashSet for a set data structure. Visited hashSet for breadth first search of graph.
   1. StringBuilder interface for string manipulation.
4. Explain implicit stack trace time as well in the space complexity.
5. Space complexity includes the input space as well.
6. Take time to understand tricky problems, remember in some interviews I moved too quickly.
7. Use stack to handle pre-order to in-order traversal conversion.
8. Use hashing, binary search, merge sort/comparison for surprising optimizations.
9. Backtracking can be defined as a general algorithmic technique that considers searching every possible combination in order to solve a computational problem. Build a solution incrementally, one piece at a time, removing those solutions that fail to satisfy the constraints of the problem at any point in time. that incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.
   1. There are three types of problems in backtracking
      1. Decision Problem – In this, we search for a feasible solution.
      2. Optimization Problem – In this, we search for the best solution.
      3. Enumeration Problem – In this, we find all feasible solutions.
   2. Backtracking can be applied only for problems which admit the concept of a "partial candidate solution" and a relatively quick test of whether it can possibly be completed to a valid solution.
   3. Backtracking is an important tool for solving [constraint satisfaction problems](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem),<sup><a href="https://en.wikipedia.org/wiki/Backtracking#cite_note-BiereHeule2009-2">[2]</a></sup> such as [crosswords](https://en.wikipedia.org/wiki/Crosswords), [verbal arithmetic](https://en.wikipedia.org/wiki/Verbal_arithmetic), [Sudoku](https://en.wikipedia.org/wiki/Algorithmics_of_sudoku), and many other puzzles.
10. Branch and bound [https://en.wikipedia.org/wiki/Branch_and_bound](https://en.wikipedia.org/wiki/Branch_and_bound). Divide the search space into subspaces and discard the subspace if the bound function on the subspace is not better than the bound seen so far, further divide the subspace otherwise.
    1. When selecting the next solution subset, use the following strategies
       1. Depth first search
       2. Breadth first search
       3. Best first search – node with best bound function value.
    2. Example problems:
       1. Traveling salesman problem
11. Left shift operator simply shifts and fills the LSB with 0 and discards MSB. Right shift operator shifts right and fills the MSB with previous sign bit for signed right shift and 0 for unsigned right shift and discards LSB.
12.  Can use enumeration of bits to simulate combinations. 4 ways, 2 bits, 4 numbers, each number ith bit 1 include ith item 0 don’t include ith item in combination.
13.  Use swapping technique to produce permutations. Swap the first item with any of the remaining n-1 items and solve for n-1 arrays recursively.
14.  Use HashMap or array for memoization in dynamic programming
15.  Even the smartest people need hints in the interview room to come up with solutions in the stipulated time. Mind is not as calm as when we work alone in the interview room, so guidance is necessary. In practice, most of the optimizations occur over time and not immediately.
16. NcK combinations, n! Permutations, and mix between n!/k!
17. Quicksort space complexity is o(logn)
18. Use sentinel node to handle edge cases in linkedList. [https://leetcode.com/problems/plus-one-linked-list/description/](https://leetcode.com/problems/plus-one-linked-list/description/) is the problem.
19. Check if the seemlingly dynamic programming problem can be solved using alternative approaches like sliding window algorithm, greedy algorithm etc..
20.  Queue for BFS and stack for DFS. Use set for remembering visited nodes.
21.  Dynamic programming, try to use lesser space for memoization. Example problem: [https://leetcode.com/problems/minimum-path-sum/editorial/](https://leetcode.com/problems/minimum-path-sum/editorial/), 562 problem
22.  Interesting simple questions
    1. Binary search
       1. Pow functions can be computed in O(log n ) time.
