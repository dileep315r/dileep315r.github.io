#### Autocorrect
***Types***
1. As you type
   1. Autocomplete
   2. Autocorrect
2. After you type
   1. Did you mean?

***Dataset source***
1. External dictionary
2. Internal documents or part of the current file.

***Algorithm***
1. Approach (1)
   1. Generate all words within two edit distances of the current word and are present in the dictionary. Dictionary check reduces the search space.
   2. Use context information like number of occurrences of the word in documents, what the query is talking about etc.. to select one word out of many matches.
2. Approach (2)
   1. Generate trigrams for all words in dataset documents. ForExample: trigrams of "happy" are "hap, app, ppy". Make a map of trigrams to words.
   2. For a given word, generate trigrams, and search for all words within one edit distances from trigram's words. This reduces the search space.
   3. Use context information to get one word out of multiple words.
3. Levenstein automata and [B-k trees](https://en.wikipedia.org/wiki/BK-tree)
   1. Solr saves inverse index by using key-value index i.e LSM/SST trees.
   2. SSTable uses in-memory AVL tree index called memtable to lookup keys quickly.
   3. Solr uses Levenstein automata instead of AVL tree for the index.
   4. Levenstein automata is similar to a trie. Not sure about how it finds approximate matches within an edit distance effectively.

Reference:
1. Medium [post](https://towardsdatascience.com/autocorrect-in-google-amazon-and-pinterest-and-how-to-write-your-own-one-6d23bc927c81)
   2. Google uses HTTP to get autocorrect. Sample curl given below
      ```agsl
       curl 'https://www.google.com/complete/search?q=m&cp=1&client=gws-wiz&xssi=t&gs_pcrt=undefined&hl=en-IN&authuser=0&psi=<user_token>' \
      -H 'authority: www.google.com' \
      -H 'accept: */*' \
      -H 'accept-language: en' \
      -H 'cookie: MyCookie
      -H 'dnt: 1' \
      -H 'referer: https://www.google.com/' \
      -H 'sec-ch-ua: "Chromium";v="112", "Google Chrome";v="112", "Not:A-Brand";v="99"' \
      -H 'sec-ch-ua-arch: "arm"' \
      -H 'sec-ch-ua-bitness: "64"' \
      -H 'sec-ch-ua-full-version: "112.0.5615.137"' \
      -H 'sec-ch-ua-full-version-list: "Chromium";v="112.0.5615.137", "Google Chrome";v="112.0.5615.137", "Not:A-Brand";v="99.0.0.0"' \
      -H 'sec-ch-ua-mobile: ?0' \
      -H 'sec-ch-ua-model: ""' \
      -H 'sec-ch-ua-platform: "macOS"' \
      -H 'sec-ch-ua-platform-version: "13.2.1"' \
      -H 'sec-ch-ua-wow64: ?0' \
      -H 'sec-fetch-dest: empty' \
      -H 'sec-fetch-mode: cors' \
      -H 'sec-fetch-site: same-origin' \
      -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/112.0.0.0 Safari/537.36' \
      -H 'x-client-data: MyInfo \
      --compressed
      ```
2. Approximate string matching [wiki page](https://en.wikipedia.org/wiki/Approximate_string_matching)
3. [Agrep linux utility](https://en.wikipedia.org/wiki/Agrep)
4. String matching algorithms [wiki](https://en.wikipedia.org/wiki/String-searching_algorithm)
5. 