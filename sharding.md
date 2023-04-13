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
      1. Place virtual nodes on the ring to balance the load even better.
   3. Each node handles the hash keys to the left of the node on the ring.
   4. https://blog.bytebytego.com/p/a-crash-course-in-caching-part-2 for more info.
   5. Adding or removing nodes from the system only requires remapping the keys that were previously stored on the affected nodes, rather than redistributing all the keys, making it easy to change the number of shards with a limited amount of data rehashed.
   6. Consistent hashing with virtual nodes
      1. Let’s take an example. Suppose we have three hash functions. For each node, we calculate three hashes and place them into the ring. For the request, we use only one hash function. Wherever the request lands onto the ring, it’s processed by the next node found while moving in the clockwise direction. Each server has three positions, so the load of requests is more uniform. Moreover, if a node has more hardware capacity than others, we can add more virtual nodes by using additional hash functions. This way, it’ll have more positions in the ring and serve more requests.
         1. If a node fails or does routine maintenance, the workload is uniformly distributed over other nodes.
         2. It’s up to each node to decide how many virtual nodes it’s responsible for, considering the heterogeneity of the physical infrastructure.
         3. For replication, Each node will replicate its data to the other nodes. We’ll call a node coordinator that handles read or write operations. It’s directly responsible for the keys. A coordinator node is assigned the key “K.” It’s also responsible for replicating the keys to n−1 successors on the ring (clockwise). These lists of successor virtual nodes are called preference lists. To avoid putting replicas on the same physical nodes, the preference list can skip those virtual nodes whose physical node is already in the list.
   7. Hinted hand off. Confusing description below.
      1. If the leader is temporarily down and the participants can’t reach it, they declare the leader dead. Now, a new leader has to be reelected. Such frequent elections have a negative impact on performance because the system spends more time picking a leader than accomplishing any actual work.
      2. In the sloppy quorum, the first n healthy nodes from the preference list handle all read and write operations. The n healthy nodes may not always be the first n nodes discovered when moving clockwise in the consistent hash ring.
      3. Once node A is up and running again, node D sends the request information to A, so it can update its data. Upon completion of the transfer, D removes this item from its local storage without affecting the total number of replicas in the system.
      4. This approach is called a hinted handoff. Using it, we can ensure that reads and writes are fulfilled if a node faces temporary failure.
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

#### Key to shard mapping info
Problem: Find the node that contains the key. Also known as service discovery.
1. Three ways
   1. Client stores/retrieves the mapping info.
   2. Set of servers store/retrieves the mapping info. Client requests one of the servers and the server redirects or fetches response from the shard server.
   3. Routing tier servers store/retrieves the info. Routing tier server redirects or fetches the response from the shard. Use zookeeper to store the information.
2. Zookeeper to store key to shard mapping: Many distributed data systems need a separate management server like ZooKeeper. Zookeeper keeps track of all the mappings in the network, and each node connects to ZooKeeper for the information. Whenever there’s a change in the partitioning, or a node is added or removed, ZooKeeper gets updated and notifies the routing tier about the change. HBase, Kafka and SolrCloud use ZooKeeper.

##### Drawbacks of sharding
1. Difficult to maintain integrity and consistency of the data. Complex logic in application layer and database layers.
2. Performance overhead, increase in application latency.

#### [Shard Manager at facebook](https://engineering.fb.com/2020/08/24/production-engineering/scaling-services-with-shard-manager/)
1. Consistent hashing addresses the issue by redistributing only a small subset of data from existing servers to new servers. However, this scheme requires application to have fine-grained keys for statistical load balancing to be effective. Consistent hashing’s ability to support constraint-based allocation (e.g., data of European Union users should be stored in European data centers for lower latency) is also limited due to its nature. As a result, only certain classes of applications such as distributed caching adopt this scheme.
2. The allocation of shards to servers is explicitly computed with the capability of incorporating various constraints like locality preference, which hashing solutions cannot support. We found that the sharding approach is more flexible than hashing and suits the needs of a wider range of distributed applications.
3. The most basic one is the ability to failover. In the event of a hardware or software failure, the system can divert client traffic away from failed servers and may even need to rebuild impacted replicas on healthy servers. In large data centers, there is always planned downtime for servers to perform hardware or software maintenance. The shard management system needs to ensure that each shard has enough healthy replicas by proactively moving replicas away from servers to be taken down if deemed necessary.
4. Additionally, the possibly uneven and ever-changing shard load requires load balancing, meaning the set of shards each server hosts must be dynamically adjusted to achieve uniform resource utilization and improve overall resource efficiency and service reliability. Finally, the fluctuation of client traffic requires shard-scaling, where the system dynamically adjusts replication factor on a per-shard basis to ensure its average per-replica load stays optimal.
5. We discovered that different service teams at Facebook were already building their own custom solutions to varying degrees of completeness. It was common to see services able to handle failover but have a very limited form of load balancing. This led to suboptimal reliability and high operation overhead. This is why we designed Shard Manager as a generic shard management platform.
6. from simple counter service with high tens of servers to complex, Paxos-based global storage service with tens of thousands of servers.
7. Various factors contribute to the wide adoption. First, integrating with Shard Manager means simply implementing a small, straightforward interface consisting of add_shard and drop_shard primitives. Second, each application can declare its reliability and efficiency requirements via intent-based specification. Third, the use of a generic constrained optimization solver enables Shard Manager to provide versatile load-balancing capability and easily add support for new balancing strategies.
8. Last but not least, by fully integrating into the overall infrastructure ecosystem, including capacity and container management, Shard Manager supports not only efficient development but also safe operation of sharded applications, and therefore provides an end-to-end solution, which no similar platforms provide. Shard Manager supports more sophisticated use cases than do similar platforms, like Apache Helix, including Paxos-based storage system use cases.
9. 
