# Sharding
Vertical sharding - Divide table into sets of columns. or Divide tables into sets of tables and distribute each set to a partition.
Horizontal sharding - Divide table data by ID(or key) ranges

#### strategies to distribute data across nodes
1. Modulus sharding is problematic since
   1. It causes large number of keys to be reshuffled to different nodes in the event of re-balancing the partitions.
   2. If the node goes down, not only the failed nodes keys needs to be distributed, but the other live nodes keys also needs to be distributed.
2. Key Range sharding
   1. Number of partitions >>> number of nodes. Each node serves several partitions. 
   2. Each partition contains a specific key range data.
   3. Good for range scans/queries.
   4. The data volume might not have been evenly distributed across the ranges.
   5. One partition might receive extremely high number of requests compared to other partitions. Suffix the key with random number and replicate the data across partitions or use auxiliary column data as part of the key to distribute data across several partitions. Implement special logic for the skewed data if necessary.
   6. Some access patterns might lead to hot partitions.
   7. The partition boundaries might be chosen manually by an administrator, or the database can choose
      them automatically.
3. Consistent hashing
   1. Each of the hash values are assigned to a position on the ring.
   2. Nodes are also assigned to a position on the ring.
   3. Each node handles the hash keys to the left of the node on the ring.
   4. https://blog.bytebytego.com/p/a-crash-course-in-caching-part-2 for more info.
   5. Adding or removing nodes from the system only requires remapping the keys that were previously stored on the affected nodes, rather than redistributing all the keys, making it easy to change the number of shards with a limited amount of data rehashed.
4. Hash partitioning
   1. Number of partitions >>> number of nodes. Each node serves several partitions.
   2. Each partition contains a specific hash range data.
   3. Fixed number of partitions vs variable number of partitions.
   4. If the partition boundaries are selected pseudo-randomly then it's called consistent hashing.
   5. Range scan queries now need to scan multiple/all partitions.
   6. Cassandra uses composite key. First part of the key determines the partition and the remaining part determines the sort order in the partition. Range scans for the second part of the key is possible.
5. Re-balancing
   1. Manual re-balancing.
   2. Automated re-balancing.
6. Finding the node
   1. Client can contain the logic.
   2. Any node can contain the logic and can route the requests to appropriate node.
   3. Separate routing tier can handle the node finding queries.

#### Secondary Indexes
1. Partition indexes by document
   1. Indexes only the documents in the current partition.
   2. Secondary index on a shard/node only indexes the documents present on the shard/node.
   3. Alias local index.
   4. Scatter/Gather queries are required to search for a secondary key.
2. Partition indexes by Term
   1. A node index may index documents not present on the node/shard.
   2. Secondary index keys are partitions and distributed across nodes/shards.
   3. Alias global index.
   4. Writes are slower with this approach as the write to a single document requires writing to multiple partitions. Requires distributed transaction to make the changes appear right after the acknowledgement of the writes. Index updates are async in practice.

#### Re-balancing 

#### partitions
Over the time throughput may change, node may fail, data size may increase. All of this might require re-balancing the data thereby load.
 1. Fixed partitions
    1. New node can steal a few partitions from every existing nodes until partitions are fairly distributed.
    2. Only the assignment of partitions to nodes changes.
    3. Change of assignment happens over time. It's not immediate.
    4. More partitions can be assigned to nodes with better hardware.
    5. Number of partitions are fixed at outset.
    6. Each partition comes with a management overhead. Hard to achieve the right number of partitions.
    7. Size of each partition is proportional to the data size.
 2. Dynamic partitions
    1. Split the partition if the size grows about the limit. One of the partitions can be transferred to a different node to balance the load.
    2. Shrink the partitions if the data decreases below a limit.
    3. Number of partitions is proportional to the data size.
3.  Hybrid
    1. Fixed number of partitions per node. 

#### Manual vs automatic
1. Fully automated approach can lead to overload of the slow node if the automatic failure detection is faulty.

No automatic load distribution of the hot keys in current day databases. Automatic rebalancing of partitions might help upto a certain extent, but it might not be effective.
Application needs to use special logic to handle these cases.

##### Drawbacks of sharding
1. Difficult to maintain integrity and consistency of the data. Complex logic in application layer and database layers.
2. Performance overhead, increase in application latency.
