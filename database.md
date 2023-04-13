#### Database selection guide
![Selection](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Ff5b7dcbd-a2b0-4677-8ffa-669acf91242b_1143x1600.jpeg)

Things to keep in my to select database
1. scalability
   1. Horizontal, vertical
   2. SQL database scaling is hard due to consistency requirements. Performance bottlenecks for large amount of data or high traffic workloads.
   3. NoSQL may sacrifice consistency for scalability.
2. performance
   1. Query efficiency and the balance between read and write performance should be considered.
   2. Some databases may be optimized for read-heavy workloads, while others may prioritize write performance.
   3. Response time for joins, complex queries
   4. Response time for simple queries
   5. SQL: As data volume and complexity increase, query performance may degrade.
   6. NoSQL databases may not be as efficient when it comes to complex queries or aggregations, as they lack the same level of support for SQL and structured schemas.
   7. NewSQL databases can be a good choice for applications that require both complex querying and high write performance.
3. data consistency
   1. PACELC, CAP theorems
   2. SQL strongly consistent
   3. NoSQL eventually consistent
4. data model
   1. Relational databases are well-suited for applications that require complex data relationships. They provide robust support for joins and referential integrity.
   2. NoSQL databases can be better suited for applications with more flexible data relationships, as they allow for more natural modeling of these structures.
5. security
   1. Authentication and Authorization
   2. Managing user accounts, roles, and permissions
   3. Relational databases, for instance, typically offer built-in support for role-based access control.
   4. Strong encryption algorithms, such as AES-256, can help prevent unauthorized access to data even if it is intercepted or compromised. Some databases also offer additional data protection features, such as data masking or redaction, which can help protect sensitive information from being inadvertently exposed in logs or query results.
   5. it is essential to consider not only the built-in security mechanisms but also the ease of integrating with existing security infrastructure, such as identity providers, firewalls, and intrusion detection systems.
6. cost
   1. Some databases, like MySQL and PostgreSQL, are open-source and can be used without incurring licensing fees, while others, such as Oracle and Microsoft SQL Server, require paid licenses.
   2. Hosting fees can also differ based on the deployment model we choose, whether it is self-hosted, cloud-based, or managed by a third-party provider.
   3. Maintenance and management costs are equally important to consider. They can significantly impact the total cost of ownership (TCO) of a database. These costs include hardware and software upgrades, staff training, and the effort required to maintain, troubleshoot, and optimize the database.
7. community support
   1. They can significantly impact the ease of adoption, integration, and ongoing support for the chosen database.
   2. A strong community can provide valuable resources, such as documentation, tutorials, and forums, while a robust ecosystem can offer integration with other technologies, tools, and services.
   3. A well-established community can provide a wealth of knowledge and experience. It makes it easier to troubleshoot issues, learn best practices, and optimize the database's performance. When evaluating a database, consider the availability of documentation, tutorials, and support channels, such as forums, mailing lists, and chat platforms.
8. Ecosystem - i.e integrations with other tools.
   1. A database with a robust ecosystem will typically offer pre-built connectors, libraries, and tools for working with various programming languages, frameworks, and services. This compatibility can streamline development and simplify the process of incorporating the database into the existing technology stack.


### SQL databases
![](https://substackcdn.com/image/fetch/f_auto,q_auto:good,fl_progressive:steep/https%3A%2F%2Fsubstack-post-media.s3.amazonaws.com%2Fpublic%2Fimages%2Fb5d5235c-260c-4cf6-969b-efa2af2265bb_1600x402.png)
##### Advantages
- Transactions
  - ACID properties
  - Relationship and referential integrity
  - Indexing
  - Query optimization
- SQL support. Complex queries support
- Structured data, predefined schema
##### Drawbacks
- Limited scalability, Challenging to scale horizontally.
- Schema migration difficulty
- Performance issues when the data grows significantly.
- Inefficient for unstructured data

Relational databases usually provide efficient querying capabilities due to their structured schema and support for SQL. Their performance is often optimized for complex queries involving joins and aggregations. However, as data volume and complexity increase, query performance may degrade, especially when dealing with large datasets.
However, NoSQL databases may not be as efficient when it comes to complex queries or aggregations, as they lack the same level of support for SQL and structured schemas.
Relational databases are generally better for applications requiring strict data consistency and complex queries, while NoSQL databases are more suitable for projects dealing with large volumes of unstructured data or requiring high scalability.

### [NoSQL](https://blog.bytebytego.com/p/understanding-database-types?utm_source=post-email-title&publication_id=817132&post_id=115767917&isFreemail=false&utm_medium=email)
[Motivations for NoSQL](https://en.wikipedia.org/wiki/NoSQL)
1. Simple design
2. Simple horizontal scaling
3. Schema flexibility
4. Custom data models and fast operations.

Scalability, data modeling, query patterns, and performance to determine the best fit. NoSQL databases types given below.
1. key value stores - Redis, Riak, RocksDB, DynamoDB
   1. High read/write throughput
   2. Horizontal scalability
   3. Caching layers, session stores, configuration stores.
   4. Low-latency access i.e gaming platforms, real-time analytics systems, recommendation engines.
   5. Key-value databases are efficient for session-oriented applications. Session oriented-applications, such as web applications, store users’ data in the main memory or in a database during a session. This data may include user profile information, recommendations, targeted promotions, discounts, and more.
2. Wide column stores or column family stores - Cassandra, HBase, BigTable
   1. Column-based databases are designed for applications that need to store and query large amounts of data across many nodes
   2. Analytical application, high read/write throughput apps.
3. Document/Object databases - MangoDB, CosmosDB, Couchbase
   1. JSON, BSON documents
   2. Flexible/dynamic schema, easy to evolve data
   3. Good for nested datastructures
   4. Content management systems, e-commerce platforms andd analytics applications
4. Graph databases - 
   1. Powerful query capabilities for traversing and analysing interconnected data.
   2. Intricate relations between entities
   3. Nodes, edges - efficient processing of complex relationships, traversals, graph algorithms.
   4. Social networks, fraud detection systems, recommendation engines.

#### NoSQL drawbacks
1. Lack of standardisation: NoSQL no standardisation of query languages or APIs. Hard to migrate to a different NoSQL system.
2. Generally NoSQL systems provide weak consistency.
3. Limited support for transactions and complex queries in NoSQL databases.

### NewSQL
- A modern approach to combining the strengths of both relational and NoSQL databases.
- relational model, ACID properties, and SQL support, while offering improved scalability, distributed architecture, and performance enhancements.
- Distributed architecture i.e partitioning and replication
- Scalability - horizontal scalability,
- strong consistency, support for high volume of transactions.
- Concurrency control - MVCC, Optimistic concurrency control
- SQL for querying, compatibility with existing relational database tools
- Config, maintenance, troubleshooting complexity
- Vendor lock in
- Lack of maturity
- CockroachDB, Spanner, TiDB
- When considering a NewSQL database, it is essential to evaluate the specific needs of the application in terms of scalability, data consistency, performance, and developer familiarity to determine the best fit.
- Often employ innovative techniques, such as distributed query processing and advanced indexing, to deliver high-performance querying and write capabilities. As a result, NewSQL databases can be a good choice for applications that require both complex querying and high write performance.

### Time series database
1. Time series data
2. High write and query performance. Handles high velocity data streams.
3. Data compression to reduce storage space and increase query performance.
4. Time based data retention policies
5. Built in time series functions i.e aggregation, down sampling, forecasting etc.
6. Horizontal scalability
7. InfluxDB and timescale DB

Columnar or column oriented - store each column separately in a file.
1. Good for analytical processing. 
2. Table consists of several columns. 
3. Query requires 4 or 5 columns. 
4. CPU cache is not filled with useless data. 
5. All the required values will be in cache one after another allowing for vector processing in CPUs. 
6. Allows for compression of data using techniques like run-length encoding.
7. While storing, sort the data by primary column, secondary column and so on.
8. Sorting improves the run length compression efficiency.
9. Used in RedShift, Parquet, RedShift

Wide column store with column families - Each family of columns stored together just like in the relational databases.
1. Used in Hbase, Cassandra, BigTable.

#### Serverless database
Amazon Aurora serverless database
- Compute, storage and router layers. Storage is decoupled from compute.
- Scales capacity automatically up and down according to the load.
- Provisioned and serverless instances can coexist for a database.

#### CAP and PACELC
The PACELC theorem states that if a system is Partition tolerant, it must choose between Availability and Consistency during a network partition and between Latency and Consistency when the network is operating normally. This theorem highlights the trade-offs that databases must make when it comes to consistency and can be a useful tool for understanding the consistency model of various database types.


For some applications, such as financial transactions, strong consistency is essential to ensure data integrity and avoid errors. In contrast, for other applications, like social media feeds or search indexes, eventual consistency may be sufficient, as temporary inconsistencies are less likely to negatively impact the user experience.

#### MySQL vs PostgreSQL
Difference areas: Feature set(data model, language(strong stored procedure support), index types), indexing & storage data structures storage and performance, concurrency control algorithms choice.
1. PostgreSQL offers good performance with read and writes, mySQL offers good read only performance. Performance difference might be visible with huge data???
2. PostgreSQL offers MVCC concurrency control. MVCC offers good performance for some kind of applications.
   1. PostgresSQL implementation of repeatable-read isolation level prevents lost updates. MySQL repeatable read isolation level doesn't detect/rollback lost updates.
   2. Bot PostgresSQL and mySQL support repeatable read.
3. Postgres offers object relational model. Postgres supports table inheritance, support for XML, JSON. Supports hstore, tdata advanced data types.
4. Postgres offers different types of indexes Hash, GIN etc..
   1. Clustered indices, secondary indexes point to primary indices in MySQL. MySQL uses clustered indices.
   2. Locking performance
5. No easy way to figure out the performance of both of the databases through algorithms inside. Need to determine through empirical testing.
6. References
   1. https://www.ibm.com/cloud/blog/postgresql-vs-mysql-whats-the-difference
7. MySQL column addColumn, dropColumn operation takes table lock

### References
1. See [this](https://cloud.google.com/products/databases) for use-cases.
