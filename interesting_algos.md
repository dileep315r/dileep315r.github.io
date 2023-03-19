1. [Geometric applications of BST](https://www.coursera.org/lecture/algorithms-part1/1d-range-search-wSISD)
2. ***String processing algorithms***
   1. Given a search string s, find the occurrences of s in string S.
       1. KMP pattern matching alo. Construct state machine for the string s and use the state machine to search for pattern s in S.
       2. Boyer-more algo. Visual explanation: Align the starting of the pattern to the start of the string S. Start matching the pattern with S from pattern end char to the pattern start char. Move the pattern until the string S end char matches with one of the pattern char.
   2. [Matching pattern p in Fixed large string S.](https://www.coursera.org/learn/algorithms-on-strings/lecture/V1AYj/herding-text-into-suffix-trie)
       1. Application in genome processing
       2. Suffix tree for the large fixed string and search patterns in the tree. Char for edge if multiple edges, otherwise use the remaining string indexes as edge.
           1. High memory footprint.
           2. No approximate pattern matching
           3. BW Transform is a good solution to this problem.
3. [Suffix Array](https://en.wikipedia.org/wiki/Suffix_array) and [suffix array](https://www.coursera.org/learn/algorithms-part2/home/info)
4. [Huffman compression and LZW compression](https://www.coursera.org/learn/algorithms-part2/home/info)
5. [Genome processing algo's](https://www.coursera.org/learn/algorithms-on-strings/lecture/V1AYj/herding-text-into-suffix-trie)
6. [Fuzzy search algorithm](https://www.baeldung.com/cs/fuzzy-search-algorithm)
7. ***Probabilistic datastructures***
   1. Bloom filter
       1. Probabilistic set data structure with only add(x) and contains(x) operations. Takes O(1) space even if the size of the set is huge.
       2. Array of M bits.
       3. N hash functions with output range in 0 to M-1 range
       4. For each of the hash functions, compute hash of input and set Array[i] if the hash of the input is i.
   2. [Count min-sketch](https://en.wikipedia.org/wiki/Count%E2%80%93min_sketch)
       1. A probabilistic data structure that serves as a frequency table of events.
       2. Int[N][M] integers.
       3. N hash functions with output in 0 to M-1 range.
       4. For a given input i, for nth hash function
           1. If hash(i) = k, then increment Int[i][k]
       5. To count the frequency of input i,
           1. Return the min of Int[*][k] where k is the hash value of the ith hash function.
   3. [HyperLogLog](https://towardsdatascience.com/hyperloglog-a-simple-but-powerful-algorithm-for-data-scientists-aed50fe47869)
       1. Uses to count distinct elements in a stream of elements with O(1) space.
       2. Find max number of leading zeros in the hash value of elements seen so far. 2^max_leading_zeros is the count of distinct elements seen so far.
       3. Above algorithms accuracy is improved by other complicated measures.
