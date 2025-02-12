
---
**I. Homogeneous and Heterogeneous Databases (5 Questions)**

#flashcards/Homogeneous_and_Heterogeneous_Databases
What is the key difference between homogeneous and heterogeneous distributed databases?
a) Data storage format  b) Network protocol  c) Schema and DBMS software  d) Physical location
??
c) Schema and DBMS software

#flashcards/Homogeneous_and_Heterogeneous_Databases
In a homogeneous distributed database, all sites have:
a)  Different schemas
b)  Identical DBMS software
c)   Different operating system
d)  Different Data storage
??
b) Identical DBMS software

#flashcards/Homogeneous_and_Heterogeneous_Databases
Which of the following is TRUE about heterogeneous distributed databases? (MSQ)
a) All sites use the same DBMS.
b) Sites may have different schemas.
c) Sites are always fully aware of each other.
d) Sites may use different query languages.
??
b) and d)

#flashcards/Homogeneous_and_Heterogeneous_Databases
Why are heterogeneous databases more complex to manage?
??
Because they require schema integration and translation between different data models and query languages.

#flashcards/Homogeneous_and_Heterogeneous_Databases
Provide an example scenario in which Heterogeneous distributed databases systems are required?
??
A company merger where each pre-existing database systems reside on different physical hardware and have different schemas.

---

**II. Distributed Data Storage (6 Questions)**

#flashcards/Distributed_Data_Storage
What are the two primary approaches to storing a relation in a distributed database?
a) Indexing and Partitioning
b) Replication and Fragmentation
c) Encryption and Compression
d) Normalization and Denormalization
??
b) Replication and Fragmentation

#flashcards/Distributed_Data_Storage
Full replication means:
a)  A copy of the relation is stored at one site.
b)  A copy of the relation is stored at every site.
c)  The relation is split into fragments.
d) The realtion is stored at two sites only
??
b) A copy of the relation is stored at every site.

#flashcards/Distributed_Data_Storage
What is a primary advantage of data replication? (MSQ)
a) Reduced storage costs
b) Increased availability
c) Simplified update process
d) Improved read performance
??
b) and d)

#flashcards/Distributed_Data_Storage
Horizontal fragmentation divides a relation based on:
a) Attributes
b) Tuples
c) Keys
d) Indexes
??
b) Tuples

#flashcards/Distributed_Data_Storage
Explain the concept of *Data Transparency* in distributed databases, and its three forms.
??
Data transparency means users should not need to know *how* or *where* data is stored. The three forms are:
    *   **Fragmentation Transparency:** Users don't know how a relation is fragmented.
    *   **Replication Transparency:** Users don't know which (or how many) replicas exist.
    *   **Location Transparency:** Users don't know the physical location of data.

#flashcards/Distributed_Data_Storage
How are names kept unique in a distributed database?
??
By Prefixing the name with the site identifier.

---

**III. Distributed Transactions (5 Questions)**

#flashcards/Distributed_Transactions
What is the difference between a local transaction and a global transaction?
??
A *local transaction* accesses data at a single site, while a *global transaction* accesses data at multiple sites.

#flashcards/Distributed_Transactions
What is the role of a transaction coordinator in a distributed system?
a) Manage local transactions
b) Ensure ACID properties of local transactions
c) Coordinate the execution of global transactions across multiple sites
d) Handle network communication
??
c) Coordinate the execution of global transactions across multiple sites

#flashcards/Distributed_Transactions
Which component is responsible for maintaining the log for recovery in distributed system?
a) Transaction manager
b) Transaction coordinator
c) Data storage
d) Network protocol
??
a) Transaction manager

#flashcards/Distributed_Transactions
Name two subsystems that each site contains in an abstract model of a transaction system.
??
*   Transaction Manager
*   Transaction Coordinator

#flashcards/Distributed_Transactions
List three types of system failure modes in distributed transactions other than traditional system failure.
??
*  Site Failure
*	Message Loss
*  Communication Link Failure
*  Network Partition

---

**IV. Commit Protocols (5 Questions)**

#flashcards/Commit_Protocols
What is the purpose of a commit protocol in a distributed database?
??
To ensure atomicity of global transactions; that is, all sites involved either commit or abort the transaction.

#flashcards/Commit_Protocols
What are the two phases of the Two-Phase Commit (2PC) protocol?
??
*   **Phase 1 (Prepare Phase):** Coordinator asks all participants if they are ready to commit.
*   **Phase 2 (Commit/Abort Phase):**  Coordinator tells all participants to commit (if all said "ready") or abort (if any said "no").

#flashcards/Commit_Protocols
What is the "blocking problem" in 2PC?
??
If the coordinator fails after participants have voted "ready" but before sending the final commit/abort decision, participants may be blocked, unable to proceed until the coordinator recovers.

#flashcards/Commit_Protocols
How does Three-Phase Commit (3PC) attempt to address the blocking problem?
??
3PC introduces an extra phase (pre-commit) to ensure that at least one other site knows the coordinator's intended decision (commit or abort), allowing recovery even if the coordinator fails. It makes assumptions about the number of site failures and network partitions.

#flashcards/Commit_Protocols
Under what circumstances Persistent messaging system can be used in alternative to commit protocol.
??
Persistent messaging can handle transaction processing across organizational boundaries, or when blocking (as in 2PC) is unacceptable.

---

**V. Concurrency Control (5 Questions)**

#flashcards/Concurrency_Control
How does the single lock-manager approach handle concurrency control?
??
All lock requests are sent to a designated, single lock-manager site.

#flashcards/Concurrency_Control
What is a primary disadvantage of the single lock-manager approach? (MSQ)
a) Complex implementation
b) The lock manager site can become a bottleneck.
c) Difficult deadlock handling
d) Vulnerability to failure of the lock-manager site.
??
b) and d)

#flashcards/Concurrency_Control
Explain the difference between the *majority protocol* and the *biased protocol* for handling replicated data.
??
*   **Majority Protocol:**  A transaction needs locks on a majority of replicas for both read and write operations.
*   **Biased Protocol:**  Read operations need a lock on only one replica, while write operations need locks on all replicas.  This favors read operations.

#flashcards/Concurrency_Control
What is a potential issue with using timestamps for concurrency control in a distributed system?
??
Ensuring that timestamps are generated fairly and uniquely across all sites, especially if clocks are not perfectly synchronized.

#flashcards/Concurrency_Control
What is the basic idea behind *quorum consensus*?
??
Assign weights to sites and define read/write quorums. A read/write operation needs to acquire locks on enough replicas to meet the respective quorum requirement.

---

**VI.  Availability (4 Questions)**

#flashcards/Availability
Why is availability a critical concern in distributed databases?
??
Because failures (site, link, network) are more likely in a distributed environment, and the system should continue functioning despite failures.

#flashcards/Availability
How does the "read one, write all available" approach improve availability?  What is a potential downside?
??
It allows read operations to proceed as long as *any* replica is available.  Writes proceed on all *available* replicas.  The downside is that it can lead to inconsistencies if network partitions occur.

#flashcards/Availability
What is the purpose of a *coordinator election* algorithm?
??
To dynamically select a new coordinator if the current coordinator fails.

#flashcards/Availability
State the CAP theorem, and its implications for system design.
??
*CAP Theorem:*  A distributed system can have at most two of these three properties: Consistency, Availability, Partition-tolerance.  This forces designers to make trade-offs. Many systems prioritize availability and partition tolerance over strict consistency.

Okay, here are 30 *new* questions on Chapter 19: Distributed Databases, including some numerical and conceptual problems requiring MathJax, and avoiding overlap with the previous set. These questions are designed to test a deeper understanding of the material.

---

**I. Distributed Data Storage (5 Questions)**

1.  #flashcards/Distributed_Data_Storage
    A relation `R(A, B, C, D)` is horizontally fragmented into three fragments: $R_1 = \sigma_{A < 5}(R)$, $R_2 = \sigma_{5 \le A < 10}(R)$, and $R_3 = \sigma_{A \ge 10}(R)$.  A query $Q = \sigma_{A=7 \text{ AND } B=2}(R)$ is executed.  Which fragments need to be accessed to answer Q, and how can the query be optimized for this fragmentation?
    ??
    Only $R_2$ needs to be accessed.  The optimized query is $Q' = \sigma_{A=7 \text{ AND } B=2}(R_2)$. Because the selection predicate $A=7$ falls entirely within the range defining $R_2$, we can directly apply the selection to $R_2$ without considering $R_1$ or $R_3$.

2.  #flashcards/Distributed_Data_Storage
    A relation `S(X, Y, Z)` is vertically fragmented into $S_1 = \Pi_{X,Y}(S)$ and $S_2 = \Pi_{Y,Z}(S)$.  Assume `Y` is a candidate key of S. Describe how to reconstruct the original relation `S` from $S_1$ and $S_2$.
    ??
    $S = S_1 \bowtie_{Y} S_2$. Since `Y` is a candidate key, the natural join on `Y` will correctly reconstruct the original relation without loss of information or introduction of spurious tuples.

3.  #flashcards/Distributed_Data_Storage
    Explain why a distributed database system might choose *not* to use full replication, even though it offers the highest availability.
    ??
    Full replication incurs high storage costs (replicating data at every site) and high update overhead (every update must be propagated to *all* sites). The trade-off is between availability and these costs.

4. #flashcards/Distributed_Data_Storage
    What is the main advantage of using a *name server* in a distributed system, and what is a significant *disadvantage*?
     ??
      Advantage: Centralized management of names and location transparency. Disadvantage: The name server can become a performance bottleneck and a single point of failure.
5.  #flashcards/Distributed_Data_Storage
    A distributed system uses site prefixes for unique names. Relation `account` exists at sites `S1`, `S2`, and `S3`.  A user wants to access the `account` relation without knowing its location. How can *aliases* help achieve location transparency?
    ??
    The system can create a global alias `account` that maps to the site-specific names (`S1.account`, `S2.account`, `S3.account`).  The user queries using the alias `account`, and the system translates it to the correct site-specific name.

---

**II. Distributed Transactions and Commit Protocols (7 Questions)**

6.  #flashcards/Distributed_Transactions_Commit_Protocols
    In a 2PC protocol, a participant site sends a `<ready T>` message to the coordinator.  What does this message signify, and what constraints does it place on the participant?
    ??
    The `<ready T>` message signifies that the participant has completed its part of transaction `T` and has written all necessary information (including redo/undo logs) to stable storage.  It *promises* to either commit or abort `T` as instructed by the coordinator.  It cannot unilaterally decide after sending `<ready T>`.

7.  #flashcards/Distributed_Transactions_Commit_Protocols
    A transaction `T` executes at sites `S1`, `S2`, and `S3`.  `S1` is the coordinator.  `S2` fails *after* sending `<ready T>` but *before* receiving the final decision from `S1`.  When `S2` recovers, what steps must it take?  Describe the process.
    ??
    `S2` must consult its log.  If it finds `<commit T>` or `<abort T>`, it performs redo(T) or undo(T), respectively.  If it finds only `<ready T>`, it must contact `S1` (or other sites) to determine the fate of `T`.  If `S1` is unavailable, `S2` may be blocked (in 2PC).  It might use a `querystatus T` message.

8.  #flashcards/Distributed_Transactions_Commit_Protocols
    Explain why the 3PC protocol is non-blocking (under certain assumptions), while 2PC can be blocking.
    ??
   2PC: If the coordinator fails after participants vote "ready" but before a decision is sent, participants are blocked.
   3PC: Introduces a "pre-commit" state. If the coordinator fails, surviving sites can elect a new coordinator that can determine the outcome based on the states of other sites (at least one will know if a pre-commit occurred). This assumes a limited number of failures and no network partitions.

9.  #flashcards/Distributed_Transactions_Commit_Protocols
    A system uses persistent messaging.  A transaction `T` at site `A` sends a persistent message to site `B` to debit an account.  Site `B`'s database crashes *after* receiving the message but *before* processing it and sending an acknowledgment.  What happens when site `B` recovers?
    ??
    The message will still be in `B`'s `received_messages` relation (or equivalent).  The receiving-site protocol dictates that `B` will process the message (debit the account) and then send an acknowledgment to `A`. This ensures exactly-once delivery.

10. #flashcards/Distributed_Transactions_Commit_Protocols
    In a persistent messaging system, why is it essential for the receiving site to check if a received message is already present in the `received_messages` relation?
    ??
To prevent duplicate processing of the message.  Network failures can lead to message retransmissions, and without the check, the same operation might be executed multiple times.

1. #flashcards/Distributed_Transactions_Commit_Protocols
    In 2PC, if the coordinator determines the final decision as *abort*, in what all cases the participating sites will receive the final decision as abort from the coordinator?
     ??
     If *any* of the participating sites send an `<abort T>` or `<no T>` message, or if the coordinator itself decides to abort, or if a timeout occurs before receiving responses from all participants.

2. #flashcards/Distributed_Transactions_Commit_Protocols
    What optimization is used in recovery to enable transaction processing during identifying the in-doubt transactions.
      ??
      Storing Lock information in the log. `<ready T, L>` where `L` stores the list of all write locks. So, during recovery, reacquire the locks and enable other transactions.

---

**III. Concurrency Control and Deadlock Handling (7 Questions)**

3. #flashcards/Concurrency_Control_Deadlock_Handling
    A distributed database uses the primary copy method.  Data item `X` has its primary copy at site `A`, and replicas at sites `B` and `C`.  Site `A` fails.  Can read and write operations on `X` continue?  Explain.
    ??
    No.  With the primary copy method, all lock requests for `X` must go to the primary site (`A`).  Since `A` is down, no locks can be granted, and neither read nor write operations can proceed.

4. #flashcards/Concurrency_Control_Deadlock_Handling
    A system uses the majority protocol.  Data item `Y` is replicated at 5 sites.  How many replicas must a transaction lock for a *read* operation?  How many for a *write* operation?
    ??
    For both read and write, the transaction must lock a *majority* of the replicas.  With 5 sites, a majority is 3 (5 / 2 + 1, rounded up).

5. #flashcards/Concurrency_Control_Deadlock_Handling
    A system uses the quorum consensus protocol.  A data item `Z` has replicas at 4 sites, with weights 1, 1, 2, and 2.  The total weight (S) is 6.  The read quorum ($Q_r$) is 3, and the write quorum ($Q_w$) is 4.  Give *two* different sets of sites that could be locked for a *read* operation.
    ??
    Many combinations are possible. Here are two:
    *   Sites with weights 1, 1, and 2 (total weight = 4, which is >= $Q_r$)
    *   Sites with weights 2 and 2 (total weight = 4, which is >= $Q_r$)

6. #flashcards/Concurrency_Control_Deadlock_Handling
    A system uses a distributed lock manager.  Transaction $T_1$ at site $A$ requests a lock on data item $X$ at site $B$. Transaction $T_2$ at site $B$ requests a lock on data item $Y$ at site $A$.  Describe how a *global deadlock* can occur, even if there are no local deadlocks at either site.  Illustrate with a wait-for graph.
    ??
    A global deadlock can occur if $T_1$ holds the lock on $Y$ at $A$ and is waiting for $X$ at $B$, while $T_2$ holds the lock on $X$ at $B$ and is waiting for $Y$ at $A$.

    Global Wait-for Graph:   $T_1 \rightarrow T_2 \rightarrow T_1$ (a cycle)

    Local Wait-for at A: $T_1$ (waiting for $T_2$ remotely)
    Local Wait-for at B: $T_2$ (waiting for $T_1$ remotely)  Neither local graph shows a cycle.

7. #flashcards/Concurrency_Control_Deadlock_Handling
    Explain how *false cycles* can occur in a distributed deadlock detection algorithm.
    ??
    False cycles can arise due to communication delays.  A lock release message from one site might arrive at the deadlock detector *after* a lock request message from another site, leading the detector to incorrectly infer a cycle in the global wait-for graph.

8. #flashcards/Concurrency_Control_Deadlock_Handling
    In a system using timestamp-based concurrency control, how are unique global timestamps typically generated?
    ??
    By concatenating a locally generated timestamp (from a logical counter or clock) with the site identifier. The site ID is usually placed in the least significant position.

9. #flashcards/Concurrency_Control_Deadlock_Handling
   What is implied by "wait-die" and "wound-wait" deadlock prevention scheme?
    ??
*   **Wait-Die:** If a transaction *Ti* requests a lock and the lock holder *Tj* has a lower time-stamp, *Ti* waits, else *Ti* aborts (dies).
*	**Wound-Wait:** If a transaction *Ti* requests a lock and the lock holder *Tj* has a lower time-stamp, *Tj* gets aborted, else *Ti* waits.
---

**IV. Availability and Replication (6 Questions)**

10. #flashcards/Availability_Replication
    A distributed system uses the "read one, write all" replication scheme. Data item `D` has replicas at sites `S1`, `S2`, and `S3`.  `S1` fails.  Can a transaction read `D`? Can it write `D`?
    ??
    A transaction *can* read `D` (from either `S2` or `S3`).  It *cannot* write `D` because "write all" requires all replicas to be available.

11. #flashcards/Availability_Replication
    What is the key difference in assumptions between the *majority protocol* and the *read one, write all available* protocol regarding network failures?
    ??
    The majority protocol *can* handle network partitions (as long as a majority of replicas are in one partition).  "Read one, write all available" assumes no network partitions, or, inconsistencies are tolerated.

12. #flashcards/Availability_Replication
    What actions must be taken when a failed site *reintegrates* into a distributed database system that uses replication?
    ??
    The reintegrating site must update its system tables and, if it had replicas, obtain the current values of those data items (and ensure it receives all future updates) to become consistent with the rest of the system.

13. #flashcards/Availability_Replication
    Briefly describe the *bully algorithm* for coordinator selection.
    ??
    The bully algorithm assumes each site has a unique ID.  When a site detects coordinator failure, it sends election messages to sites with higher IDs.  If no response, it declares itself the coordinator.  A recovering site with the highest ID will "bully" lower-ID sites to become the coordinator.

14. #flashcards/Availability_Replication
    What is an advantage of using a *backup coordinator* compared to relying solely on an election algorithm after coordinator failure?
    ??
    A backup coordinator allows for *immediate* continuation of processing, as it maintains the same state as the primary coordinator. Election algorithms require time to elect a new coordinator and gather state information.

15. #flashcards/Availability_Replication
     What is a disadvantage of using a backup coordinator?
      ??
      Overhead during the normal processing, also requires additional communication to be synchronized.

---

**V. Heterogeneous Databases, Cloud, and Directory Systems (5 Questions)**

16. #flashcards/Heterogeneous_Cloud_Directory
    What is the role of a *wrapper* in a heterogeneous database system or a mediator system?
    ??
    A wrapper provides a uniform interface (often relational) to a local data source, translating queries from a global schema to the local schema and results back to the global schema.

17. #flashcards/Heterogeneous_Cloud_Directory
    What is the primary challenge in ensuring global serializability in a *multidatabase system* where local sites ensure local serializability?
    ??
    The multidatabase system has limited or no control over the local concurrency control mechanisms.  Local schedules might be serializable, but the global schedule might not be.  (Example: $T_1$ before $T_2$ at one site, $T_2$ before $T_1$ at another).

18. #flashcards/Heterogeneous_Cloud_Directory
   What are the differences between *Mediator systems* and *Multidatabase systems*?
    ??
Mediator systems provide integrated global view and query facilities, but they do not handle transactions. On the otherhand, Multidatabase systems consider transaction processing.

19. #flashcards/Heterogeneous_Cloud_Directory
    Describe the basic data model used by many cloud data storage systems (like Bigtable).
    ??
    A key-value store, where data is stored and retrieved using a unique key.  The "value" can be complex (e.g., multiple attributes, as in Bigtable), but the system doesn't interpret it beyond basic operations.

20. #flashcards/Heterogeneous_Cloud_Directory
     What is the role of the *distinguished name (DN)* in LDAP?  Give an example.
     ??
       The DN uniquely identifies an entry in an LDAP directory. It's a hierarchical name composed of relative distinguished names (RDNs). Example: `cn=John Doe, ou=Engineering, o=Example Corp, c=US`


