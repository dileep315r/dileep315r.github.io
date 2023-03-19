### Kafka

Use file system to write messages, append messages to existing files.
1. Don’t cache explicitly, rely on OS caching of the log file.
2. Sequential disk reads/writes are much faster, faster than memory access in some cases.
3. Don’t process messages in storage and transit paths. Common encoding at processing, storage. Use send_file system call to send data to client directly from disk over network without process heap intervention.
4. Use batching so that the messages can be compressed and network overhead reduces and messages can be written to disk at once. Batching can be configured on client side.
5. Partitioning and replication are provided. Partitioning can be either random or through specified message properties.
6. Every message is assigned an identifier on the producer side. Producer can figure out duplicacy of messages with identifier
7. Transactional production to different topics is supported.
8. Offset is specific to the client and server maintains the offsets.
9. Replication can be configured for availability or consistency
10. Zookeeper is used to store the replica status
11. Relica is in-sync only if
12. Heartbeats are received
13. Caught up to the master queue
14. Lead partition maintains in sync replica set
15. Message is deemed published only if all the followers in ISR receive the message
16. Controller is responsible for the registration of brokers
17. Consumers pull the data from brokers with long polling
18. Offers log compaction. Log compaction is required for re-syncing of data to databases.
