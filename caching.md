Use cache to speed up reads of not so frequently updated data.

1. Read strategies
   1. Read through. Example Varnish. Cache takes care of reads from the storage system. Requires same data model for cache and storage. Doesn't tolerate cache failures.
   2. Cache aside. Example Redis. App takes care of reads from the storage system.
2. Write strategies
    1. Write through. Varnish. Cache takes care of write to the storage system.
    2. Write around. Redis. App writes to the storage system.
    3. Write back. Redis writing data asynchronously to redis database.
3. Combine above two strategies for final solution. ***Consistency*** is a problem in caching.

#### Cache problems
1. Avalanche
   1. Large number of keys expire at the same time. Increases load on the storage system.
   2. Mitigation
      1. Staggered expiration. Add small random value to TTL.
2. Stampede
   1. Sudden increase in the number of requests to the storage system due to 
      1. Cache miss of popular keys.
      2. Spike in traffic.
      3. Restart of cache.
      4. Cache node failure and moving the traffic to a different node.
   2. Mitigation
      1. Consistent hashing to evenly distribute load to remaining non failed nodes.
      2. Circuit breakers to control load coming to cache servers.
      3. Rate limiting to control load coming to cache servers.
3. Cache miss attack/Cache penetration
   1. Solutions
      1. Store the 404 Not found response as well in the cache. Set TTL for cached 404 responses.
      2. Bloom filters to check for the existence of the key.
4. Hot keys
   1. Popular tweets of celebrity.
   2. Single cache node experiences resource overload due to the hot keys.
   3. Solutions
      1. Prefix hot key with random number and it would distribute traffic across multiple nodes. The hot key data will be replicated in multiple nodes.
      2. Store hot key values in application memory.
5. Large key problem
   1. Key value size is huge.
   2. Network bandwidth, memory and latency issues.
   3. Solution
      1. Change business requirements
      2. Divide and store small parts separately.
      3. Set long TTL for large keys
      4. Store compressed large key values
6. Cache inconsistency problems
   1. Within the cache system.
   2. Inconsistency with the storage system.
   3. Eventual consistency is used in cache systems.
   4. Multiple failures of same node under consistent hashing can lead to inconsistencies.
      1. Node A fails, key K rehashed to Node B, node B caches key K
      2. Node A comes back online, caches K with latest data.
      3. Node A fails, key K rehashed to Node B, node B already contains stale data of K.
      4. Solution: No automatic rehash.
7. Cache with single node per shard
   1. Use disk to backup the data
   2. Write-back disk backup vs write-through disk backup. There is a middle way as well that ack's the writes only if the writes are stored to disk.
8. Replication strategies
   1. Synchronous replication.
   2. Async replication. Redis uses async replication.
   3. Semi-sync quorum based replication.
9. Order of writes to cache
   1. Write to database first and then to cache. This is better than writing to cache first.
10. Concurrent write to the cache or write conflicts.
    1. Cache can end up having old value.
    2. Solution: Use compare with version number and swap only if version numbers match to update the cache entries. Version numbers can be maintained per item, per database, per shard. Memory vs retry frequency trade-off.
11. Monitor
    1. Cache hit ratio
    2. Key size
    3. Cache evictions
    4. Latency
    5. Invalidation rate

#### Cache eviction strategies
1. Least recently used
2. Least frequently used
3. First in First out
4. Random replacement

### Redis
Implement rate limiter with Redis by using key with expiration time to 1 minute(or rate limit window span) to count requests.

##### why is redis fast
1. In memory database. Single thread, IO multiplexing
2. Uses Simple Dynamic string for storing strings.
3. Uses LinkedList and ZipList for lists.
4. Uses hashtable for Hash
5. Uses skip list data structure for sorted set
