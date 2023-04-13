#### Stream processing
1. A type of data processing engine that is designed with infinite data sets in mind.
2. System aspects
   1. Delivery guarantee
   2. Fault tolerance
   3. State Management
   4. Performance throughput and latency
   5. Advanced Features : Event Time Processing, Watermarks, Windowing
3. type of systems
   1. Native Streaming
      1. It means every incoming record is processed as soon as it arrives, without waiting for others. There are some continuous running processes (which we call as operators/tasks/bolts depending upon the framework) which run for ever and every record passes through these processes to get processed. Examples : Storm, Flink, Kafka Streams, Samza.
   2. Micro-batching
      1. It means incoming records in every few seconds are batched together and then processed in a single mini batch with delay of few seconds. Examples: Spark Streaming, Storm-Trident.
4. Spark has emerged as true successor of hadoop in Batch processing and the first framework to fully support the Lambda Architecture (where both Batch and Streaming are implemented; Batch for correctness, Streaming for Speed).
   1. custom memory management (like flink) called tungsten, watermarks, event time processing support,etc.
   2. option to switch between micro-batching and continuous streaming mode in 2.3.0 release.
   3. High throughput, good for many use cases where sub-latency is not required
   4. Exactly Once
   5. Stateless by nature????
   6. Lags behind Flink in many advanced features????
5. Storm
   1. Disadvantages
      1. No state management 
      2. No advanced features like Event time processing, aggregation, windowing, sessions, watermarks, etc 
      3. Atleast-once guarantee
6. Flink
   1. Flink is essentially a true streaming engine treating batch as special case of streaming with bounded data.
   2. Low latency with high throughput, configurable according to requirements
   3. Auto-adjusting, not too many parameters to tune
   4. As a summary, the core part is that Flink implements its algorithms not against Java objects, arrays, or lists, but actually against a data structure similar to java.nio.ByteBuffer. Flink uses its own specialized version, called MemorySegment on which algorithms put and get at specific positions ints, longs, byte arrays, etc, and compare and copy memory. The memory segments are held and distributed by a central component (called MemoryManager) from which algorithms request segments according to their calculated memory budgets.
   5. lightweight snapshot
7. [Kafka stream vs flink](https://www.confluent.io/blog/apache-flink-apache-kafka-streams-comparison-guideline-users/)
8. One major advantage of Kafka Streams is that its processing is Exactly Once end to end.
9. Spark streaming supports Stream joins, internally uses rocksDb for maintaining state.
10. Samza is kind of scaled version of Kafka Streams. While Kafka Streams is a library intended for microservices , Samza is full fledge cluster processing which runs on Yarn.
    1. Very good in maintaining large states of information (good for use case of joining streams) using rocksDb and kafka log.
11. One important point to note, if you have already noticed, is that all native streaming frameworks like Flink, Kafka Streams, Samza which support state management uses RocksDb internally. RocksDb is unique in sense it maintains persistent state locally on each node and is highly performant. It has become crucial part of new streaming systems.
12. As a summary, the core part is that Flink implements its algorithms not against Java objects, arrays, or lists, but actually against a data structure similar to java.nio.ByteBuffer. Flink uses its own specialized version, called MemorySegment on which algorithms put and get at specific positions ints, longs, byte arrays, etc, and compare and copy memory. The memory segments are held and distributed by a central component (called MemoryManager) from which algorithms request segments according to their calculated memory budgets.

##### Use-case
1. Complex Event processing (CEP) - Search for pattern across incoming events. Solutions in market exist.
2. Stream analytics - P99 response time in the last 1 minute. Storm, Flink, Spark streaming, Kafka streaming frameworks aimed at stream analytics.
3. Materialized view maintenance i.e Table-Table join. Log compaction useful for maintaining table. Twitter timeline maintenance is example. Use local tables to lookup and update the cache/view.
4. Filtering events.

Stream processing is a data management technique where as actor model is a distributed modules communication/coordination technique. Actor model communication is ephemeral i.e events not stored. Stream processing using actor model is not fault tolerant.

#### CDC
change data capture (CDC), which is the process of observing all data changes written to a database and extracting them in a form in which they can be replicated to other systems.

#### Even sourcing
In event sourcing, the application logic is explicitly built on the basis of immutable events that are written to an event log. In this case, the event store is append-only, and updates or deletes are discouraged or prohibited. Events are designed to reflect things that happened at the application level, rather than low-level state changes.
#### problems with event sourcing
1. Operations like compare and set cannot be performed. Claiming username. Use CDC with transactional features for this use-case.
2. Eventual consistency. Dangling references due to replication lag.

#### Diff between stream processing and batch processing
1. Stream processing -- events not bounded by time, continuous stream of input, Batch processing - Fixed data
2. Stream processing results expected near real time, batch results not expected near real time.
3. Stream processing continuous output - fraud detection, batch on off output - reports, search indexes
4. Fault tolerance
   1. Batch - better fault tolerance
   2. Stream - micro-batching and checkpointing techniques.