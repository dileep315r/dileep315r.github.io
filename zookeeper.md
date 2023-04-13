#### Zookeeper
#### [Lines from official documentation](https://zookeeper.apache.org/doc/r3.8.1/zookeeperOver.html)
1. ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. It exposes a simple set of primitives that distributed applications can build upon to implement higher level services for synchronization, configuration maintenance, and groups and naming.
2. The ZooKeeper implementation puts a premium on high performance, highly available, strictly ordered access.
3. The ZooKeeper implementation puts a premium on high performance, highly available, strictly ordered access. The performance aspects of ZooKeeper means it can be used in large, distributed systems. The reliability aspects keep it from being a single point of failure. The strict ordering means that sophisticated synchronization primitives can be implemented at the client.
4. Replicated over a set of hosts called an ensemble.
5. The servers that make up the ZooKeeper service must all know about each other. They maintain an in-memory image of state, along with a transaction logs and snapshots in a persistent store. As long as a majority of the servers are available, the ZooKeeper service will be available.
6. Clients connect to a single ZooKeeper server. The client maintains a TCP connection through which it sends requests, gets responses, gets watch events, and sends heart beats. If the TCP connection to the server breaks, the client will connect to a different server.
7. ZooKeeper stamps each update with a number that reflects the order of all ZooKeeper transactions. Subsequent operations can use the order to implement higher-level abstractions, such as synchronization primitives.
8.  It is especially fast in "read-dominant" workloads. ZooKeeper applications run on thousands of machines, and it performs best where reads are more common than writes, at ratios of around 10:1.
9. Unlike standard file systems, each node in a ZooKeeper namespace can have data associated with it as well as children.
10. We use the term znode to make it clear that we are talking about ZooKeeper data nodes.
11. The data stored at each znode in a namespace is read and written atomically. Reads get all the data bytes associated with a znode and a write replaces all the data. Each node has an Access Control List (ACL) that restricts who can do what.
12. ZooKeeper also has the notion of ephemeral nodes. These znodes exists as long as the session that created the znode is active. When the session ends the znode is deleted.
13. Latest version: Clients can also set permanent, recursive watches on a znode that are not removed when triggered and that trigger for changes on the registered znode as well as any children znodes recursively.
14. Guarantees
    1. Sequential consistency - Updates from a client will be applied in the order that they were sent.
    2. Single System Image - A client will see the same view of the service regardless of the server that it connects to. i.e., a client will never see an older view of the system even if the client fails over to a different server with the same session.
    2. Timeliness - The clients view of the system is guaranteed to be up-to-date within a certain time bound.
15. sync : waits for data to be propagated
16. The replicated database is an in-memory database containing the entire data tree. Updates are logged to disk for recoverability, and writes are serialized to disk before they are applied to the in-memory database.
17. Read requests are serviced from the local replica of each server database. Requests that change the state of the service, write requests, are processed by an agreement protocol.
18. ZooKeeper uses a custom atomic messaging protocol. Since the messaging layer is atomic, ZooKeeper can guarantee that the local replicas never diverge. When the leader receives a write request, it calculates what the state of the system is when the write is to be applied and transforms this into a transaction that captures this new state.
19. we rely on time for liveness not for correctness.
20. our assumption of FIFO channels is very practical given that we use TCP for communication. Specifically we rely on the following property of TCP: Ordered delivery, no messages after close.
21. Atomic broadcast system in zookeeper
    1. Reliable delivery, Total order and causal order properties.
    2. Terms: packet, proposals and messages.
    3. Total order of messages. Zxid is the message number given by leader.
    4. Message is delivered only when the proposal is committed. Quorum of nodes must agree. All quorums have size (n/2+1) where n is the number of servers that make up a ZooKeeper service.
    5. ZooKeeper is a holistic protocol. We do not focus on individual proposals, rather look at the stream of proposals as a whole. Our strict ordering allows us to do this efficiently and greatly simplifies our protocol. Leadership activation embodies this holistic concept. A leader becomes active only when a quorum of followers (The leader counts as a follower as well. You can always vote for yourself ) has synced up with the leader, they have the same state. This state consists of all of the proposals that the leader believes have been committed and the proposal to follow the leader, the NEW_LEADER proposal. (Hopefully you are thinking to yourself, Does the set of proposals that the leader believes has been committed include all the proposals that really have been committed? The answer is yes. Below, we make clear why.)
    6. ZooKeeper messaging consists of two phases:
       1. Leader activation : In this phase a leader establishes the correct state of the system and gets ready to start making proposals. 
       2. Active messaging : In this phase a leader accepts messages to propose and coordinates message delivery.
22. After leader election a single server will be designated as a leader and start waiting for followers to connect. The rest of the servers will try to connect to the leader. The leader will sync up with the followers by sending any proposals they are missing, or if a follower is missing too many proposals, it will send a full snapshot of the state to the follower.
23. There is a corner case in which a follower that has proposals, U, not seen by a leader arrives. Proposals are seen in order, so the proposals of U will have a zxids higher than zxids seen by the leader. The follower must have arrived after the leader election, otherwise the follower would have been elected leader given that it has seen a higher zxid. Since committed proposals must be seen by a quorum of servers, and a quorum of servers that elected the leader did not see U, the proposals of U have not been committed, so they can be discarded. When the follower connects to the leader, the leader will tell the follower to discard U.
24. Any uncommitted proposals from a previous epoch seen by a new leader will be committed by that leader before it becomes active.
25. Common pattern to work around this is to issue a sync before issuing a read. This too does not strictly guarantee up-to-date data because sync is not currently a quorum operation. The stronger guarantee of linearizability is provided if an actual quorum operation (e.g., a write) is performed before a read.
26. Fuzzy snapshots are described in [here](https://zookeeper.apache.org/doc/r3.4.8/zookeeperAdmin.html) and [here in implementation section](http://sangarshanan.com/mit6.824/2020/04/01/zookeeper.html)
27. The wait-free property has proved to be essential for high performance.
28. In distributed systems like RAFT master handles all the traffic and scaling up the number of servers won’t really scale up the performance since leader is the bottleneck and leader has more replicas to handle and while this bottlneck is needed to keep things to be linearizable Zookeeper prefers higher read performance and hence lets you query from the replicas that are not master directly by sacrificing linearity which means you could read stale data. But Writes are linearizable
29. Zookeeper moved away from locks cause its blocking and hence can cause slow or faulty clients to negatively impact the performance of faster clients.
30. Zookeeper has the following properties
    1. Wait Free (Performance ++)
    2. FIFO Client Ordering (all requests from a given client are executed in the order that they were sent by the client.)
    3. Linearizable writes (all requests that update the state of ZooKeeper are serializable and respect precedence)
31. Zookeeper is read heavy so client side caching is important so it allows clients to cache and watch for updates to the cached object and receive a notification. Chubby uses leases to avoid blocking from faulty clients
32. All znodes store data and all znodes except for ephemeral znodes can have children
33. The asynchronous API, however, enables an application to have both multiple outstanding ZooKeeper operations and other tasks executed in parallel. The ZooKeeper client guarantees that the corresponding callbacks for each operation are invoked in order.
34. If the version number is 1 it does not perform version checking.
35. sync(path): Waits for all updates pending at the start of the operation to propagate to the server that the client is connected to. Sync can ensure that the read for a znode is linearizable though it comes at a performance cost. It forces a server to apply all its pending write requests before processing a read. Similar to FLUSH primitive
36. Even when there is no activity between the client and the server, the client sends the last served zxid to that server. In case of disconnectivity from that server, the client is connected to another one. Using the last zxid, ZooKeeper ensures that the client gets the same view as the previous server. If the new server is not at the same zxid as the client, then it doesn’t establish a session with it unless both are not in the same state. ZooKeeper guarantees that the client will be connected to a server with the same recent view.
37. Session is transferable to other servers if the current connected server is not reachable??? Does leader advertise the session status to all the servers in the ensemble???
38. implement efficient and sophisticated coordination protocols at the client even though reads are not precedence-ordered and the implementation of data objects is wait-free.
39. 
#### Other sources documentation
1. Use-cases
   1. Worker assignment
   2. leader election, synchronization
      1. Avoid locking with herd effect by utilizing the watches, regular nodes with zxid in name flag.
   3. membership services
   4. dynamic configuration management
   5. naming???
2. The formal consistency model by Zookeeper lies between sequential consistency and linearizability, called ordered sequential consistency.
3. As per official documentation: ZooKeeper is a centralized service for maintaining configuration information, naming, providing distributed synchronization, and providing group services. It exposes a simple set of primitives that distributed applications can build upon to implement higher level services for synchronization, configuration maintenance, and groups and naming.
   1. ZooKeeper allows distributed processes to coordinate with each other through a shared hierarchical namespace which is organized similarly to a standard file system. The namespace consists of data registers - called znodes, in ZooKeeper parlance - and these are similar to files and directories. Unlike a typical file system, which is designed for storage, ZooKeeper data is kept in-memory, which means ZooKeeper can achieve high throughput and low latency num.
   2. The client application processes store their coordination data on znodes.
4. There is a set of ZooKeeper servers called the ZooKeeper ensemble.
5. Unlike standard file systems, each node in a ZooKeeper namespace can have data associated with it as well as children.
6. Along with wait-free data objects, the other ZooKeeper design decisions that enable the implementation of a high-performance (hundreds of thousands of transactions per second) processing pipeline are as follows:
   1. We need first in first out (FIFO) execution for client requests. Multiple write requests are queued in the server so that they can be executed in the FIFO order.
   2. We require linearizability to handle requests from clients that alter the state of ZooKeeper.
7. Only the write request needs to be forwarded to the leader, and the leader broadcasts the request to all other followers. After broadcasting the request to the followers, the leader responds to the follower who forwarded the write request to it. Then, that follower replies to the client’s write request. The broadcasting of the write requests ensures that each server has eventually the same data to show the client. For read requests, the follower doesn’t need to forward the request to the leader and can process the request itself.
8. The end clients don’t need to keep track of the current leader since the ZooKeeper service nodes will know it.
9. Components of zookeeper
   1. Replicated database: This is an in-memory copy of the database so that read and write operations can be done locally.
      1. The replicated database is the storage component of ZooKeeper. When the client calls either the create() or setData() method, data is stored in an in-memory data object called a znode (Zookeeper node) in the form of a tree.
      2. Each write operation is logged on the disk before it is performed on in-memory database.
      3. After logging it on the disk, if there is any other operation currently being performed on the same data, then this request goes to the queue.
      4. See [this](https://stackoverflow.com/questions/21809161/confused-about-transaction-logs-in-zookeeper) answer to get idea about snapshots for recovery. ??? ZooKeeper takes periodic snapshots of all the delivered messages for fault tolerance. These messages are stored on the disk for recovery.
         1. Since this recovery is a background process and doesn’t lock the ZooKeeper state, we call these snapshots, fuzzy snapshots.
         2. This tree is extracted from the write-ahead log which was stored on the majority of nodes as part of consensus.
   2. Atomic broadcast
   3. Request processor: This is like a manager that keeps all the transactions atomic. Only the leader can use this service.
10. ZAB protocol
    1. Used to agree on a leader in the ensemble, synchronize the replicas, manage the broadcast of update transactions, and recover from a crashed state to a valid state.
    2. Transactions are identified by a specific type of identifier, called zxid. This identifier consists of two parts <e,c>, where e is the epoch number of the leader that generates the transaction and c is an integer acting as a counter for this epoch.
    3. Note: Practically, Zookeeper uses a leader election algorithm called Fast Leader Election (FLE), to employ an optimisation. It attempts to elect a leader that has the most up-to-date history from a quorum of processes. This algorithm minimizes the data exchange between the leader and the followers in the Discovery phase. The counter c is incremented every time a new transaction is introduced by the leader, while e is incremented when a new leader becomes active.
        1. Leader election process
           1. Discovery
           2. Synchronization
           3. Broadcast
11. Ephemeral z-nodes are useful to implement membership services and distributed lock/mutual exclusion.
12. 

#### Tradeoffs and comparisons
1. Drawbacks of old coordination services
    1. Old systems specialized for different use cases.
    2. The old coordination systems use blocking primitives like locks.
        1. Zookeeper is similar to Chubby but without the locking service.
2. Zookeeper advantages
    1. Customization. Can expose new services on top of existing functionality.
        1. An API through which they can create their own primitives according to their application requirements and use them.
    2. Wait-free service with relaxed consistency guarantees?? Against the coordination services purpose.
        1. The coordination kernel refers to the wait-free, relaxed consistency-guaranteed service offered by ZooKeeper. With the help of the ZooKeeper coordination kernel, numerous crucial applications can implement different coordination primitives without changing the underlying service core.

***References:***
1. [MIT article](http://sangarshanan.com/mit6.824/2020/04/01/zookeeper.html)
2. [Zookeeper internals](https://zookeeper.apache.org/doc/r3.8.1/zookeeperInternals.html)
2. [Overview of zookeeper](https://zookeeper.apache.org/doc/r3.8.1/zookeeperOver.html)
2. [ZAB protocol](https://cwiki.apache.org/confluence/display/ZOOKEEPER/Zab1.0)
2. [Zookeeper site](https://zookeeper.apache.org/)
