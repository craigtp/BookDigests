# Book Digest: Designing Data-Intensive Applications : The Big Ideas Behind Reliable, Scalable, and Maintainable Systems

Title     : Designing Data-Intensive Applications : The Big Ideas Behind Reliable, Scalable, and Maintainable Systems  
Author(s) : Martin Kleppmann  
ISBN-10   : 1449373321  
ISBN-13   : 978-1449373320  

## Chapter 1 - Reliable, Scalable & Maintainable Applications

Key Concepts of Data-Intensive Applications:

- Functional vs. Non-Functional Requirements:
  - Functional: What the application should do (data storage, retrieval, search, processing)
  - Non-Functional: General properties (security, reliability, compliance, scalability, compatibility, maintainability)
- Focus on Reliability:
  - Ensures systems work correctly despite faults (hardware, software, human error)
  - Fault-tolerance techniques hide certain faults from the user.
- Scalability for Growing Demands:
  - Strategies to maintain performance under increasing load
  - Requires quantifiable measures of load (e.g., Twitter timelines) and performance (e.g., response time percentiles)
  - Scalable systems add processing capacity to stay reliable under high load.
- Maintainability for Easier Management:
  - Reduces complexity for engineers and operations teams
  - Achieved through good abstractions, operability (system health visibility and management), and adaptability (modification for new uses).
- Patterns and Techniques for Success:
  - No single solution, but recurring patterns and techniques exist for building reliable, scalable, and maintainable applications.

## Chapter 2 - Data Models & Query Languages
- Various Data Models Exist: We explored a broad range of models, but details were limited due to their vast number.
- Hierarchical vs. Relational Model:
  - Hierarchical: Represents data as a tree structure (good for simple relationships).
  - Relational: Designed to handle complex relationships not supported by the hierarchical model.
- NoSQL Databases - A Modern Approach: Introduced for applications where the relational model isn't ideal. Two main categories:
  - Document Databases: Ideal for self-contained data with infrequent document relationships.
  - Graph Databases: Designed for scenarios where anything can be linked to anything else.
- Document and Graph Databases: Flexibility Through Schema:
  - Often lack a strict schema (data structure definition), allowing for easier adaptation to changing needs.
  - Applications likely still have an assumed data structure, with the schema being implicit (understood during read) or explicit (enforced during write).
- Unique Query Languages for Each Model: Every data model uses its own query language or framework. Examples include SQL, MapReduce, MongoDB's aggregation pipeline, Cypher, - SPARQL, Datalog, CSS, and XSL/XPath (some with interesting similarities to database query languages).
- Data Models Beyond Our Coverage: Many other data models exist, including:
  - Genome data analysis (e.g., GenBank)
  - Particle physics data analysis (custom solutions at LHC scale)
  - Full-text search (often used alongside databases)

## Chapter 3 - Storage & Retrieval
- Storage Engines: Two Main Categories
  - OLTP (Optimized for Transactions): Handles high volume user requests with small data access per query (indexes used for fast retrieval based on key). Disk seek time is a - bottleneck.
  - OLAP (Optimized for Analytics): Handles lower volume, demanding queries that scan millions of records (column-oriented storage for compact data encoding). Disk bandwidth is a - bottleneck.
- OLTP Storage Engine Philosophies
  - Log-structured: Append-only writes with file deletion (efficient for writes due to sequential disk access). Examples: LevelDB, Cassandra, HBase.
  - Update-in-place: Overwrites data within fixed-size disk pages. Examples: B-trees (used in most relational and non-relational databases).
- Column-Oriented Storage for OLAP Efficiency
  - Minimizes data retrieved from disk during scans by storing data in columns instead of rows.
- Benefits of Understanding Storage Engines
  - Informed decisions on choosing the right database tool for your application.
  - Ability to predict the impact of adjusting database tuning parameters.
  - Improved comprehension of database documentation.

## Chapter 4 - Encoding & Evolution
- Impact of Data Encoding:
  - Efficiency: Affects data processing speed.
  - Architecture & Deployment: Influences application design and deployment strategies.
- Rolling Upgrades and Evolvability:
  - Gradual deployment of new application versions.
  - Enables frequent releases and reduces downtime risk.
  - Crucial for evolvability (ease of application modification).
- Data Encoding and Compatibility During Upgrades:
  - Different code versions might run on different nodes.
  - Data encoding needs to ensure:
    - Backward compatibility (new code reads old data).
    - Forward compatibility (old code reads new data).
- Data Encoding Formats and Compatibility:
  - Programming Language-Specific:
    - Limited to one language.
    - Often lacks compatibility.
  - Textual Formats (JSON, XML, CSV):
    - Widely used, but compatibility depends on usage.
    - Optional schema languages can be helpful or hinder interoperability.
    - Vague about data types (caution with numbers and binary data).
  - Binary Schema-Driven Formats (Thrift, Protocol Buffers, Avro):
    - Compact and efficient encoding with clear compatibility rules.
    - Schemas useful for documentation and code generation.
    - Requires data decoding before human consumption.
- Data Encoding in Dataflow Scenarios:
  - Databases: Encoding during write, decoding during read.
  - RPC/REST APIs: Client encodes request, server decodes/encodes response, client decodes response.
  - Asynchronous Messaging: Messages encoded by sender, decoded by receiver.
- Conclusion: Careful data encoding planning enables backward/forward compatibility and smooth rolling upgrades.

## Chapter 5 - Replication
- Replication Purposes:
  - High availability: Maintain system functionality during machine/datacenter outages.
  - Disconnected operation: Allow application function during network interruptions.
  - Reduced latency: Geographically closer data copies for faster user interaction.
  - Scalability: Enable handling higher read volume by distributing reads across replicas.
- Challenges of Replication:
  - Concurrency control: Ensuring consistent data updates despite simultaneous modifications.
  - Fault tolerance: Addressing issues like unavailable nodes, network problems, and data corruption.
- Three Main Replication Approaches:
  - Single-leader: Writes to a single leader, data changes then sent to followers (reads from any replica, but follower data may be outdated). Easy to understand but lacks - robustness.
  - Multi-leader: Writes to any of multiple leader nodes, leaders propagate changes to each other and followers (more robust but complex and offers weaker consistency).
  - Leaderless: Writes to multiple nodes, reads from multiple nodes simultaneously (most robust but complex and offers weak consistency).
- Synchronous vs. Asynchronous Replication:
  - Synchronous: Write confirmed only after successful update on all replicas (slower but ensures data consistency).
  - Asynchronous: Faster write performance but risks data loss during failures (e.g., promoting an out-of-sync replica to leader).
- Replication Lag and Consistency Models:
  - Replication lag: Time difference between leader and follower data.
  - Consistency models: Guidelines for application behavior under replication lag.
    - Read-after-write consistency: Users always see their own writes.
    - Monotonic reads: Users don't see older data after seeing newer data.
    - Consistent prefix reads: Users see data in a logical sequence (e.g., question and answer).
- Concurrency and Conflict Resolution:
  - Multi-leader and leaderless approaches can encounter concurrent write conflicts.
  - Algorithms determine write order and methods resolve conflicts (e.g., merging updates).

## Chapter 6 - Partitioning
- Purpose of Partitioning: Efficient storage and processing of massive datasets across multiple machines.
- Goal: Balanced distribution of data and queries to avoid overloaded nodes (hot spots).
- Choosing a Partitioning Scheme:
  - Key-range partitioning: Sorts keys and assigns a range of keys to each partition.
    - Advantages: Efficient range queries.
    - Disadvantages: Risk of hot spots for frequently accessed key ranges.
    - Rebalancing: Dynamic splitting of ranges when partitions grow too large.
  - Hash partitioning: Applies a hash function to each key to assign a partition based on the hash value.
    - Advantages: Potentially even load distribution.
    - Disadvantages: Inefficient range queries due to loss of key order.
    - Rebalancing: Moving entire partitions between nodes when adding/removing nodes. Dynamic partitioning is also possible.
- Hybrid Partitioning: Combines approaches (e.g., using a compound key for partitioning and sorting).
- Partitioning and Secondary Indexes:
  - Requires partitioned secondary indexes as well.
  - Two main methods:
    - Document-partitioned indexes (local indexes):
      - Advantages: Only updates single partition on write.
      - Disadvantages: Requires scatter/gather across partitions when reading secondary index.
    - Term-partitioned indexes (global indexes):
      - Advantages: Serves reads from a single partition.
      - Disadvantages: Requires updates to potentially multiple partitions on write.
- Routing Queries to Partitions: Techniques range from basic load balancing to complex parallel query execution engines.
- Partitioned Database Scalability: Each partition operates mostly independently, enabling horizontal scaling.
- Challenge of Writes Spanning Multiple Partitions: Handling scenarios with writes succeeding in some partitions but failing in others (addressed in future chapters).

## Chapter 7 - Transactions
- Transactions: Abstraction for Simplified Data Management
  - Hides concurrency problems and hardware/software faults.
  - Simplifies error handling through transaction abort and retry.
- Benefits of Transactions:
  - Reduced need to consider various error scenarios (crashes, network issues, power outages, etc.).
  - Mitigates data inconsistencies, especially for complex data access patterns.
- Transactions and Concurrency Control:
  - Ensures consistent data state despite concurrent access by multiple users.
  - Different isolation levels provide varying degrees of protection against race conditions (inconsistencies caused by concurrency).
- Common Race Conditions (and How Transactions Address Them):
  - Dirty Reads (Prevented by Read Committed and Stronger Levels): Reading uncommitted data written by another client.
  - Dirty Writes (Prevented by Most Transaction Implementations): Overwriting another client's uncommitted write.
  - Read Skew (Non-repeatable Reads): Seeing different data snapshots during a transaction (Prevented by Snapshot Isolation using MVCC).
  - Lost Updates: Concurrent modifications overwriting each other (Some Snapshot Isolation or Manual Locking with SELECT FOR UPDATE).
  - Write Skew: Basing a write decision on outdated data (Only Serializable Isolation Prevents).
  - Phantom Reads: Reads affected by concurrent writes (Snapshot Isolation helps, but special mechanisms address write skew phantoms).
- Isolation Levels and Responsibility:
  - Weaker levels require manual handling of some anomalies (e.g., explicit locking).
  - Serializable offers strongest protection but can impact performance.
- Serializable Transaction Implementation Approaches:
  - Serial Execution: Simple but suitable only for very fast transactions with low throughput.
  - Two-Phase Locking: Traditional approach but can have performance drawbacks.
  - Serializable Snapshot Isolation (SSI): Newer, optimistic approach with fewer downsides.
- Transactions and Data Models: Valuable for various data models, not just relational.

## Chapter 8 - The Trouble With Distributed Systems
- Unreliable Network: Packet loss, delays, make it uncertain if messages are received or not.
- Unreliable Clocks: Significant clock skew, jumps, make time-based decisions unreliable.
- Unreliable Processes: Processes can pause/crash/restart unexpectedly.
- Partial Failures are Defining Characteristic: Must design systems to tolerate these failures for continued operation.
- Fault Detection Challenges:
  - No perfect mechanism to detect node failures.
  - Timeouts used but can't differentiate network vs. node failures.
  - Degraded nodes (e.g., slow network) can be harder to handle than failed nodes.
- Making Systems Tolerate Faults is Difficult:
  - No shared memory or global knowledge between nodes.
  - Decisions require communication and agreement between nodes (quorum).
- Shifting from Idealized Single-Machine Development: Deterministic behavior on a single machine vs. the messy reality of distributed systems.
- Distributed Systems vs. Single Machine: Avoid distributed systems if possible (keep things on a single machine for simplicity).
- Reasons to Use Distributed Systems:
  - Scalability
  - Fault tolerance
  - Low latency (geographically close data)
- Network/Clock/Process Unreliability Not Immutable: Real-time guarantees and bounded delays are achievable but expensive (most systems choose cheap over reliable).
- Supercomputers vs. Distributed Systems: Supercomputers halt entirely on component failures, while distributed systems can theoretically run forever with node-level maintenance.

## Chapter 9 - Consistency & Consensus
- Linearizability: Popular consistency model mimicking a single data copy with atomic operations.
  - Advantages: Easy to understand (like a single-threaded variable).
  - Disadvantages: Slow, especially in high-latency networks.
- Causality: Weaker consistency model with ordering based on cause-and-effect.
  - Advantages: Less overhead than linearizability, less sensitive to network issues.
  - Details: Allows for concurrent operations resulting in branching/merging version history.
- Lamport Timestamps and Limitations: Used for causal ordering but insufficient for certain tasks (e.g., ensuring unique usernames during concurrent registrations).
- Consensus: Reaching agreement on a decision across all nodes, with an irrevocable outcome.
- Problems Reducible to Consensus:
  - Linearizable compare-and-set registers
  - Atomic transaction commit
  - Total order broadcast
  - Locks and leases
  - Membership/coordination service
  - Uniqueness constraints
- Single-Leader Approach: Centralized decision-making for efficiency (e.g., linearizable databases).
  - Limitations: Vulnerable to leader failure or network disruptions causing system stalls.
- Handling Leader Failures:
  1. Wait for recovery (blocks system progress).
  2. Manual failover by human intervention (slow).
  3. Automatic leader election using a consensus algorithm (recommended).
- Consensus and Single-Leader Systems: Consensus is still required for leader maintenance/changes, even if not for every write operation.
- Fault-Tolerant Consensus Algorithms: Exist and can be used to build robust systems.
- ZooKeeper: Provides outsourced consensus, failure detection, and membership services.
- Alternatives to Consensus: Leaderless/multi-leader replication may tolerate eventual inconsistencies (branching version histories) forgoing linearizability.
- Value of Theory in Distributed Systems:
  - Theoretical research informs practical work.
  - Helps define what's achievable/impossible in distributed systems.
  - Provides insights into potential flaws of distributed systems.

## Chapter 10 - Batch Processing
- Design Principles:
  - Immutable inputs.
  - Outputs intended for further processing by other programs.
  - Complex problems solved by composing small, single-purpose tools.
- Uniform Interface:
  - Unix: Files and pipes.
  - MapReduce and Dataflow Engines: Distributed file system (usually HDFS for initial input and final output).
  - Dataflow Engines: Additional in-memory data transport mechanisms.
- Two Main Problems:
  - Partitioning:
    - MapReduce: Group related data (by key) together using mappers and repartitioned reducers.
    - Dataflow Engines: Similar approach but avoid sorting unless necessary.
  - Fault Tolerance:
    - MapReduce: Frequent writes to disk for easy recovery but slower execution.
    - Dataflow Engines: Less data written to disk, more in-memory, requires recomputation on failures. Deterministic operators reduce recomputation.
- Join Algorithms:
  - Sort-merge joins: Sort and merge based on join key to bring matching records together.
  - Broadcast hash joins: One small input is loaded entirely into a hash table. Mappers for large input can query the hash table for each record.
  - Partitioned hash joins: Similar to broadcast hash joins but using partitioned data (same key, hash function, number of partitions).
- Restricted Programming Model:
  - MapReduce and dataflow engines hide complexities: fault tolerance, retries, discarded outputs from failed tasks.
  - Code focuses on core logic (mappers/reducers) without implementing fault tolerance mechanisms.
- Batch Processing Job Characteristics:
  - Reads input data, produces output data, without modifying the input (output derived from input).
  - Bounded input data (known, fixed size).
  - Job finishes reading input and eventually completes.

## Chatper 11 - Stream Processing
- Concept: Continuously processing unbounded (never-ending) streams of data, similar to batch processing but on ongoing data.
- Message Brokers: Streaming equivalent of a file system.
- Two Main Types of Message Brokers:
  - AMQP/JMS-style:
    - Asynchronous RPC style.
    - Individual message assignment and acknowledgement.
    - Message deletion after acknowledgement (ideal for task queues, order not important).
  - Log-based:
    - Partitioned message delivery for parallelism.
    - Order-preserving delivery within partitions.
    - Consumers track progress with checkpoints (offset of last processed message).
    - Message persistence for replaying old messages.
- Data Sources as Streams:
  - User activity events
  - Sensor readings
  - Data feeds (e.g., market data)
  - Database writes (changelogs through change data capture or event sourcing)
- Benefits of Representing Databases as Streams:
  - Continuously update derived data systems (search indexes, caches, analytics)
  - Build new data views by replaying historical changes
- Stream Processing Techniques:
  - Maintaining state as streams
  - Replaying messages
  - Stream joins (stream-stream, stream-table, table-table)
- Purposes of Stream Processing:
  - Complex event processing (searching for event patterns)
  - Stream analytics (computing windowed aggregations)
  - Materialized view updates (keeping derived data systems up-to-date)
- Challenges of Reasoning About Time in Stream Processing:
  - Processing time vs. event timestamps
  - Handling straggler events (arriving late after window closure)
- Types of Joins in Stream Processing:
  - Stream-stream joins (finding related events within a time window)
  - Stream-table joins (enriching activity events with database lookups)
  - Table-table joins (creating materialized views by joining changelogs)
- Fault Tolerance and Exactly-Once Semantics:
  - Discarding partial outputs from failed tasks.
  - Fine-grained recovery mechanisms: microbatching, checkpointing, transactions, or idempotent writes.

## Chapter 12 - The Future Of Data Systems
- Multiple Tools for Different Tasks: No single tool fits all use cases, so compose various software pieces for an application.
- Data Integration with Batch Processing and Streams: Data changes flow between systems using batch processing and event streams.
- Systems of Record and Derived Data:
  - Systems of record store authoritative data.
  - Derived data is transformed from systems of record (indexes, views, machine learning models, etc.).
- Benefits of Asynchronous and Loosely Coupled Data Processing:
  - Increased system robustness and fault tolerance (problems isolated).
  - Easier application evolution (changes trigger data re-derivation).
  - Data processing similar to internal database operations.
- Dataflow Applications as Unbundled Databases: Build applications by composing loosely coupled database components.
- Updating Derived State: Derived state updates based on underlying data changes, can be further consumed by downstream systems.
- Dynamic User Interfaces: Dataflow can extend to user interfaces for real-time updates and offline functionality.
- Ensuring Correctness with Faults:
  - Scalable integrity with asynchronous event processing.
  - Idempotent operations using end-to-end identifiers.
  - Asynchronous constraint checks (clients wait or proceed at risk).
  - More scalable and robust than traditional distributed transactions.
- Benefits of Dataflow and Asynchronous Constraint Checking:
  - Avoids complex coordination.
  - Maintains data integrity with good performance even in geographically distributed systems with faults.
- Data Integrity Audits: Verify data integrity and detect corruption.
- Ethical Considerations of Data-Intensive Applications:
  - Data can be misused (biased decisions, discrimination, surveillance, privacy breaches).
  - Unintended consequences of well-intentioned data use.
- Software Engineers' Responsibility: Work towards a world that treats people with respect and humanity.

