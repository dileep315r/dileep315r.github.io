### Techniques to index data and find nearby restaurants/vehicles quickly
1. Geo-hashing, divide the map into grids. Given a latitude and longitude, we can pinpoint the grid number with hash function on the latitude and longitude.
   1. Geohashing is not dynamic.
   2. When a grid is densely populated, we need to iterate through all the items in the grid to find the items matching our criteria.
   3. Too many grids, we might need to search many grids.
   4. Too few grids, we might iterate through items in the grid.
2. K-d tree
   1. Index such that each node divides the search space further in half along one dimension.
3. Quad trees
   1. Divide the current set of nodes into four boxes if the number of nodes is greater > limit.
   2. Works well for the densely populated areas.
4. Good solution
   1. Use geo-hashing at level one. As it reduces the search space drastically in a single shot.
   2. Use Quad trees to search within a single grid.