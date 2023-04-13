#### Replication types
1. Synchronous replication
   1. Synchronous replication requires two phase commit or consensus protocols like algorithms. See [this](https://courses.cs.washington.edu/courses/cse544/15au/lectures/lecture14-2PC-replication.pdf) link for more details.
   2. Spanner uses paxos protocol and two phase commit for distributed transactions.
2. Asynchronous replication
3. Semi-synchronous replication

#### Adding new follower
1. Snapshot of the leader
2. Copy snapshot to follower
3. Follower does continuous sync from the last snapshot timestamp

#### Follower fails and comes back online again
1. Follower syncs the information from the leader and resumes.
#### Leader fails

#### Automatic fail-over
1. Detect failure
   1. Most systems use timeout detect failure
   2. Membership/gossip protocol for failure detection.
2. Elect new leader
   1. Take nodes with the latest data.
3. Make new leader as master
4. Problems
   1. Split brain
   2. Loss of un-synced data
   3. Reuse of auto-increment numbers cause problems.

#### Replication methods
1. Statement based replication
   1. SQL statements executed on followers in the same order
2. WAL log replication
   1. Raw ordered disk byte changes applied to the followers. Tighly coupled with internal database implementation.
3. Logical(row based) replication
   1. Ordered row change data is applied to followers. MySQL binlog is an example.
4. Trigger based replication
   1. Above approaches doesn't give the flexibility to add application logic.
   2. Application logic can be used to only replicate a subset of the database, one kind of database to another, conflict resolution logic.
   3. Trigger procedure logs changes to a separate table.
   4. External sync process replicates the changes to the follower.

#### Replication lag
Lag is in the order of fraction of seconds typically.
1. Problems
   1. Read after write consistency
   2. Monotonic reads
   3. Consistent prefix reads

### Multi-leader replication
1. Multi datacenter operation   
   1. Performance
      1. Nearest datacenter write reduces latency. Writing to other masters happen asynchronously.
   2. Tolerance of datacenter outages

#### Multi-leader topologies
Amazon.com used this strategy. Difficult to get it right, maintain. Surprising user issues like items appear in shopping cart even after the removal of the item.
1. Star, mesh(all-to-all), cycle.
   1. Star and cycle problems
      1. Extra hop
      2. Failure of one node impacts all other nodes in the replication path.
   2. Mesh problems
      1. Some links are faster than others. Update operation might be issued before the insert operation is synced to the node.

#### Leaderless replication
High availability is the advantage. DynamoDB popularized the concept. No leader. All writes are issued to all the nodes which are hosting the key.
If node is unresponsive for writes, use either one of the following strategies
1. Read repair
   1. If you see a stale data item during the read operation, then issue the write operation to the stale data node(s).
2. Anti-entropy process
   1. Use Merkle-tree to efficiently find and correct differing keys in two nodes that should host same copy of data.
   2. Merkle-tree
      1. Leaf nodes contain keys and values.
      2. Parent nodes contain hash of the child node data.
      3. Repeat the hashing process until root node.
      4. When comparing, traverse from the root of the tree to the children of the tree.
      5. No need to traverse a node if the hash values are same in both of the nodes.
      6. The disadvantage is that when a node joins or departs the system, the tree’s hashes are recalculated because multiple key ranges are affected.
3. Quorum for reads and writes.
4. Consistency can be configured by configuring the quorum w and r
5. Sloppy quorums and hinted handoff for even high availability. If the node is down, then store the values in a neighbouring node until the node comes back online.

#### Conflict resolution
Current conflict resolution techniques is applied per item, doesn't look at the transaction.
1. Last write wins
2. Version vectors
3. Maintain all conflicting writes and ask the user to perform conflict resolution.
   1. If it's a database, then delegate the conflict resolution to the application later

#### Consistency models
1. Linearizability
   1. Behaves as if there is a single copy of data. Read, write, compare_and_set are atomic operations.
2. Causal consistency
   1. If the effect is returned, then the cause must also be present in the database. 
3. Read after write
4. Monotonic reads
5. Consistent prefix reads
6. Sequential consistency
7. Eventual consistency
8. Strict serializability
   1. A replication protocol exhibits "strong consistency" if the replicated objects are linearizable. Like linearizability, "strong consistency" is weaker than "external consistency", because it does not say anything about the behavior of transactions.
Check https://jepsen.io/consistency for consistency hierarchy
