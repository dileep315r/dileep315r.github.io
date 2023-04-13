#### Kafka
1. Use file system to write messages, append messages to existing files.
2. Don’t cache explicitly, rely on OS caching of the log file.
3. Sequential disk reads/writes are much faster, faster than memory access in some cases.
4. Don’t process messages in storage and transit paths. Common encoding at processing, storage. Use send_file system call to send data to client directly from disk over network without process heap intervention.
5. Use batching so that the messages can be compressed and network overhead reduces and messages can be written to disk at once. Batching can be configured on client side.
6. Partitioning and replication are provided. Partitioning can be either random or through specified message properties.
7. Every message is assigned an identifier on the producer side. Producer can figure out duplicacy of messages with identifier
8. Transactional production to different topics is supported.
9. Offset is specific to the client and server maintains the offsets.
10. Replication can be configured for availability or consistency
11. Zookeeper is used to store the replica status
12. Replica is in-sync only if
    1. Heartbeats are received
    2. Caught up to the master queue
13. Lead partition maintains in sync replica set
14. Message is deemed published only if all the followers in ISR receive the message
15. Controller is responsible for the registration of brokers
16. Consumers pull the data from brokers with long polling
17. Offers log compaction. Log compaction is required for re-syncing of data to databases.

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
