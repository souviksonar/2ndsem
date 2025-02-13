

#flashcards/Distributed_Databases_Overview
QUESTION:  What are the key differences between homogeneous and heterogeneous distributed databases?
OPTIONS:
A) Homogeneous databases use the same schema and software at all sites, while heterogeneous databases may use different schemas and software.
B) Homogeneous databases are always faster than heterogeneous databases.
C) Heterogeneous databases are simpler to manage than homogeneous databases.
D) Homogeneous databases can only use replication, while heterogeneous databases can only use fragmentation.
??
SOLUTION:
A) Homogeneous databases use the same schema and software at all sites, enabling easier management and querying. Heterogeneous databases, on the other hand, can have varying schemas and software, making query and transaction processing more complex due to the need for translation and coordination between different systems. Options B, C, and D are incorrect generalizations or mischaracterizations.
<!--SR:!2025-02-16,4,270-->

#flashcards/Data_Replication
QUESTION:  What is "full replication" in a distributed database, and what is one advantage and one disadvantage of this approach?
OPTIONS:
A) Full replication means storing data at only one site; Advantage: Simplicity; Disadvantage: Single point of failure.
B) Full replication means storing the relation at all sites; Advantage: High availability; Disadvantage: Increased update cost.
C) Full replication means partitioning the relation across all sites; Advantage: Reduced storage cost; Disadvantage: Complex query processing.
D) Full replication means storing data only at the primary site; Advantage: Easy concurrency control; Disadvantage: Low availability.
??
SOLUTION:
B) Full replication means storing the relation at all sites.  An advantage is high availability because if one site fails, the data is still accessible from other sites. A disadvantage is the increased cost of updates, as every replica must be updated.
<!--SR:!2025-02-16,4,270-->

#flashcards/Data_Fragmentation
QUESTION: Explain the difference between horizontal and vertical fragmentation. Provide an example SQL expression using the `account` relation (with attributes `branch_name`, `account_number`, `balance`) that demonstrates horizontal fragmentation.
OPTIONS:
A) Horizontal fragmentation divides the schema; Vertical fragmentation divides the tuples.  Example: `SELECT * FROM account WHERE balance > 1000`
B) Horizontal fragmentation divides the tuples; Vertical fragmentation divides the schema. Example: `SELECT branch_name, account_number FROM account`
C) Horizontal fragmentation divides the tuples; Vertical fragmentation divides the schema. Example: `SELECT * FROM account WHERE branch_name = 'Downtown'`
D) Horizontal fragmentation divides the schema; Vertical fragmentation divides the tuples. Example:  `CREATE VIEW v_account AS SELECT account_number, balance FROM account`
??
SOLUTION:
C) Horizontal fragmentation divides the tuples based on a condition; Vertical fragmentation divides the schema (columns). The example `SELECT * FROM account WHERE branch_name = 'Downtown'` correctly demonstrates horizontal fragmentation by selecting tuples based on the `branch_name` attribute.
<!--SR:!2025-02-16,4,270-->

#flashcards/Data_Transparency
QUESTION:  What are the three types of data transparency mentioned in the context of distributed databases?
OPTIONS:
A) Location, Fragmentation, and Security Transparency
B) Fragmentation, Replication, and Location Transparency
C) Network, Hardware, and Software Transparency
D) Performance, Scalability, and Availability Transparency
??
SOLUTION:
B) The three types of data transparency are Fragmentation Transparency (users are unaware of how data is fragmented), Replication Transparency (users are unaware of data replication), and Location Transparency (users are unaware of the physical location of data).
<!--SR:!2025-02-16,4,270-->

#flashcards/Naming_Schemes
QUESTION: What are the four criteria for naming data items in a distributed database system?
OPTIONS:
A) Unique names, efficient location finding, transparent location changes, autonomous data item creation.
B) Short names, memorable names, centralized naming, replicated names.
C) Global names, local names, aliases, fragmentation transparency.
D) Replication transparency, location transparency, fragmentation transparency, security transparency.
??
SOLUTION:
A) The four criteria are: 1. Every data item must have a system-wide unique name. 2. It should be possible to find the location of data items efficiently. 3. It should be possible to change the location of data items transparently. 4. Each site should be able to create new data items autonomously.

#flashcards/Centralized_Name_Server
QUESTION:  What is a significant disadvantage of using a centralized name server in a distributed database?
OPTIONS:
A) It simplifies name resolution.
B) It enhances data availability.
C) It creates a single point of failure and a potential performance bottleneck.
D) It allows for autonomous data item creation at each site.
??
SOLUTION:
C) A centralized name server is a single point of failure. If it goes down, the entire system's ability to locate data items is compromised. It can also become a performance bottleneck as all name resolution requests must go through it.

#flashcards/Aliases
QUESTION: How do aliases help achieve network transparency in a distributed database system where each site prefixes its own identifier to names?
OPTIONS:
A) Aliases create shorter names for data items.
B) Aliases map user-friendly names to the actual, site-prefixed names, hiding the physical location from the user.
C) Aliases replicate data items across multiple sites.
D) Aliases fragment data items across multiple sites.
??
SOLUTION:
B) Aliases provide a layer of abstraction. Users can refer to data items using aliases, and the system maps these aliases to the real, site-specific names. This hides the physical location of the data and allows for data movement without affecting user queries.

#flashcards/Distributed_Transactions
QUESTION:  What are the responsibilities of a local transaction manager in a distributed database system?
OPTIONS:
A) Starting all transactions in the system.
B) Maintaining a log for recovery and coordinating concurrent execution of transactions at its site.
C) Coordinating the termination of all transactions.
D) Distributing subtransactions to appropriate sites.
??
SOLUTION:
B) The local transaction manager is responsible for managing transactions *at its site*. This includes maintaining a log for recovery purposes and coordinating the concurrent execution of transactions executing at that site.

#flashcards/Transaction_Coordinator
QUESTION: What is the role of the transaction coordinator in a distributed transaction?
OPTIONS:
A) To maintain the local log at each site.
B) To execute all subtransactions.
C) To initiate transactions, distribute subtransactions, and coordinate the termination (commit or abort) of transactions originating at its site.
D) To resolve all deadlocks in the system.
??
SOLUTION:
C) The transaction coordinator has a system-wide (for that transaction) role. It starts transactions that originate at its site, distributes subtransactions to other sites for execution, and crucially, coordinates the termination of the transaction, ensuring that it either commits at all participating sites or aborts at all sites.

#flashcards/System_Failure_Modes
QUESTION:  Besides site failure, what are other failure modes unique to distributed systems?
OPTIONS:
A) Hardware failure and software bugs
B) Loss of messages, communication link failure, and network partition.
C) Power outage and disk crash
D) Database corruption and transaction rollback.
??
SOLUTION:
B) Loss of messages, communication link failure and network partition are unique issues for distributed systems, as they relate to the distributed nature of communication and coordination.

#flashcards/Two_Phase_Commit_2PC
QUESTION: In the Two-Phase Commit (2PC) protocol, what happens during Phase 1 (the "prepare" phase)?
OPTIONS:
A) The coordinator decides whether to commit or abort the transaction.
B) The coordinator asks all participants to prepare to commit, and participants respond with "ready" or "abort".
C) All participants write their updates to disk.
D) The coordinator sends the final "commit" or "abort" message to all participants.
??
SOLUTION:
B) In Phase 1, the coordinator polls the participants, asking them if they are prepared to commit. Each participant then votes either "ready" (if it can commit) or "abort" (if it cannot).

#flashcards/Two_Phase_Commit_2PC_Phase2
QUESTION: What happens if the coordinator in 2PC receives at least one "abort" message during Phase 1?
OPTIONS:
A) It immediately commits the transaction.
B) It retries the transaction.
C) It aborts the transaction and informs all participants.
D) It waits for a timeout and then commits.
??
SOLUTION:
C) If even a single participant cannot commit (and thus sends "abort"), the entire transaction must be aborted to maintain atomicity. The coordinator will then send an "abort" message to all participants in Phase 2.

#flashcards/2PC_Coordinator_Failure
QUESTION:  What is the "blocking problem" in the context of 2PC and coordinator failure?
OPTIONS:
A) The coordinator blocks all other transactions.
B) Participants may have to wait indefinitely for a failed coordinator to recover to learn the transaction's outcome.
C) The network becomes blocked.
D) The database is blocked from accepting new transactions.
??
SOLUTION:
B) If the coordinator fails after participants have voted "ready" but before sending the final decision, the participants are blocked. They cannot unilaterally decide to commit or abort, as they don't know the global decision. They must wait for the coordinator to recover.

#flashcards/2PC_Site_Recovery
QUESTION: If a site participating in a 2PC transaction recovers and finds a `<ready T>` record in its log but no `<commit T>` or `<abort T>` record, what must it do?
OPTIONS:
A) It immediately commits transaction T.
B) It immediately aborts transaction T.
C) It consults the coordinator (or other sites if the coordinator is unavailable) to determine the fate of T.
D) It rolls back transaction T and restarts it.
??
SOLUTION:
C) The `<ready T>` record indicates that the site voted to commit but hasn't received the final decision. It must find out what the coordinator decided before proceeding.

#flashcards/Three_Phase_Commit_3PC
QUESTION: What is the primary advantage of the Three-Phase Commit (3PC) protocol over 2PC?
OPTIONS:
A) 3PC is simpler to implement.
B) 3PC is faster than 2PC.
C) 3PC avoids the blocking problem under certain failure conditions (assuming no network partitions).
D) 3PC eliminates the need for a coordinator.
??
SOLUTION:
C) 3PC introduces a "pre-commit" state, which allows non-failed sites to reach a decision even if the coordinator fails, provided that fewer than K sites fail. This reduces the blocking window.

#flashcards/Persistent_Messaging
QUESTION: Explain the concept of persistent messaging and its role in distributed transaction processing.
OPTIONS:
A) A way to send messages quickly across a network.
B) A method to guarantee message delivery exactly once, ensuring atomicity and durability in distributed operations.
C) A protocol for encrypting messages.
D) A technique for replicating messages across multiple sites.
??
SOLUTION:
B) Persistent messaging systems ensure that messages are delivered exactly once, even in the presence of failures. This is used as an alternative to 2PC in situations where blocking is unacceptable. It helps achieve atomicity by ensuring that either a message is delivered (and the corresponding action taken) or not sent at all.

#flashcards/Persistent_Messaging_Implementation
QUESTION: Describe the basic protocol used by a sending site in a persistent messaging system.
OPTIONS:
A) The sending site sends the message directly to the receiving site.
B) The sending site writes the message to a special relation (e.g., `messages_to_send`) and a delivery process monitors this relation, sending and retrying until acknowledged.
C) The sending site broadcasts the message to all sites.
D) The sending site encrypts the message and sends it to a central server.
??
SOLUTION:
B) The key is the use of a persistent store (the `messages_to_send` relation). This ensures that the message isn't lost if the sending site fails. The delivery process handles the reliable sending and retrying.

#flashcards/Persistent_Messaging_Receiving
QUESTION: How does a receiving site in a persistent messaging system ensure that a message is processed exactly once?
OPTIONS:
A) By sending an acknowledgment immediately upon receiving the message.
B) By adding the received message to a `received_messages` relation *within a transaction* and then sending an acknowledgment *after* the transaction commits.
C) By discarding duplicate messages based on timestamps.
D) By forwarding the message to another site.
??
SOLUTION:
B) The crucial part is the transaction. The message is added to the `received_messages` relation, and the acknowledgment is sent *only* after the transaction commits. This prevents the message from being processed multiple times if the receiving site crashes and recovers. Option A is unsafe. Option C is used for handling delayed messages, but not for ensuring exactly-once processing.

#flashcards/Concurrency_Control
QUESTION: Why is concurrency control necessary in a distributed database system?
OPTIONS:
A) To prevent data loss.
B) To improve query performance.
C) To ensure data consistency and isolation in the presence of concurrent transactions accessing shared data.
D) To simplify database administration.
??
SOLUTION:
C) The goal of concurrency control, whether in a centralized or distributed system, is to maintain the ACID properties of transactions, specifically consistency and isolation, when multiple transactions are running concurrently.

#flashcards/Single_Lock_Manager
QUESTION: What is a primary disadvantage of the single-lock-manager approach to distributed concurrency control?
OPTIONS:
A) It is difficult to implement.
B) It leads to frequent deadlocks.
C) The lock manager site becomes a single point of failure and a potential performance bottleneck.
D) It cannot handle replicated data.
??
SOLUTION:
C) Similar to the centralized name server, a single lock manager suffers from being a single point of failure and bottleneck.

#flashcards/Primary_Copy
QUESTION: In the primary copy approach to distributed locking, where are lock requests for a data item sent?
OPTIONS:
A) To all sites that store a replica of the data item.
B) To a randomly chosen site.
C) To the primary site that holds the primary copy of the data item.
D) To the site where the transaction originated.
??
SOLUTION:
C) The defining characteristic of the primary copy approach is that all lock requests for a given data item are directed to its designated primary site.

#flashcards/Majority_Protocol
QUESTION: In the majority protocol for distributed locking with replicated data, what condition must be met for a transaction to proceed?
OPTIONS:
A) It must obtain a lock on all replicas.
B) It must obtain a lock on at least one replica.
C) It must obtain a lock on a majority of the replicas.
D) It must obtain a lock from the transaction coordinator.
??
SOLUTION:
C) The majority protocol requires locking more than half of the replicas.  This ensures that conflicting operations cannot proceed concurrently on different sets of replicas.

#flashcards/Biased_Protocol
QUESTION:  How does the biased protocol differentiate between handling shared and exclusive locks in a distributed database?
OPTIONS:
A) Shared locks require locking all replicas, while exclusive locks require locking only one.
B) Shared locks require locking only one replica, while exclusive locks require locking all replicas.
C) Both shared and exclusive locks require locking all replicas.
D) Both shared and exclusive locks require locking only one replica.
??
SOLUTION:
B) The biased protocol optimizes for reads. Shared locks (for reading) can be obtained on any single replica, reducing overhead. Exclusive locks (for writing) require locking *all* replicas to maintain consistency.

#flashcards/Quorum_Consensus
QUESTION: Explain the conditions that must be satisfied by the read quorum ($Q_r$) and write quorum ($Q_w$) in the quorum consensus protocol, where $S$ is the total weight of all sites.
OPTIONS:
A) $Q_r + Q_w < S$ and $2 * Q_w < S$
B) $Q_r + Q_w > S$ and $2 * Q_w > S$
C) $Q_r + Q_w = S$ and $2 * Q_w = S$
D) $Q_r > S$ and $Q_w > S$
??
SOLUTION:
B) The conditions $Q_r + Q_w > S$ ensures that any read quorum intersects with any write quorum, guaranteeing that a read will see the latest written value. The condition $2 * Q_w > S$ ensures that two write operations cannot occur concurrently on different sets of replicas.

#flashcards/Timestamping
QUESTION: How are globally unique timestamps typically generated in a distributed database system?
OPTIONS:
A) By using a central time server.
B) By concatenating a locally unique timestamp with the site identifier.
C) By using a random number generator.
D) By using the transaction ID.
??
SOLUTION:
B) Concatenating a local timestamp (generated using a logical clock or local time) with the site ID ensures uniqueness across the entire distributed system.

#flashcards/Deadlock_Handling
QUESTION: Why is deadlock detection more complex in a distributed database system compared to a centralized one?
OPTIONS:
A) Distributed systems use different locking protocols.
B) Deadlocks cannot occur in distributed systems.
C) A global wait-for graph needs to be constructed, which requires communication and coordination between sites.
D) Distributed systems have fewer transactions.
??
SOLUTION:
C) Deadlocks can involve resources and transactions spread across multiple sites.  Detecting these distributed deadlocks requires constructing a global wait-for graph, which is more complex than maintaining a local wait-for graph in a centralized system.

#flashcards/Availability
QUESTION:  What does "high availability" mean in the context of distributed database systems?
OPTIONS:
A) The system is always available.
B) The system has a low mean time to failure (MTTF).
C) The time for which the system is not fully usable should be extremely low.
D) The system can handle a large number of concurrent users.
??
SOLUTION:
C) High availability means minimizing downtime. While a system can never be *always* available (100% uptime), a highly available system aims for very low periods of unavailability (e.g., "five nines" or 99.999% uptime).

#flashcards/Reconfiguration
QUESTION: What is a key challenge when a failed site recovers and needs to be reintegrated into a distributed database system?
OPTIONS:
A) The site's data is permanently lost.
B) The site must be completely rebuilt.
C) The site must catch up with all updates that occurred while it was down, potentially while other updates are still happening.
D) The site's IP address changes.
??
SOLUTION:
C) Reintegration requires bringing the recovered site's data up to date, which is complicated by the fact that the system may have continued to operate (and update data) while the site was down.

#flashcards/CAP_Theorem
QUESTION: According to Brewer's CAP Theorem, what are the three properties of a distributed system, and what is the core trade-off?
OPTIONS:
A) Consistency, Availability, and Performance; you can only have two.
B) Consistency, Availability, and Partition tolerance; you can only have two.
C) Concurrency, Atomicity, and Performance; you can only have two.
D) Centralization, Atomicity, and Partition tolerance; you can only have two.
??
SOLUTION:
B) The three properties are Consistency (all nodes see the same data at the same time), Availability (the system remains operational even with failures), and Partition tolerance (the system continues to operate despite network partitions). The theorem states that you can choose at most two of these. In the presence of partitions (which are inevitable in large distributed systems), you must choose between consistency and availability.

#flashcards/Eventual_Consistency
QUESTION: Briefly define "eventual consistency" in the context of distributed databases.
OPTIONS:
A) All replicas are always consistent.
B) Replicas may be temporarily inconsistent, but will eventually converge to a consistent state if updates stop.
C) The system uses a single master for all updates.
D) The system uses two-phase commit to ensure consistency.
??
SOLUTION:
B) Eventual consistency is a weaker consistency model where replicas are not guaranteed to be consistent at all times. However, if updates cease for a period, the system guarantees that all replicas will eventually converge to the same state.

Okay, here are 30 *new* questions based on the provided PDF, continuing with the same format and covering different aspects of the material:

#flashcards/Distributed_Query_Processing_Cost
QUESTION: In distributed query processing, what factors, beyond disk accesses, are considered when measuring the cost of a strategy?
OPTIONS:
A) CPU usage and memory consumption at a single site.
B) Network bandwidth and latency.
C) The cost of data transmission over the network and the potential for parallel processing.
D) The number of users connected to the system.
??
SOLUTION:
C) In a distributed system, the cost of transmitting data between sites (network communication) is a significant factor.  Also, the ability to execute parts of the query in parallel at different sites can impact overall performance and thus must be considered in the cost.

#flashcards/Query_Transformation_Horizontal
QUESTION: Given a relation `employee` horizontally fragmented into `employee1` (where `dept = 'Sales'`) and `employee2` (where `dept = 'Marketing'`), how would the query `SELECT * FROM employee WHERE dept = 'Sales'` be transformed?
OPTIONS:
A) `SELECT * FROM employee1 UNION ALL SELECT * FROM employee2`
B) `SELECT * FROM employee1 INTERSECT SELECT * FROM employee2`
C) `SELECT * FROM employee1`
D) `SELECT * FROM employee2`
??
SOLUTION:
C) Because `employee1` *already* contains only tuples where `dept = 'Sales'`, the query can be simplified to just selecting from `employee1`. The union with `employee2` is unnecessary and inefficient.

#flashcards/Query_Transformation_Vertical
QUESTION:  If a relation R(A, B, C, D) is vertically fragmented into R1(A, B, tuple_id) and R2(C, D, tuple_id), what operation is needed to reconstruct the original relation R?
OPTIONS:
A)  A selection based on A.
B)  A projection on B and C.
C)  A join of R1 and R2 on the `tuple_id` attribute.
D)  A union of R1 and R2.
??
SOLUTION:
C) Vertical fragmentation splits the attributes. To reconstruct the original relation, you need to perform a natural join (or an explicit join) on the common attribute, which in this case is the `tuple_id`.

#flashcards/Semijoin
QUESTION: What is the purpose of using a semijoin in distributed query processing?
OPTIONS:
A) To replicate data across multiple sites.
B) To fragment data across multiple sites.
C) To reduce the amount of data transferred between sites during a join operation.
D) To encrypt data during transmission.
??
SOLUTION:
C) A semijoin sends only the *relevant* columns and tuples from one relation to another, filtering out data that wouldn't participate in the final join result. This minimizes the data transferred, improving efficiency.

#flashcards/Semijoin_Formal
QUESTION: Given relations `r1` at site S1 and `r2` at site S2, what does the expression  `r1 ⋉ r2` represent, and what does it achieve in a distributed query?
OPTIONS:
A)  The full outer join of r1 and r2, returning all tuples from both.
B)  The Cartesian product of r1 and r2, combining all possible pairs of tuples.
C)  The semijoin of r1 with r2, selecting tuples from r1 that would contribute to the join with r2. It reduces data transfer from S1 to S2.
D) The semijoin of r2 with r1, selecting tuples from r2 that would contribute to the join with r1.
??
SOLUTION:
C) The symbol `⋉` denotes the semijoin. `r1 ⋉ r2` projects the join attributes of r1 and r2 from r1 and sends the result to site 2 to join with r2, then selecting only the relevant tuples that would match with r1, and then performs a join with the projected attributes of r1. It does *not* return tuples from r2 that don't participate in the join.

#flashcards/Parallel_Join
QUESTION: How can parallelism be exploited in a distributed join operation involving multiple relations at different sites?
OPTIONS:
A) By sending all relations to a single site and performing the join there.
B) By performing joins between pairs of relations at different sites simultaneously.
C) By replicating all relations at all sites.
D) By fragmenting all relations horizontally.
??
SOLUTION:
B) Different parts of the join (e.g., joining different pairs of relations) can be executed concurrently at different sites, reducing the overall query execution time.

#flashcards/Heterogeneous_Databases
QUESTION: What is a multidatabase system?
OPTIONS:
A) A database system that uses multiple data models.
B) A database system that spans multiple physical locations.
C) A software layer on top of existing heterogeneous database systems, providing an illusion of logical integration.
D) A database system that replicates data across multiple sites.
??
SOLUTION:
C) A multidatabase system provides a unified view and query interface over multiple, potentially different, pre-existing database systems, without physically integrating them.

#flashcards/Multidatabase_Advantages
QUESTION: What is a key advantage of using a multidatabase system approach?
OPTIONS:
A) It eliminates the need for local databases.
B) It provides perfect data consistency across all databases.
C) It preserves investment in existing heterogeneous databases and allows for local autonomy.
D) It simplifies transaction management.
??
SOLUTION:
C) Multidatabase systems allow organizations to leverage their existing database infrastructure and retain control over their local data, while still enabling access to data across different systems.

#flashcards/Unified_View_Challenges
QUESTION: What are some of the challenges in creating a unified view of data in a heterogeneous distributed database?
OPTIONS:
A) Different data models, different names for the same relation/attribute, different data representations, and different units of measure.
B) Network latency and bandwidth limitations.
C) The need for data replication.
D) The complexity of two-phase commit.
??
SOLUTION:
A) The core challenge is dealing with the *differences* between the underlying heterogeneous databases: different schemas, naming conventions, data types, and even units of measurement.

#flashcards/Query_Processing_Heterogeneous
QUESTION: What is a "wrapper" in the context of query processing in a heterogeneous database?
OPTIONS:
A) A security mechanism to protect data.
B) A software component that translates data and queries between a global schema and a local data source's schema.
C) A tool for optimizing query execution plans.
D) A protocol for distributed transaction management.
??
SOLUTION:
B) Wrappers are essential for bridging the gap between the unified view (global schema) presented by the multidatabase system and the individual schemas of the underlying heterogeneous databases.

#flashcards/Mediator_Systems
QUESTION: What is the primary distinction between a mediator system and a full-fledged multidatabase system?
OPTIONS:
A) Mediator systems do not provide a global schema.
B) Mediator systems typically focus on query processing and often do not handle transaction processing.
C) Mediator systems require physical integration of the underlying databases.
D) Mediator systems only work with homogeneous databases.
??
SOLUTION:
B) While the terms are sometimes used interchangeably, a mediator system often focuses on providing an integrated view for querying and may not implement full transactional capabilities (like two-phase commit) across the heterogeneous sources.

#flashcards/Local_vs_Global_Serializability
QUESTION: Why is guaranteeing local serializability at each site *not* sufficient to ensure global serializability in a multidatabase system?
OPTIONS:
A) Local databases cannot guarantee serializability.
B) Global transactions do not involve local databases.
C) Inconsistent ordering of global transactions at different sites can lead to a non-serializable global schedule, even if each site's local schedule is serializable.
D) Two-phase locking cannot be used in multidatabase systems.
??
SOLUTION:
C) The classic example involves two transactions, T1 and T2, accessing data items A and B at different sites.  If T1 precedes T2 at site 1 and T2 precedes T1 at site 2, the global schedule is non-serializable, even if each site maintains local serializability.

#flashcards/Cloud_Databases_Key_Value
QUESTION:  What is a key-value store, and why is it suitable for cloud databases?
OPTIONS:
A) A relational database system optimized for cloud environments.
B) A system that stores and retrieves data items based on a key, offering simplicity and scalability for large datasets.
C) A system for storing and retrieving encrypted data.
D) A system for managing metadata in a cloud environment.
??
SOLUTION:
B) Key-value stores provide a simple, highly scalable way to store and retrieve data, which is well-suited for the massive datasets and distributed nature of cloud environments.  They don't offer the full functionality of relational databases, but their simplicity and scalability are key advantages.

#flashcards/Cloud_Data_Representation
QUESTION: Why are data representation formats like JSON and XML widely used in cloud databases?
OPTIONS:
A) They are the only formats supported by cloud databases.
B) They provide strong data typing and schema enforcement.
C) They offer a flexible schema, accommodating records with varying structures and complex attributes.
D) They are inherently more secure than other formats.
??
SOLUTION:
C) The flexible schema capabilities of JSON and XML are crucial for handling the semi-structured or unstructured data often found in cloud applications.  Traditional relational schemas with fixed structures are often too restrictive.

#flashcards/Tablets
QUESTION:  What is a "tablet" in the context of cloud data storage?
OPTIONS:
A)  A physical storage device.
B)  A user interface for accessing cloud data.
C)  A relatively small, dynamically sized partition of a table.
D)  A security token for accessing cloud data.
??
SOLUTION:
C) Tablets are the units of data partitioning in many cloud storage systems.  They are dynamically split and merged to handle data growth and load balancing.

#flashcards/Tablet_Controller
QUESTION:  What is the role of a tablet controller in a cloud database system?
OPTIONS:
A)  To execute queries against tablets.
B)  To store the actual data within tablets.
C)  To track the partitioning function and the mapping between tablets and physical sites.
D) To provide a user interface for managing tablets.
??
SOLUTION:
C) The tablet controller is responsible for managing the dynamic partitioning of data into tablets and knowing which physical server is responsible for storing each tablet. This is essential for routing requests to the correct location.

#flashcards/PNUTS_Architecture
QUESTION: Briefly describe a key component of the PNUTS parallel storage system architecture shown in the diagram.
OPTIONS:
A) Routers direct requests to appropriate tablet servers.
B) All data is stored on a single, central server.
C) Two-phase commit is used for all updates.
D) Data is partitioned based on user ID.
??
SOLUTION:
A) From the diagram (page 96), we can identify key components such as *Routers* (which direct incoming requests), *Tablet Servers* (which store the data in tablets), and the *Tablet Controller* (which manages the mapping between tablets and servers).  The best answer from the choices given is A.

#flashcards/Directory_Systems
QUESTION: What are the two main types of directory systems, categorized by their organization and purpose?
OPTIONS:
A) Local and Global
B) White pages and Yellow pages
C) Hierarchical and Relational
D) Secure and Unsecure
??
SOLUTION:
B) White pages are organized by name or identifier for forward lookups (finding information *about* an entry). Yellow pages are organized by properties for reverse lookups (finding entries that *match* certain criteria).

#flashcards/LDAP
QUESTION: What does LDAP stand for, and what is its primary purpose?
OPTIONS:
A) Local Data Access Protocol; for accessing local databases.
B) Lightweight Directory Access Protocol; a protocol for accessing and managing directory information.
C) Logical Data Arrangement Protocol; for organizing data logically.
D) Large Data Application Protocol; for handling large datasets.
??
SOLUTION:
B) LDAP is a widely used protocol for accessing and managing directory information, often used for user authentication, storing organizational information, and similar tasks.

#flashcards/LDAP_Data_Model
QUESTION: What is a "distinguished name" (DN) in LDAP?
OPTIONS:
A) A unique identifier for an entry in an LDAP directory, composed of a sequence of relative distinguished names (RDNs).
B) The name of the LDAP server.
C) The username used to access the LDAP directory.
D) A type of query used in LDAP.
??
SOLUTION:
A) The DN uniquely identifies an entry within the hierarchical structure of the LDAP directory, similar to a full path in a file system.

#flashcards/LDAP_RDN
QUESTION: Give an example of a common Relative Distinguished Name (RDN) used in LDAP, and what it typically represents.
OPTIONS:
A)  `ipAddress`; representing an IP address.
B)  `cn`; representing the common name (e.g., a person's name).
C)  `password`; representing a user's password.
D)  `timestamp`; representing the last modification time.
??
SOLUTION:
B) `cn=John Doe` is an example, where `cn` (common name) is the RDN and represents the name of the entry (e.g., a person or resource). Other common RDNs include `ou` (organizational unit), `o` (organization), and `c` (country).

#flashcards/LDAP_Object_Classes
QUESTION:  What is the purpose of object classes in LDAP?
OPTIONS:
A) To define the structure of the directory tree.
B) To specify the attributes and their types that entries of a particular class can or must have.
C) To control access permissions to the directory.
D) To define the network protocol used by LDAP.
??
SOLUTION:
B) Object classes are analogous to classes in object-oriented programming.  They provide a schema for entries, defining what attributes are allowed or required.

#flashcards/LDAP_DIT
QUESTION: What does DIT stand for in the context of LDAP, and what does it represent?
OPTIONS:
A) Data Interchange Type; describes the format of data exchanged.
B) Directory Information Tree; the hierarchical structure in which entries are organized.
C) Distinguished Identification Tag; a unique identifier for an entry.
D) Data Integrity Tool; ensures the consistency of the directory.
??
SOLUTION:
B) The Directory Information Tree (DIT) is the overall hierarchical structure of the LDAP directory, similar to a file system's directory tree.

#flashcards/LDAP_Queries
QUESTION: What is a "base" in an LDAP query?
OPTIONS:
A) The LDAP server's address.
B) The node in the DIT from where the search starts.
C) The username used for authentication.
D) The type of query being performed (e.g., search, modify).
??
SOLUTION:
B) The base specifies the starting point for the search within the directory tree.

#flashcards/LDAP_URLs
QUESTION:  In an LDAP URL, what does the `??sub` component typically indicate?
OPTIONS:
A)  The username and password for authentication.
B)  The attributes to be returned.
C)  A search scope that includes the entire subtree below the base DN.
D)  A filter to be applied to the search results.
??
SOLUTION:
C)  `??sub` is a common way to specify the search scope as the entire subtree rooted at the base DN. Other scopes include `??base` (just the base entry) and `??one` (the base and its immediate children).

#flashcards/LDAP_API
QUESTION: Does LDAP define standard DDL and DML statements like SQL?
OPTIONS:
  A) Yes
  B) No
??
SOLUTION:
B) No. LDAP defines a *network protocol* for interacting with a directory, including operations for querying, adding, modifying, and deleting entries. However, it doesn't have a specific query language like SQL with DDL and DML statements. Instead, client applications use an API (like the C API shown in the slides) or tools that implement the LDAP protocol.

#flashcards/LDAP_Transactions
QUESTION:  Does the LDAP protocol natively support multi-operation atomic transactions?
OPTIONS:
A)  Yes
B)  No
??
SOLUTION:
B)  No. Each LDAP operation (e.g., add, modify, delete, search) is typically treated as a separate transaction. There's no built-in mechanism in the core LDAP protocol for grouping multiple operations into a single atomic transaction.  This is a significant difference from relational databases.

#flashcards/Distributed_Directory_Trees
QUESTION: What is a "referral" in the context of distributed LDAP directories?
OPTIONS:
A) A recommendation for another user.
B) A pointer from a node in one Directory Information Tree (DIT) to a node in another DIT.
C) A log entry recording access to the directory.
D) A type of error message.
??
SOLUTION:
B) Referrals are a key mechanism for creating a distributed directory service.  They allow different parts of the overall directory structure to be managed by different servers, while still presenting a unified view to the client.

#flashcards/3PC_Assumptions
QUESTION: What is a key assumption of the Three-Phase Commit (3PC) protocol that makes it less practical in real-world systems?
OPTIONS:
A) The assumption of a single coordinator.
B) The assumption of no network partitioning.
C) The assumption that all sites have the same processing speed.
D) The assumption of a limited number of transactions.
??
SOLUTION:
B) The assumption of *no network partitions* is often unrealistic in large, distributed systems. Network partitions can (and do) occur, and 3PC is not designed to handle them correctly. This limits its practical applicability.

#flashcards/3PC_Precommit
QUESTION: What is the purpose of the "pre-commit" state in the Three-Phase Commit (3PC) protocol?
OPTIONS:
A) It is the same as the "prepare" phase in 2PC.
B) It allows the coordinator to abort the transaction after participants have voted to commit.
C) It provides a mechanism for non-failed sites to reach a decision even if the coordinator fails, reducing blocking.
D) It allows participants to unilaterally commit the transaction.
??
SOLUTION:
C) The pre-commit state is the key innovation of 3PC. After participants vote to commit ("ready"), the coordinator enters the pre-commit state and records this decision at multiple sites. This knowledge allows the system to make progress even if the coordinator subsequently fails, as long as a sufficient number of sites remain operational.
