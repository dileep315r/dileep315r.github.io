### Cassandra
#### Design goals
1. Extremely high availability
2. High throughput and low latency 
In order to achieve these goals Cassandra trades off some other properties, such as strong consistency. Cassandra's design is inspired from BigTable paper
#### Data model
1. table
2. schema(column names and types) - The schema defines the structure of each row, which consists of the various columns and their types. It also determines the primary key.
   1. primary key - partition key, clustering columns (or row key optional)
   2. All the rows corresponding to a single partition are guaranteed to be stored collocated in the same nodes, while rows belonging to different partitions can be distributed across different nodes.
3. Column families just like BigTable?? Official documentation doesn't mention it. See https://stackoverflow.com/questions/60798118/how-do-you-call-the-data-model-of-dynamodb-and-cassandra for changed data model.
##### Design notes
1. Classic consistent hashing implementation with virtual nodes on the ring and preference lists for replication.
2. Gossip protocol to broadcast the cluster state, membership info in the cluster. 
   1. Each node communicates with a set of nodes and propagates info about those nodes to the cluster. 
   2. Seed nodes are configured on each node for bootstrapping the cluster.
   3. Operator can add new node and provide that info to one node, and it broadcasts to other nodes.
   4. Why gossip protocol
      1. My answer: broadcasting is heavy, takes a lot of bandwidth as the cluster size increases.
   5. Other mechanisms used for high availability
      1. Hinted hand-offs
      2. Read repair
      3. Anti entropy process
   6. Uses SSTable to achieve high write throughput. SSTable idea is inspired from BigTable.
      1. Mem-table, WAL, SSTable, Compaction are the main concepts.
3. Routing middleware:
   1. Client can be configured to learn info about the cluster from a cassandra node.
   2. Client can send the requests to any cassandra node and the node sends the requests to the appropriate nodes in the cluster.
4. Leaderless replication. Tunable consistency level. No multi-row transactions.
   1. Read and Writes can be configured to 
      1. ALL - succeeds only of all the replicas respond.
      2. ONE - Any one replica must respond
      3. Quorum - Majority of the replicas must respond. SOME - some of the nodes must respond.
   2. Quorum reads and writes can be configured i.e (w + r) > n
      1. Some people claim that the quorum reads and writes achieve strong consistency. Not quite true.
   3. Reads returns the item with latest timestamp out of all the retrieved replica items.
   4. Above configurations will give various consistency, availability and latency models.
5. Linearizability
   1. Last write wins conflict resolution leads to non linearizability
   2. Quorum reads with read repairs does not lead to linearizability since implementing compare and set operation is not possible
   3. 4 phase protocol implemented can be configured on cassandra for linearizability
      1. 4 phases of protocol. Similar to 2 phase atomic commit protocol.
         1. Leader asks to prepare for the transaction(not sure single item or multi item), followers vote for participating in the transaction.
         2. Leader reads the version numbers of the item from all the followers. Compare and proceed only if the versions are same. All the writes are implemented with compare and set.
         3. Leader proposes a new value for the item and followers promise to commit.
         4. Leader sends commit or rollback.
6. Query efficiency
   1. Queries without partition key would scan all the partitions.
      1. Secondary indexes can be built to reduce latency for such queries. Document partitioned indexes are used to speed up the queries.
   2. Materialized views
   3. Denormalize data to avoid joins. Cassandra doesn't provide joins.
   4. Batch operations that would alter several rows in multiple partitions and in multiple tables.
      1. Logged batch - provides atomicity, but no isolation.
      2. Un-logged batch - no atomicity and isolation.
7. Doesn't use GFS/HDFS like BigTable/HBase

### DynamoDB
1. "Fast, flexible NoSQL database service for single-digit millisecond performance at any scale" is the pitch
2. The multi-tenant architecture explained above ensures high utilization of resources. We’ll also see that the multi-tenant approach provides flexibility for resource provisioning—we can allocate or deallocate resources on the partition level.
3. customers will have the option to select strong consistency for their tables. If not selected, they can choose to have eventual consistency.
4. No fixed schema - since the dataase is aimed for varied use cases
5. Primary key - partition key and sort key similar to cassandra. No clumn families
   1. the primary key for a table can have one of two schemas: only a partition key or a partition key with a sort key.
   2. All the rows with same partition key would be stored in a single partition. Hash(partition key) determines the partition.
   3. The rows inside partition are ordered by partition key, sort key
   4. This is quite different from Cassandra??? Definitely different from BigTable.
   5. the internal hash function provides us with the partition in which we will store the item for inserts.
   6. Within the partition, we will store items ordered by partition key—the sorting order of items can be ascending or descending depending on the user's request.
6. API - CRUD item
7. Automatic provisioning and manual provisioning like in cosmosDB
   1. The number of partitions/size of partitions would change based on the provision
   2. However, applications might access some keys more frequently. This results in underutilizing dedicated throughput for partitions accessed that are less frequently, and overloading and downtime of partitions that are accessed more frequently. Our partitioning must adapt to customer traffic patterns to solve the problem above.
   3. We define read capacity unit (RCU) as the ability of the system to complete one read request of an item of arbitrary size, say x KB. We define write capacity unit (WCU) as the ability of the system to complete one write request of an item of the same arbitrary size.
   4. For example, if a table has provisioned throughput of 10,000 RCUs and 5,000 WCUs, then for items of size x KB, at maximum throughput, it cannot read more than 10,000 items and cannot write more than 5,000 items per second.
   5. Our design works such that it assumes that all keys have an equal chance of being accessed. As a result, it divides throughput equally among all partitions. So after dividing a table into ten partitions, a single partition will have a throughput of 1,000 RCUs and 500 WCUs.
   6. When adding or removing partitions, we will distribute a table's provisioned throughput equally among the new number of partitions.
   7. If the table has provisioned throughput changes, the new throughput would be equally divided amongst the table's partitions.
   8. Method 1
      1. Assign RCUs to physical partitions equally. Resource usage will be enforced at the physical partition level.
      2. problem:
         1. Applications might access some partitions more frequently than others(hot partitions). Traffic to different partitions may vary over time. It leads to over and under-utilization of the pre-allocated resources.
         2. Throttling is when a partition's read or write requests get rejected because it is experiencing more traffic than it can handle, either because the traffic requires more throughput than the partition is allocated or because there aren't enough resources. Throttling is necessary to provide consistently good performance to clients. Had we not throttled, the excess load can bog down specific nodes with excessive load
            1. The first reaction of any user would be to increase the provisioned throughput of their table, but this could very well result in over-provisioning of throughput for partitions that might not need it; only the partition that is experiencing throttling needs more throughput.
            2. We need a solution that allows us to control the throughput of a partition without affecting the throughput of other partitions of its parent table.
            3. Bursting a partition means temporarily tapping into the unused throughput of its co-resident partitions.
               1. We can allow a partition to burst for an arbitrarily short period, say 300 seconds. We cannot allow bursting to permanently use the unused throughput of a co-resident partition since the co-resident partition belongs to another customer and that user has provisioned that throughput for their partition. We also cannot reserve throughput for bursting since that results in underutilizing the node's resources.
               2. Workload isolation between co-resident partitions means that the workload of one partition does not interfere with the workload to any of its co-resident partitions.
               3. Our design must be careful only to allow a partition to burst if unused throughput is available. This is a form of workload isolation.
               4. Token bucket algorithm can be used to enforce resource limits. Not convinced about the outline given by author.
               5. Bursting is temporary and only happens when the node has unused throughput. Adaptive capacity is reactive and only happens after throttling is observed. If our service is to guarantee a five nines SLA, then we need to do better.
            4. Adaptive capacity
               1. Move the partition experiencing high traffic to a new node which has enough capacity.
               2. Increase the throughput limits for the partition if the partition has been experiencing burst for threshold time.
            5. Global admission control
               1. We can build on our token bucket system by moving the tracking of tokens to a more global level. We will call this system global admission control (GAC).
               2. Our GAC will track the consumption of a table using tokens. A GAC is a control center node.
               3. Request routers maintain local token buckets to allow requests to pass through. Requests routers allow requests to pass through to partitions if they have tokens available.
               4. Request routers communicate to the GAC service to replenish tokens. These requests are made in a matter of seconds.
               5. The GAC estimates global token consumption using the information provided by the client.
               6. The GAC allocates tokens that are available to the user's overall tokens.
               7. We can keep the partition-level token buckets from our bursting solution and set an upper limit to them to ensure that one application cannot consume all or a significant share of the throughput of storage nodes.
               8. While GAC enables adjusting to throughput requirements, throttling can still occur when some items are hot for longer periods. It would be better to have some permanent scaling out in such cases.
               9. One solution is to split the partition based on key distribution if the consumed throughput crosses a certain threshold. If we wish to keep keys continuous, the split point should be where the throughput requirement is equally split between the resulting child partitions.
               10. Our users should not have to choose the right provisioned throughput for applications with highly irregular loads. In such cases, we should regulate throughput based on recent traffic partitions. As soon as we observe a peak, we should either increase the resources available to a partition or split the partition.
8. Replication
   1. We require replication not only across availability zones but even inside an availability zone. We want that all replicas of a partition have the same copy.
   2. Every partition will have multiple replicas spread throughout the global network. The replicas of a single partition are called a replication group.
   3. Replicating based on partitions is more useful than replicating full tables since it allows control over having different resources allocated to different partitions of the same table. Replication based on tables will result in replicating all partitions of a table, potentially underutilizing resources since all table partitions might not require the extra resources.
   4. The replicas of a single partition are called a replication group. Our replication groups will maintain consistent replicas worldwide using an algorithm called Multi-Paxos. This is similar to Spanner.
      1. Multi-paxos as outlined by the author
         1. A node can play all three roles. At any one point, a replication group has one leader. All the rest of the nodes are both acceptors and learners.
         2. Once the quorum of promises are received, the leader sends the commit decision to the client and the learner nodes.
         3. Any replica (a node member of the replication group) can trigger an election to elect a leader. 
         4. The leader replica serves to write requests and strongly-consistent read requests. The leader replica will remain the leader if it keeps renewing its leadership lease. A non-leader replica will trigger an election if it considers the leader replica faulty, unhealthy, or unavailable. The new leader will start serving writes and consistent reads after the previous leader's lease expires.
         5. Only the leader replica can serve instant consistent reads. Other replicas of the replication group will eventually be able to serve consistent reads.
         6. One way to maintain write availability is for the leader replica to add another member to the replication group as a log replica as soon as it finds that some replica is unresponsive or faulty. This is the fastest way to maintain the minimum number of replicas required to form a quorum.
         7. Our replication system provides eventual read consistency. Our system does this because, eventually, all replicas maintain the same entries as all members in their replication group. However, it is important to notice that only the leader replica provides instant consistent reads.
         8. Our system must ensure that a failed or faulty leader replica node is detected instantly. If the leader replica loses connection with all replication group members, then its failure is easy to detect. Gray network failures make it hard to detect a failure of the leader replica. A gray failure is defined as a failure in a component of a cloud network whose manifestations are fairly subtle, making it harder to detect. (Source: Gray Failure)
         9. One solution for gray failures is to enable communication between replicas in the replication group such that they can confirm that the leader replica can communicate with the rest of the replication group. The follower replica can confirm from enough (a simple majority) of its fellow members of the replication group that communication with the leader is happening before deciding to start an election. If it cannot get confirmation from enough member replicas that they can communicate with the leader replica, then it will trigger a leader election.
         10. Since all other follower nodes can communicate with the leader replica, they reply to the node with failed communication with the leader replica that they can communicate with the leader replica. So no election is triggered. If the majority (minimum two in this example) of follower nodes replied that they could not communicate with the leader replica, then the follower node that asked would have triggered an election.

9. Fault tolerance
   1. After decades of relentless chasing to extract more performance from silicon-based processors, we've reached a point where it is becoming increasingly challenging to guard against the possible data and calculation malfunctions. Hyperscalers like Google and Facebook have reported a new category of silent errors due to silicon level defects. See Detection and Prevention of Silent Data Corruption in an Exabyte-scale Database System and Silent Data Corruptions at Scale for more details.
   2. We will regularly archive our write-ahead logs. So, in the event of a node failure, we can recreate the partition using the archived write-ahead log.
   3. However, in case of a replica node failure, the repair process can take a while since replacing a replica involves copying the write-ahead log and the memory index. One solution is to introduce log replicas in partition groups. A log replica only stores the write-ahead log. Log replicas are like acceptors in Paxos.
   4. As soon as a leader replica of a replication group detects an unhealthy node, it backs up its write-ahead log in a node and adds it to the replication group as a log replica. This maintains the same level of durability as the replication group would in the absence of the unhealthy replica. This process is quick since only the unarchived write-ahead log needs to be backed up.
   5. Hardware failures can also cause incorrect data writes. These are hard to track because they can occur anywhere in the network without indicating hardware failure. The faulty server is working fine because it is serving acknowledgments and participating in replication.
   6. We can add checksums to avoid faulty data writes. The frequency of verifying data using checksums can vary based on the historical performance of the hardware. The hardware, known to fail more frequently, might require more frequent checksums. We can have checksums for a single log entry or the entire log. Using checksums prevents incorrect data from spreading throughout the replication group.
   7. We can use archived data to verify write-ahead logs. If a node realizes its write-ahead log is already archived, we can use archived data to verify that the replica has the correct write-ahead log. If not, this means that the node could be faulty.
   8. Continuous verification: Our design should carry out data verification of data at rest. These can be scheduled, and their frequency can vary. Such verification can help identify silent errors like bit rot, which is a non-functioning bit.
   9. Failure injection and stress tests can help us better understand the resilience of our code.
   10. Formal methods and extensive testing of our protocols. Testing is also important while deploying upgrades as it can reduce the chances of deploying buggy code.
