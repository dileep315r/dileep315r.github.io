#### Kafka
1. Use file system to write messages, append messages to existing files. See [link](https://kafka.apache.org/documentation/#design_filesystem) for more details.
    1.   The key fact about disk performance is that the throughput of hard drives has been diverging from the latency of a disk seek for the last decade. As a result the performance of linear writes on a JBOD configuration with six 7200rpm SATA RAID-5 array is about 600MB/sec but the performance of random writes is only about 100k/sec—a difference of over 6000X.
    2.    These linear reads and writes are the most predictable of all usage patterns, and are heavily optimized by the operating system. A modern operating system provides read-ahead and write-behind techniques that prefetch data in large block multiples and group smaller logical writes into large physical writes.
    3.  To compensate for this performance divergence, modern operating systems have become increasingly aggressive in their use of main memory for disk caching. A modern OS will happily divert all free memory to disk caching with little performance penalty when the memory is reclaimed. All disk reads and writes will go through this unified cache. This feature cannot easily be turned off without using direct I/O, so even if a process maintains an in-process cache of the data, this data will likely be duplicated in OS pagecache, effectively storing everything twice.
    4.  As a result of these factors using the filesystem and relying on pagecache is superior to maintaining an in-memory cache or other structure—we at least double the available cache by having automatic access to all free memory, and likely double again by storing a compact byte structure rather than individual objects. Doing so will result in a cache of up to 28-30GB on a 32GB machine without GC penalties.
    5.  Furthermore, this cache will stay warm even if the service is restarted, whereas the in-process cache will need to be rebuilt in memory (which for a 10GB cache may take 10 minutes) or else it will need to start with a completely cold cache (which likely means terrible initial performance). This also greatly simplifies the code as all logic for maintaining coherency between the cache and filesystem is now in the OS, which tends to do so more efficiently and more correctly than one-off in-process attempts. If your disk usage favors linear reads then read-ahead is effectively pre-populating this cache with useful data on each disk read.
    6.  This suggests a design which is very simple: rather than maintain as much as possible in-memory and flush it all out to the filesystem in a panic when we run out of space, we invert that. All data is immediately written to a persistent log on the filesystem without necessarily flushing to disk. In effect this just means that it is transferred into the kernel's pagecache.
    7.  This style of pagecache-centric design is described in an article on the design of Varnish [here](https://varnish-cache.org/docs/trunk/phk/notes.html).
    8. Having access to virtually unlimited disk space without any performance penalty means that we can provide some features not usually found in a messaging system. For example, in Kafka, instead of attempting to delete messages as soon as they are consumed, we can retain messages for a relatively long period (say a week). This leads to a great deal of flexibility for consumers, as we will describe.
    9. Once poor disk access patterns have been eliminated, there are two common causes of inefficiency in this type of system: too many small I/O operations, and excessive byte copying.
    10. The small I/O problem happens both between the client and the server and in the server's own persistent operations.
    11. To avoid this, our protocol is built around a "message set" abstraction that naturally groups messages together. This allows network requests to group messages together and amortize the overhead of the network roundtrip rather than sending a single message at a time. The server in turn appends chunks of messages to its log in one go, and the consumer fetches large linear chunks at a time.
    12. This simple optimization produces orders of magnitude speed up. Batching leads to larger network packets, larger sequential disk operations, contiguous memory blocks, and so on, all of which allows Kafka to turn a bursty stream of random message writes into linear writes that flow to the consumers.
    13. The other inefficiency is in byte copying. At low message rates this is not an issue, but under load the impact is significant. To avoid this we employ a standardized binary message format that is shared by the producer, the broker, and the consumer (so data chunks can be transferred without modification between them).
    14. Modern unix operating systems offer a highly optimized code path for transferring data out of pagecache to a socket; in Linux this is done with the sendfile system call.
    15. 
3. Don’t cache explicitly, rely on OS caching of the log file.
4. Sequential disk reads/writes are much faster, faster than memory access in some cases.
5. Don’t process messages in storage and transit paths. Common encoding at processing, storage. Use send_file system call to send data to client directly from disk over network without process heap intervention.
6. Use batching so that the messages can be compressed and network overhead reduces and messages can be written to disk at once. Batching can be configured on client side.
7. Partitioning and replication are provided. Partitioning can be either random or through specified message properties.
8. Every message is assigned an identifier on the producer side. Producer can figure out duplicacy of messages with identifier
9. Transactional production to different topics is supported.
10. Offset is specific to the client and server maintains the offsets.
11. Replication can be configured for availability or consistency
12. Zookeeper is used to store the replica status
13. Replica is in-sync only if
    1. Heartbeats are received
    2. Caught up to the master queue
14. Lead partition maintains in sync replica set
15. Message is deemed published only if all the followers in ISR receive the message
16. Controller is responsible for the registration of brokers
17. Consumers pull the data from brokers with long polling
18. Offers log compaction. Log compaction is required for re-syncing of data to databases.

#### Kafka group consumer protocol
1. The Kafka consumer group protocol is a way for multiple Kafka consumers to coordinate their consumption of data from a Kafka topic. The protocol ensures that each consumer in a group only consumes data from a subset of the partitions in the topic, and that no data is lost or duplicated.
2. To use the Kafka consumer group protocol, each consumer in the group must be assigned a unique group ID. When a consumer joins a group, it will contact the group coordinator, which is a Kafka broker that is responsible for managing the group. The group coordinator will then assign the consumer a subset of the partitions in the topic.
3. Once a consumer has been assigned a subset of partitions, it will only consume data from those partitions. The consumer will keep track of the offset of the last message it has consumed from each partition. This offset is used to ensure that the consumer does not consume the same message twice.
4. If a consumer fails, the group coordinator will rebalance the partitions among the remaining consumers in the group. This ensures that no data is lost and that all of the partitions are still being consumed.

#### Kafka cluster
1. Yes, Kafka uses a gossip protocol to maintain cluster membership and metadata. The gossip protocol is a lightweight, peer-to-peer protocol that is used to exchange information about the state of a distributed system. In the case of Kafka, the gossip protocol is used to keep track of which nodes are in the cluster, their roles (e.g., controller, broker, etc.), and the state of their partitions.
2. A Kafka client can connect to ZooKeeper and query it for the list of brokers in the cluster. This is useful in cases where the Kafka cluster is dynamic and the broker addresses may change frequently.
3. Kafka clusters have a special role known as the "controller" which is responsible for managing the registration of brokers. If the controller detects the failure of a broker, it is responsible for electing one of the remaining members of the ISR to serve as the new leader. The result is that we are able to batch together many of the required leadership change notifications which makes the election process far cheaper and faster for a large number of partitions. If the controller itself fails, then another controller will be elected.

#### Kafka streams partition assignment
Kafka Streams uses the consumer group API to manage storing consumer offsets for all source topics. Kafka Streams also piggybacks off the same mechanism to assign tasks to all StreamThreads on those application instances.
