#### Coding interview quick guide
1. Use a modulo operator for cyclic shifts.
    1. https://leetcode.com/problems/moving-average-from-data-stream/ is example problem.
2. Pairs are super helpful data structures to express certain algorithms compactly.
3. HashSet for a set data structure. Visited hashSet for breadth first search of graph.
4. StringBuilder interface for string manipulation. String builder is memory efficient than plain carnation of strings.
    1. Building a list of strings and then joining them would consume much less memory than the string concatenation using the + operator. The final method, which is only applicable for Java is by using a StringBuilder. It is said that if we have an array of strings already built, then a join operation may be faster than a StringBuilder. However, for our implementation, we can use the StringBuilder on the fly and that turns out giving us the best performance according to leetcode stats.
5. Use substring method to get substring of words. Helpful method for string processing algos.
    1. Java String. A[n]
        1. substring(int beginIndex) -- \[beginIndex, n\]
        2. substring(int beginIndex, int endIndex) -- [beginIndex, endIndex)
        3. charAt(int index) -- char at specified index, index starts from 0
        4. startsWith(String prefix, int toOfffset) -- prefix begins at toOffset
        5. trim()
        6. matches(String regex)
        7. length()
        8. isEmpty()
        9. Priority Queue - poll to remove, offer to add element, peek to take a look at the value. PriorityQueue in java is min heap. Sometimes insert duplicate elements into the queue to avoid using the decrease key operation.
        10. Stack - pop and push. Queue - poll, offer or addLast, addFirst
        11. Use Arrays.fill method to fill array with a fixed value.
        12. HashCode is equal for two strings with same length and chars.
        13. TreeMap - subMap(start, end) to get subTree in the range.
        14. Collections.sort, Collections.min, Collections.swap for collection of elements. Use Comparator class and compareTo helper method to modify.
        15. Collections.binarySearch for binarySearch or Arrays.binarySearch()
        16. lastIndexOf(char) method of string
        17. LinkedHashMap implements LRU policy. https://leetcode.com/problems/lru-cache/ 
6. Consider implicit stack trace time as well for the space complexity.
7. Consider imput space as well for space complexity.
8. Interesting stack problems/solutions
    1. Use stack to handle pre-order to in-order traversal conversion.
    2. https://leetcode.com/problems/trapping-rain-water/. Not easy to come up with stack idea.
    3. https://leetcode.com/problems/largest-rectangle-in-histogram/ No easy to come-up with stack idea.
        1. Try to reduce the problem to finding max of "max of rectangles of a certain type/criteria(i.e group rectangles based on certain critera such that the max of the group can be found out in O(1))"
        2. The above problem considers all the rectangle involving a histogram bar at a time. Max of such rectangles is the rectangle with hight of the bar and extends to the right and left as far as possible.
    4. A stack is usually the choice for these increasing / decreasing columns type of problems.
    5. Tricky modified stack requirement questions
       1. Min stack https://leetcode.com/problems/min-stack/ Stack pair of elements(element, min) or two stacks
       2. Max stack https://leetcode.com/problems/max-stack/ Two trees, Stack(pop) + Heap(pop_max) + Lazy update of heap with set(set contains pop()'ed IDs not values) or LL with TreeMap
       3. Max frequency stack https://leetcode.com/problems/maximum-frequency-stack/
9. Use hashing, binary search, merge sort/comparison for surprising optimizations.
10. Backtracking can be defined as a general algorithmic technique that considers searching every possible combination in order to solve a computational problem. Build a solution incrementally, one piece at a time, removing those solutions that fail to satisfy the constraints of the problem at any point in time. that incrementally builds candidates to the solutions, and abandons a candidate ("backtracks") as soon as it determines that the candidate cannot possibly be completed to a valid solution.
    1. There are three types of problems in backtracking
        1. Decision Problem – In this, we search for a feasible solution.
        2. Optimization Problem – In this, we search for the best solution.
        3. Enumeration Problem – In this, we find all feasible solutions.
    2. Backtracking can be applied only for problems which admit the concept of a "partial candidate solution" and a relatively quick test of whether it can possibly be completed to a valid solution.
    3. Backtracking is an important tool for solving [constraint satisfaction problems](https://en.wikipedia.org/wiki/Constraint_satisfaction_problem),<sup><a href="https://en.wikipedia.org/wiki/Backtracking#cite_note-BiereHeule2009-2">[2]</a></sup> such as [crosswords](https://en.wikipedia.org/wiki/Crosswords), [verbal arithmetic](https://en.wikipedia.org/wiki/Verbal_arithmetic), [Sudoku](https://en.wikipedia.org/wiki/Algorithmics_of_sudoku), and many other puzzles.
    4. Good problems
        1. https://leetcode.com/problems/generate-parentheses/ two dimensions.
        2. https://leetcode.com/problems/maximum-length-of-a-concatenated-string-with-unique-characters/ backtracking reduced the amount of memory used over bruteforce technique. 
11. Branch and bound [https://en.wikipedia.org/wiki/Branch_and_bound](https://en.wikipedia.org/wiki/Branch_and_bound). Divide the search space into subspaces and discard the subspace if the bound function on the subspace is not better than the bound seen so far, further divide the subspace otherwise.
    1. When selecting the next solution subset, use the following strategies
        1. Depth first search
        2. Breadth first search
        3. Best first search – node with best bound function value.
    2. Example problems:
       1. Traveling salesman problem
12. Left shift operator simply shifts and fills the LSB with 0 and discards MSB. Right shift operator shifts right and fills the MSB with previous sign bit for signed right shift and 0 for unsigned right shift and discards LSB.
13. Can use enumeration of bits to simulate combinations. 4 ways, 2 bits, 4 numbers, each number ith bit 1 include ith item 0 don’t include ith item in combination.
14. Permutations generation
    1. Backtracking. Sub-problems solved again and again. Results are stored in the output list.
        1. Swap. A[j..n] forms the possible next values set.
            1. Swap the first item with any of the remaining n-1 items in the current array and solve for the remaining n-1 elements recursively.
            2. Swap back once done.
            3. Stop recursion when no elements remaining in the remaining array.
            4. Add the solutions to the output list.
        2. Pass the possible next values set in recursive calls. Use string builder to keep track of partial solution.
            1. https://leetcode.com/problems/permutations-ii/ problem for permutations without duplicate numbers.
            2. Same as above except two modifications.
            3. Pass the extra hash that would contain the possible numbers to choose from, in recursive calls.
        3. [Next permutation](https://leetcode.com/problems/next-permutation/)
            1. Traverse from left to right and find the first decreasing element with index i.
            2. Swap ith element with the least great element on the right side of ith index.
            3. Reverse the elements from (i + 1)th index to the nth index.
        4. [Find kth permutation](https://leetcode.com/problems/permutation-sequence/description/).
        5. Constrained next permutation problem https://leetcode.com/problems/next-greater-element-iii/description/
15. Backtrack find combinations of values. All approaches are given in details [here](https://leetcode.com/problems/subsets/)
    1. Recursive/iterative with/without memoization. Solve for A[i..n] recursively/iteratively. For each combination in A[i..n] output, add A[i - 1] element to generate new combination. Add generated combination to the output of A[i-1..j] and return the output.
    2. For each length k in [1..n]
        1. generate all combinations of length k using following approach ```gen(i = 0, k, partial_result, all_results)```
            1. Include ith element in the combination i.e add A[i] to the partial_result and call gen(i+1, k - 1, partial_result, all_results)
            2. if partial_result_size == k, add partial_result to all_results and return.
    3. Use bitmask, Generate integers from 0 to 2^n. Include A[i] in the combination if ith bit is 1. One bitmask corresponds to one combination.
16. NcK combinations, n! Permutations, and mix between n!/k!
17. Quicksort space complexity is o(logn). QuickSort worst case time complexity is o(n^2). Worst case may occur if the array is already sorted in descending order.
18. Use sentinel node to handle edge cases in linkedList. [https://leetcode.com/problems/plus-one-linked-list/description/](https://leetcode.com/problems/plus-one-linked-list/description/) is the problem.
    1. https://leetcode.com/problems/add-two-numbers/description/
    2. Sentinel node case in array. Use a condition like ```i == 0``` below to handle -1 index case. Struggled to come up with the below code though the idea is clear. for each element, current_cumulative_sum - min_cumulative_sum_before is the idea. https://leetcode.com/problems/maximum-subarray/ is the problem. Kadane's algorithm is a better practical runtime solution than the solution below.
     ```
     class Solution {
        fun maxSubArray(nums: IntArray): Int {
            var currentMinSum = 0
            var currentSum = 0
            var currentMaxWindowSum = 0

            for((i, num) in nums.withIndex()) {
                currentSum = currentSum + nums[i]
                val currentWindowSum = currentSum - currentMinSum
            
                if(currentWindowSum > currentMaxWindowSum || i == 0) {
                    currentMaxWindowSum = currentWindowSum
                }

                if (currentSum < currentMinSum) {
                    currentMinSum = currentSum
                    // currentMinIndex = i
                }
            }

            return currentMaxWindowSum
        }
     }
     ```
    1. https://leetcode.com/problems/binary-tree-maximum-path-sum/ binary search tree. Smartly avoids if conditions with the use of 0 as the filler.
    2. https://leetcode.com/problems/range-sum-query-2d-immutable/ matrix with size greater than one used for handling edge cases.
    3. https://leetcode.com/problems/unique-number-of-occurrences/ avoids if check in for loop using hash size check in the end.
    4. https://leetcode.com/problems/valid-parentheses/editorial/ hash character is used to avoid extra if condition.
19. Queue for BFS and stack for DFS. Use set for remembering visited nodes.
20. Dynamic programming
    1. If you implement recursive equation as it is with memoization, it can still be considered as a recursive approach. It uses stack and memoized memory.
       1. Good Dynamic programming approach works from bottom to top and stores only the required intermediate results. Lazy DP problem implementation is recursive and well thought through bottom up approach is a good DP solution.
       2. DP solution save the intermediate results in the input array/grid if possible i.e mutate the inout.

    2. Check if the seemingly dynamic programming problem can be solved using alternative approaches like sliding window algorithm, greedy algorithm etc..
    3. Dynamic programming, try to use lesser space for memoization.
    4. Use HashMap or array for memoization in dynamic programming
    5. Example problem: [https://leetcode.com/problems/minimum-path-sum/](https://leetcode.com/problems/minimum-path-sum/), 562 problem
    6. https://leetcode.com/problems/longest-palindromic-subsequence/ problem. Not easy to come up with space optimization ide.
    7. Use bitmask for representing a sub-problem. https://leetcode.com/problems/campus-bikes-ii/ is an interesting problem.
21. Binary search
    1. Pow functions can be computed in O(log n ) time.
    2. Consider the below classic BST routine
       ```
       low = 0, high = n - 1
       while(low <= high) {
          mid = (high + low)/2 //derived from low + num_elelments/2
          if(target < mid) high = mid - 1
          if(target > mid) low = mid + 1 
          if(mid) return
       }
       ```
        1. Insights
            1. Irrespective of the array indexing, (low + mid)/2 points to an index such that there are lower or equal elements on the left than the right.
            2. Low index points to the leadt great value of the search value when no answer found and the routine stops.
            3. Routine ends with examining one element array in the end if no answer found.
            4. If ```f(target < mid) high = mid - 1``` condition is changed to ```f(target <= mid) high = mid - 1```, then the routine ends with the starting index of the repeating search element.
    3. Interesting binary search. Useful for the scenario in which, the linear search is likely more efficient than plain binary search.  The element most probably occurs on the immediate right of the current position.
        1. Meta-search. https://leetcode.com/problems/find-smallest-common-element-in-all-rows/
          ```
          d <<= 1
          If (A[left + d] >= search_val) then new_left = left + 1, d = 1
          else left += d
          ```
22. Linear time sorting algo's
    1. Counting sort - elements in range [0, k], count number of elements of each number in [0,k]. Cumulative add to find number of elements(m) lesser than a number in [0,k] and place the element in mth position in the output. Fill the output from the end to the beginning. Reduce the frequency by 1 as the output array is filled.
    ```
       C[A[j]] = C[A[j] - 1
    ```
    1. Radix sort - Sort all the numbers by LSB digit using counting sort. Repeat the stable sort until MSB. Use counting sort to sort each column.
    2. Bucket sort - Assign each number to bucket and sort bucket using insertion sort.
23. Graph algo's
    1. Adjacency list, adjacency matrix, linked objects representations. Adjacency list commonly used.
    2. Find cycle in a directed graph
        1. DFS Graph coloring algo, non explored white, partially explored gray, fully explored black. Graph has cycle iff edge from current node to grey node. Edge from current node to black node is a cross edge.
    2. Cycles in a undirected graph
        1. DFS or BFS, iterative or recursive, maintain visited node to parent map, skip trivial cycles(A-B-A i.e edge A to B, came to B from A via the edge, trying to go to A via the same edge, current child node should not be a parent of current node).
        2. DFS or BFS, iterative or recursive, maintain visited nodes set, delete the opposite edge every time an edge is used to make sure that we don't traverse the same edge again. Cycle if we visit the same node again.
24. Union-find/Disjoint-set data structure complexity M operations, N nodes. O(M*alpha(N)), M is inverse ackerman function.
    1. Use cases
        1.  https://leetcode.com/problems/number-of-islands/
        2. Use union find to figure out whether two nodes are connected are not in O(1) time. Connected components problem.
        3. Other leetcode examples: https://leetcode.com/problems/sentence-similarity-ii/description/, 1101, 305, 1697
        4. https://leetcode.com/problems/evaluate-division/description/
        5. graph partition problem. We are asked to partition the nodes into several groups and find the largest one. https://leetcode.com/problems/largest-component-size-by-common-factor/
25. Use ```int[][]\{\{1, 0}, \{-1, 0\}, \{0, 1\}, \{0, -1\}\};``` to deal with grid traversal.
26. Try to see if heap can be used in place sorting for further optimization.
    1. Heap vs quick_sort vs counting_sort vs bucket_sort tradeoff in some of the cases.
27. BFS distinguish between levels.
    1. https://leetcode.com/problems/binary-tree-right-side-view/ has survey of all the methods described below.
    2. Store the current level number of nodes and pop exactly those many number of nodes to process the level completely.
    3. Maintain two queues and switch the queues to distinguish between levels in BFS.
    4. Another way is to store level info with every node.
    5. Another way is to add special/sentinel node in the queue to mark the ending of a level.
        ```
        LinkedList<Integer> queue = new LinkedList<Integer>();
            queue.addLast(start);
            Integer lastNode = start, distance = -1;

            while (queue.size() > 0) {
                LinkedList<Integer> nextQueue = new LinkedList<Integer>();

                while (queue.size() > 0) {
                    int nextNode = queue.removeFirst();
                    for (Integer neighbor : graph.get(nextNode)) {
                        if (!visited[neighbor]) {
                            visited[neighbor] = true;
                            nextQueue.addLast(neighbor);
                            lastNode = neighbor;
                        }
                    }
                }
                // increase the distance for each level of BFS traversal.
                distance += 1;
                queue = nextQueue;
            }
        ```
28. ArrayDeque can also be used for queue implementation. ArrayDequeue is implemented using Array in Java. TreeSet is an implementation for SortedSet in java. NavigableSet is a subtype of the sorted set. TreeSet is an [implementation](https://jenkov.com/tutorials/java-collections/sortedset.html) of the NavigableSet.
29. Topology sort
    1. Topology sort -- Arrange the nodes left to right in such a way that all the edges point from one of the left nodes to one of the right nodes.
    2. Topology sort in an undirected graph?? No, the undirected edge leads to cycles, and it's impossible to arrange nodes in topology sort order if the graph has cycle(s).
    3. Multiple ways
        1. Maintain a reverse adjacency list, remove incoming edges in the reverse adjacency list recursively until there are no nodes.
        2. DFS algo can be used.
           1. DFS with nodes printed after the children explored returns the reverse topology sort.
           2. Construct reverse adjacency list, run DFS, find cycles using colouring algo.
        3. Maintain in-degree count, decrement in-degree count each time the node is reached. No need to delete edges.
            1. Kahn's algorithm for topology sort. Slightly modified BFS. Add nodes with no incoming edges to the explored nodes set. For each node in explored set, remove edges to the neighbours and if neighbour has zero incoming edges, add neighbour to the next explored nodes set. Continue till there are no nodes left to explore.
30. Use Character class for storing Char's separately in Java/Kotlin.
    1. Use ```input.charAt(index) - '0'``` to get the integer value from char.
31. [Not super important] Master Theorem, also known as Master Method, provides asymptotic analysis (i.e. the time complexity) for many of the recursion algorithms that follow the pattern of divide-and-conquer.
    1. It does not apply to all recursion algorithms.
    2. T(n)=a⋅T(n/b) + f(n)
    3. Based on conditions, O(n^d) or O(n^log(a, base b)) or O(n^d.log(n)) is the time complexity.
32. BST problems
    1. https://leetcode.com/problems/recover-binary-search-tree/ has good explanations for in-order traversal especially iterative in-order traversal.
    2. BST the closest value to X, lies on the Binary search path from root node to the non-existent value.
    3. Successor or predecessor of a node can be found without full in order traversal of the tree. https://leetcode.com/problems/inorder-successor-in-bst/description/
    4. Successor or predecessor for the non-existent element lies on the search path.
    5. Fun fact: The number of unique binary tree structures that can be constructed using n nodes is C(n)C(n)C(n), where C(n)C(n)C(n) is the nth Catalan number.
    6. BST https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/ find first and last occurrences of the element
33. Max flow problem
    1. Graph with directed edges and positive values(capacity) for edges.
    2. Flow coming into a node must be equivalent to flow going out of a node.
    3. Given Source and destination, find max flow possible.
    4. Max flow is equivalent to the capacity of the minimum cut.
    5. Flow is max flow iff there are no augmenting paths.
34. Cut property: Least weighed edge must be in the spanning tree. Krushkal's and Prim's algo.
35. List, Set, Queue inherit from Collection. Map doesn't inherit from collection.
36. Use Random().nextInt() to generate random number in Java.
37. Arrays and maps are duals. Map can be used wherever the array can be used. If you can't use an array with less space, but array should be maintained, then use map. Use array instead of HashMap if you know that the keys are sequential. Examples: Chars from 'a' to 'z'.
    1. Quote from one of the leet-code [answer](https://leetcode.com/problems/minimum-knight-moves/) "In Java, the HashSet is not the most efficient data structure. For this reason, using the HashSet data structure to keep track of the visited cells in the Java implementation will result in the TLE (Time Limit Exceeded) exception."
    2. https://leetcode.com/problems/single-row-keyboard/ array instead of map.
38. Use pen and paper to visualize the indices when implementing tricky index implementation code.
39. PriorityQueue Heapify with shift-down approach takes O(n) time.[Shift-down is better than shift-up](https://stackoverflow.com/questions/9755721/how-can-building-a-heap-be-on-time-complexity) since the bulk of the tree is in the leaf nodes.
40. Extend the concept from 1D to 2D for solving some questions. For example https://leetcode.com/problems/range-sum-query-2d-immutable/ can be solved by extending the 1D concept.
41. [Binary Index Tree](https://cs.stackexchange.com/questions/10538/bit-what-is-the-intuition-behind-a-binary-indexed-tree-and-how-was-it-thought-a). Easier alternative to a segment tree. Easier to implement.
    1. Given set of elements,
        1. Update element at an index. Let's call it as put(i, value) op.
        2. Return cumulative frequency until an index. Let's call it as get(i) op.
    2. Natural way to speed up get operation is to precompute data since the getFrequency(i) is issued frequently.
    3. Natural way to speed up put operation is to not precompute anything, just set the value at that position.
    4. Middle ground is needed to speed up both operations.
    5. Instead of precomputing everything precompute only range of indices. For get, add precomputed ranges. For put, modify the ranges the index is part of.
    6. Balanced BST of indices. At a node with children, store sum of (left subtree indices and the node index value).
        1. For lookup, follow the BST to find the index.
            1. Start with sum 0.
            2. Ignore parent node, if the current node is left child of parent.
            3. Add parent node partial(range) sum to the counter if current node is right child of parent.
            4. Add the value of index node that we are looking for to the sum.
        2. For update
            1. Traverse from node up to the root.
            2. Increment value of node, if it's left parent of previous node.
    7. Figure out nodes/indices to update for put oop or figure out the nodes/indices to update for get op
        1. Using a bit manipulation trick.
            1. Write out node n in binary.
            2. Set the counter to 0.
            3. Repeat the following while n ≠ 0:
                1. Add in the value at node n.
                2. Clear the rightmost 1 bit from n.
42. Segment tree is a very flexible data structure, because it is used to solve numerous range query problems like finding minimum, maximum, sum, greatest common divisor, least common denominator in array in logarithmic time.
    1. Operations
        1. Update element
        2. Range query i.e sum of elements in a range, minimum of elements in a range.
    2. Maintain the segment tree in an array.
       1. update(i, val), update element and it's ancestral nodes.
       2. rangeSum(i, j), recursively call rangeSum(i, root) + rangeSum(root, j). rangeSum(node_left_min, node_right_max) = node_value.
       3. update(i, j, val) - lazy updates, mark the updates in the nodes and propagate the changes only when required.
    3. Subclass of segment tree:
        1. Looks like segment tree, but it can be solved without augmented structure. Example: https://leetcode.com/problems/range-addition/description/
    4. Persistent segment tree. Updates at different timestamps needs to be maintained.
       1. Same concept as Maintaining database index to maintain the snapshot isolation level. Use copy on write strategy. Create new node only if the node data changes.
    2. Lazy propagation: See this [link](https://www.youtube.com/watch?v=xuoQdt5pHj0)
    3. Range minimum problem: https://www.youtube.com/watch?v=c5O7E_PDO4U
       1. Segment tree, Sparse table are two solutions. Other solutions explained in the video.
       2. O(nlog(n)) construction time, O(1) time complexity for range Minimum query. See [this](https://www.youtube.com/watch?v=c5O7E_PDO4U) table for more information.
       3. Table of results dp[n][log(n)] = min(dp[n][logn - 1], dp[n - 1][logn - 1]).
       4. At each point compute min from (i to 2^j) j <= log(n)
       5. For range minimum, min(i, log(j - i + 1), (j - i + 1 - log(j - i + 1), j))
43. Tries
    1. Use hash for storing trie children. https://leetcode.com/problems/word-squares is an example problem.
        ```
        class TrieNode {
          HashMap<Character, TrieNode> children = new HashMap<Character, TrieNode>();
          List<Integer> wordList = new ArrayList<Integer>();
          public TrieNode() {}
        }
        ```
    2. https://leetcode.com/problems/index-pairs-of-a-string/description/ problem for trie

44. Djikstra implementations
    1. Distances array, visited set. Loop through distances to find the next node to visit.
    2. Distances array, priority queue of distances. No need for decrease key operation. Insert duplicate entries to the priority queue, when popping only consider the elements whose distance is lesser than the corresponding value in the distances array.
45. Line sweep algorithm to find 1-D interval intersections.
    1. Intervals with (start_time, end_time)
    2. Sort the intervals according to start_time. Add intervals to the priority queue with end_time as the key for the priority queue and interval as the value.
    3. For each interval in sort order
        1. Remove intervals whose end_time is lesser than the current interval start_time from the priority queue.
        2. All the intervals left in the priority queue intersect with the current interval.
        3. Add the current interval to the priority queue.
    4. Problems:
        1. https://leetcode.com/problems/employee-free-time
        2. https://leetcode.com/problems/meeting-rooms/
        3. https://leetcode.com/problems/meeting-rooms-ii/
        4. https://leetcode.com/problems/interval-list-intersections/
46. Simultaneous minimum and maximum.
    1. Can be solved using 3*n/2 comparisons instead of 2n - 2 comparisons.
    2. Compare pairs of elements from the input first with each other, and then compare the smaller with the current minimum and the larger to the current maximum, at a cost of comparisons for every 2 elements.
47. "Expand Around Center" for palindrome problem.
    ```
       // Example code for the longest palindrome substring
       main {
          expandAroundCenter(s, i, i); // for odd length palindrome
          expandAroundCenter(s, i, i + 1); // for even length palindrome
       }
    
       private int expandAroundCenter(String s, int left, int right) {
           int L = left, R = right;
           while (L >= 0 && R < s.length() && s.charAt(L) == s.charAt(R)) {
              L--;
              R++;
           }
           return R - L - 1;
        }
    ```
48. Huffman coding
    1. ***Problem***: Character file. Lossless compression. Encode, decode. Assign variable length binary character codewords(i.e 10111 - B, 10 - A etc..) to characters based on the frequencies of the characters in the file.
    2. Use prefix codes i.e no two codes are the prefixes of one another. Theorem: Prefix codes always achieve the optimal data compression among any character codes.
    3. This compression can achieve 20% to 90% of space savings. Space savings depend on the nature of the data.
    4. Represent codewords using a binary tree. Path label to leaf represent a codeword for the character at the lef node. Tree must be a full binary tree for optimal data compression.
    5. Algorithm:
        1. Min priority queue of nodes(frequency, left, right, char)
        2. Pop two nodes from the priority queue
            1. Create a new node with the popped nodes as the children and frequency as the sum of frequencies of two nodes.
            2. Insert new node into the priority queue.
        3. Repeat the process until there is only one element in the priority queue.
    6. Greedy algorithm, assigns the longest codes to the least frequent characters.
    7. Example problem: https://leetcode.com/problems/minimum-time-to-build-blocks/description/
49. Sometimes, rewriting the equations would lead to optimal computation
    1. Test whether an array has sub-array whose average is greater than avg. Example problem https://leetcode.com/problems/maximum-average-subarray-ii/
        1. Sum(A[ai..aj])/(j - i + 1) >= avg can be rewritten as (A[i] - avg) + (a[i +1] - avg) + ... >= 0
    2. A[i] + A[j] + (j - i) can be rewritten as (A[i] + i) + (A[j] - j).
        1. Sample problem: https://www.interviewbit.com/problems/maximum-absolute-difference/
50. Mini-max problems: Binary search used brilliantly for mini-max problems.
    ```
       // template for binary search given below
       while (left < right) {
          int mid = (left + right) / 2;
          if (condition)
             right = mid;
          else
             left = mid + 1;
       }
       return left;
    ```
    1. [410. Split Array Largest Sum](https://leetcode.com/problems/split-array-largest-sum/)
    2. [774. Minimize Max Distance to Gas Station](https://leetcode.com/problems/minimize-max-distance-to-gas-station/)
    3. [875. Koko Eating Bananas](https://leetcode.com/problems/koko-eating-bananas/)
    4. [1011. Capacity To Ship Packages Within D Days](https://leetcode.com/problems/capacity-to-ship-packages-within-d-days/)
    5. [Divide chocolate](https://leetcode.com/problems/divide-chocolate/)
    6. [Gas stations](https://leetcode.com/problems/minimize-max-distance-to-gas-station)
    7. https://leetcode.com/problems/maximum-tastiness-of-candy-basket
    8. https://leetcode.com/list/o2pr208d/ for full list of such problems.
51. Sliding window algorithms and/or two pointer algorithms. Generally results in O(n) time complexity.
    1. Expand or contract at back, front or both. This algorithm discards subset of input search space each time the expansion or contraction happens.
    2. Example: https://leetcode.com/problems/container-with-most-water. Not easy to come up with contraction from both sides idea. Not easy to prove that it works.
    3. Example: https://leetcode.com/problems/trapping-rain-water/. Not easy to come up with contraction from both sides idea.
    4. https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/ problem can be solved using two pointers instead of a hash map.
    5. https://leetcode.com/problems/longest-substring-with-at-most-k-distinct-characters/ sliding window
52. Good hashmap problems. Tricky to come up with hash solution.
    1. https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/ two, three sum etc problems.
    2. Sub-array sum and it's cousins https://leetcode.com/problems/maximum-size-subarray-sum-equals-k/description/
    3. See if you can use array data structure instead of hashmap if key belong to a small ordered set.
53. Good DFS, BFS, Dijkstra problems
    1. Modified BFS or Bellman ford or Dijkstra algorithm. https://leetcode.com/problems/cheapest-flights-within-k-stops/
    2. https://leetcode.com/problems/network-delay-time/ BFS, DFS modified and Dijkstra.
    3. https://leetcode.com/problems/walls-and-gates/ Walls anf gates simultaneous BFS from all the gates.
    4. Bidirectional binary search https://leetcode.com/problems/word-ladder/
       ![image](https://leetcode.com/problems/minimum-knight-moves/Figures/1197/1197_bi_bfs_illustration.png)
        1. https://leetcode.com/problems/minimum-knight-moves/ problem has good explanation for bidirectional BFS.
            1. Quote from answer "in theory, the above implementation of bidirectional BFS should be faster than the unidirectional BFS. However, in reality, this is not the case for the Java implementation, due to heavy usage of sophisticated data structures, which are inefficient compared to simple arrays."
        2. In a game board(chess etc), BFS from a location explores next bigger circle in each step of the BFS. Use this info to apply efficient bidirectional BFS. Pi*d^2 vs Pi*d^2/2 area covered for bidirectional BFS.
        3. https://leetcode.com/problems/word-ladder/description/ Bidirectional BFS efficient. 
    5. Binary tree height of the node to return nodes. Sort of like finding centroid algo https://leetcode.com/problems/find-leaves-of-binary-tree/description/
    6. Sometimes the tree construction is hard, optimize the tree/graph construction. https://leetcode.com/problems/word-ladder/solutions/ problem.
    7. "It is not surprising that problems that can be solved with BFS can also be solved with DFS. However, in most scenarios one method is more efficient than the other."
    8. https://leetcode.com/problems/minimum-knight-moves/ problem DP optimizes solution over BFS.
    9. https://leetcode.com/problems/fixed-point/ good binary search problem.
54. GCD algo, euclid's method.
    1. gcd(a,b) = gcd(max(a,b) - min(a,b), min(a,b)), can be proved by contradiction.
    2. For a > b, gcd(a,b) = a if b == 0, gcd(b, a % b)
55. Two sum, two sum II, three sum problems - hash for unsorted, two pointers for sorted.
    1. https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/
    2. Two pointers to solve
56. Sub-array sum or prefix sum problems
    1. https://leetcode.com/problems/subarray-sum-equals-k/
57. Use recursion to simulate variable number of nested for loops. See https://leetcode.com/problems/4sum/ for details.
58. Consider modification of the input to reduce storage overhead and surprising optimizations.
    1. https://leetcode.com/problems/number-of-islands/ number of islands in a grid problem. Stores the already explored nodes by making the input grid value to zero.
59. Comparisons of n elements with each other to find duplicates would take O(n2) time. Instead assign each of the numbers to a group in O(1) time, use hash, total time to find duplicates would be O(n).
    1. Problems:
        1. https://leetcode.com/problems/number-of-distinct-islands/ find unique islands. Use path signature hash to represent islands.Or use set<Node>#hashCode() as hash of the island.
        2. https://leetcode.com/problems/largest-component-size-by-common-factor/description/ assign numbers to common factors and merge groups.
60. Heap increase key, decrease key vs treeMap situation. Both O(log(n)) time. Interviewers are not able to understand that the increaseKey can be implemented for heap, so better to avoid heap in this situation.
    1. Stream of (ID, action) pairs. Action is either increase count or decrease count. Count starts at zero. Tree or a heap to maintain order of elements.
    2. Similar problem https://leetcode.com/problems/design-a-leaderboard/ Use TreeMap. Other way is HashMap and heap to get top K, O(Nlog(k))
61. Good priority queue problems
    1. https://leetcode.com/problems/minimum-cost-to-connect-sticks/description/
    2. Huffman coding described above.
    3. https://leetcode.com/problems/merge-k-sorted-lists/ priority queue optimizes over maintaining full sorted order.
    4. https://leetcode.com/problems/meeting-scheduler/ priority queue optimized than sorting the input.
    5. https://leetcode.com/problems/meeting-rooms-ii/description/ and https://leetcode.com/problems/meeting-rooms-iii/
    6. Scenario of inserting element into already sorted list could be a sign to use priority queue.
    7. Try to use lexicographical order of tuples as key when the elements should be ordered by two competing requirements/criteria.
    8. https://leetcode.com/problems/find-median-from-data-stream/description/ find median of data  using two priority queues, PQ avoids maintaining full sort order.
       1. Other solutions
          1. Reservoir sampling can be used for approximate answer.
          2. Buckets, assign numbers to buckets, find right bucket, sort bucket and find median.
          3. Segment trees
          4. Order statistic trees. are data structures which seem to be tailor-made for this problem. They have all the nice features of a BST, but also let you find the kth order element stored in the tree. Not ideal for interviews.
62. Range sum problems. Given an array, find the sum of elements from i to j.
    1. Range sum immutable
       1. Compute cumulative sum once and reuse it for range sum queries.
       2. https://leetcode.com/problems/range-sum-query-2d-immutable/description/ extends 1D cumulative sum to the 2D cumulative sum.
    2. Range sum mutable. Extra operation, update(i, value).
       1. Use segment tree.
       2. Sparse table data structure. Update might be complicated.
       3. Binary index tree.
63. Matrix problems
    1. Excel sheet computation https://leetcode.com/problems/design-excel-sum-formula/description/
       1. When a formula is assigned to a cell, make a list of all the cells, save the list, compute sum and save sum, recursively update the cells that depend on this cell using topology sort.
       2. Bruteforce computation approach.
64. Sorted 2D matrix walk down/up to find solution
    1. https://leetcode.com/problems/search-a-2d-matrix-ii/ brilliant walk
    2. https://leetcode.com/problems/leftmost-column-with-at-least-a-one/description/
65. String matching algorithms https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string/editorial/ http://www-igm.univ-mlv.fr/~lecroq/string/index.html
    1. Edit distance dynamic programming algo. Add, Remove, Replace as the number of operations. Little-bit tough to come up with the DP equation.
       1. Three cases s1, s2. DP(s1(i, j), s2(i, j))
       2. s1[j] = s2[j], DP(s1(i, j - 1), s2(i, j - 1))
       3. s1[j] != s2[j], remove character j, DP(s1(i, j), s2(i, j - 1)) + 1
       4. s1[j] != s2[j], add character in the end DP(s1(i, j - 1), s2(i, j - 1)) + 1
66. Math problems:
    1. Simple division https://leetcode.com/problems/divide-two-integers/description/
67. Prefer to use ```for(i =0; i < 10; i++)``` than ```for(i in indices)``` for the interview. The former is more flexible, allows for easy optimization.
68. 
