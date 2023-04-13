### Indexing to find nearby objects quickly
1. B-Tree indices - not a good solution
   1. Index on lat
   2. Index on lang
   3. Retrieve addresses matching lat range, retrieve lang range addresses, intersect both sets.
   4. Problems: A single lat range spans an entire section of the globe. Several points need to be retrieved. Not efficient.
2. Space filling curves, convert two 2D map into one dimension using space filling curve and use B-Tree to index one dimension.
3. Geo-hashing, divide the map into grids. Given a latitude and longitude, we can pinpoint the grid number with hash function on the latitude and longitude.
   1. Geohashing is not dynamic.
   2. When a grid is densely populated, we need to iterate through all the items in the grid to find the items matching our criteria.
   3. Too many grids, we might need to search many grids.
   4. Too few grids, we might iterate through items in the grid.
   5. Implementation methods:
      1. Each grid is assigned to a redis partition in redis geo-sharding.
      2. B-Tree index data by grid number in a database.
3. K-d tree
   1. Index such that each node divides the search space further in half along one dimension.
   2. See [this animation](https://en.wikipedia.org/wiki/File:Kdtreeogg.ogv) for range search animation. Range search is quite complicated to understand.
   3. Range tree is very similar to a k-d tree.
4. Quad trees
   1. Divide the current set of nodes into four boxes if the number of nodes is greater > limit.
   2. Works well for the densely populated areas.
5. R-tree
   1. Multi-dimensional B-trees
   2. Each node stores the set of bounding boxes. Bounding boxes may intersect but not enclose/contain other boxes fully. Subtree contains all the objects that fit within the bounding box.
6. Good solution
   1. Use geo-hashing at level one. As it reduces the search space drastically in a single shot.
   2. Use Quad trees to search within a single grid.

References:
1. [k-d tree Wiki article](https://en.wikipedia.org/wiki/K-d_tree)
2. [Nearest neighbour search wiki page](https://en.wikipedia.org/wiki/Nearest_neighbor_search)
3. [R-trees](https://en.wikipedia.org/wiki/R-tree)
4. [Generalised search tree](https://en.wikipedia.org/wiki/GiST)
5. https://www.youtube.com/watch?v=M4lR_Va97cQ
