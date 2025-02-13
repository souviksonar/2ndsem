Okay, here are 40 questions based on the provided PDF content, formatted as requested, and suitable for postgraduate students.

#flashcards/Distributed_Databases_Overview
QUESTION:  What is the primary distinction between a parallel database system and a distributed database system?
OPTIONS:
A) Parallel systems have tightly coupled processors; distributed systems have loosely coupled sites.
B) Parallel systems have no physical components in common; distributed systems do.
C) Parallel systems can have independent database management systems on each site; distributed systems cannot.
D) Parallel systems are always homogeneous; distributed systems are always heterogeneous.
??
SOLUTION:
A) Parallel systems are characterized by tightly coupled processors that form a single database system, while distributed systems consist of loosely coupled sites with potentially independent database systems.
<!--SR:!2025-02-17,4,270-->

#flashcards/Distributed_Databases_Overview
QUESTION:  In a distributed database system, data resides in:
OPTIONS:
A) A single, centralized location.
B) Multiple locations.
C) The location of the query origin.
D) The transaction coordinator.
??
SOLUTION:
B) Multiple locations.
<!--SR:!2025-02-16,3,250-->

#flashcards/Homogeneous_vs_Heterogeneous
QUESTION: In a homogeneous distributed database, all sites have _________ database management system software.
OPTIONS:
A) Different
B) Identical
C) Compatible, but potentially different versions of
D) Either A or C is acceptable
??
SOLUTION: B) Identical
<!--SR:!2025-02-17,4,270-->

#flashcards/Homogeneous_vs_Heterogeneous
QUESTION:  Which of the following is NOT a characteristic of a *homogeneous* distributed database system?
OPTIONS:
A) All sites have identical DBMS software.
B) Sites are aware of one another.
C) Sites agree to cooperate in processing user requests.
D) Sites retain complete autonomy over their schemas and DBMS.
??
SOLUTION:
D) Sites *surrender* a portion of their autonomy in a homogeneous system.
<!--SR:!2025-02-17,4,270-->

#flashcards/Homogeneous_vs_Heterogeneous
QUESTION: A major problem for query processing in *heterogeneous* distributed databases is the difference in _________.
OPTIONS:
A) Transaction Coordinators
B) Commit Protocols
C) Schemas
D) Site Identifiers
??
SOLUTION: C) Schemas
<!--SR:!2025-02-17,4,270-->

#flashcards/Distributed_Data_Storage
QUESTION: List the two primary approaches to storing a relation `r` in a distributed database.
??
SOLUTION:
The two primary approaches are:
1.  Replication
2.  Fragmentation
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Replication
QUESTION: Full replication means that a copy of a relation is stored at:
OPTIONS:
A) At least two sites.
B) Every site in the system.
C) The primary site and a backup site.
D) Only at the site where the relation was created.
??
SOLUTION:
B) Every site in the system.
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Replication
QUESTION: One advantage of data replication is increased _________.  One disadvantage is increased _________ on update.
??
SOLUTION:
One advantage of data replication is increased *availability*. One disadvantage is increased *overhead* on update.
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Replication
QUESTION: What benefit does the "primary copy" scheme provide in managing replicated data?
??
SOLUTION:
The primary copy scheme simplifies the management of replicas by designating one copy as the primary, often associated with the origin of the data. It helps with concurrency control.
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Fragmentation
QUESTION: Horizontal fragmentation splits a relation by assigning each _______ of the relation to one or more fragments.
OPTIONS:
A) Attribute
B) Tuple
C) Column
D) Schema
??
SOLUTION:
B) Tuple
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Fragmentation
QUESTION: Define horizontal fragmentation of a relation *r* mathematically, using a predicate *Pi* to create fragment *ri*.
??
SOLUTION:
$r_i = \sigma_{P_i}(r)$
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Fragmentation
QUESTION:  Vertical fragmentation of relation *r* with schema *R* involves defining subsets of attributes  $R_1, R_2, ..., R_n$ such that their union equals:
OPTIONS:
A)  $r$
B)  $r_i$
C)  $R$
D) $\Pi_{R_i}(r)$
??
SOLUTION:
C)  $R$
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Fragmentation
QUESTION:  How is the original relation *r* reconstructed from its *vertical* fragments $r_1, r_2, ..., r_n$?
??
SOLUTION:
$r = r_1 \bowtie r_2 \bowtie ... \bowtie r_n$ (Natural join of all fragments)
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Transparency
QUESTION:  What are the three forms of data transparency mentioned in the text?
??
SOLUTION:
The three forms are:
1.  Fragmentation transparency
2.  Replication transparency
3.  Location transparency
<!--SR:!2025-02-17,4,270-->

#flashcards/Data_Transparency
QUESTION:  What does *replication transparency* mean in the context of distributed databases?
??
SOLUTION:
Replication transparency means that users view each data object as logically unique, and are not concerned with which data objects are replicated or where replicas are placed. The system handles replication details.
<!--SR:!2025-02-17,4,270-->

#flashcards/Naming
QUESTION: To avoid name clashes in a distributed database, each site prefixes its own _________ to any name it generates.
OPTIONS:
A) Timestamp
B) Transaction ID
C) Site Identifier
D) User ID
??
SOLUTION:
C) Site Identifier
<!--SR:!2025-02-17,4,270-->

#flashcards/Naming
QUESTION:  Why is using a central name server in a distributed database potentially problematic?  Name *two* disadvantages.
??
SOLUTION:
Two disadvantages are:
4.  The name server can become a performance bottleneck.
5.  If the name server crashes, the system may become unusable.
<!--SR:!2025-02-17,4,270-->

#flashcards/Naming
QUESTION: What is an alias used for in distributed database systems concerning naming?
??
SOLUTION: An alias is a way to give alternate names to data items. The user refers to a data item by a simpler name which is translated to a complex name by the system. It improves location transparency.
<!--SR:!2025-02-17,4,270-->

#flashcards/Distributed_Transactions
QUESTION:  A _______ transaction accesses and updates data in only one local database, while a _______ transaction accesses and updates data in several local databases.
??
SOLUTION:
A *local* transaction accesses and updates data in only one local database, while a *global* transaction accesses and updates data in several local databases.
<!--SR:!2025-02-17,4,270-->

#flashcards/System_Structure
QUESTION: Name the two subsystems that an abstract model of a transaction system contains at each site in a distributed database.
??
SOLUTION:
The two subsystems are:
6.  Transaction manager
7.  Transaction coordinator
<!--SR:!2025-02-17,4,270-->

#flashcards/System_Structure
QUESTION: What is the role of the *transaction coordinator* in a distributed database system?
??
SOLUTION:
The transaction coordinator coordinates the execution of the various transactions (both local and global) initiated at that site. This includes starting the transaction, breaking it into subtransactions, distributing subtransactions, and coordinating termination (commit or abort).
<!--SR:!2025-02-17,4,270-->

#flashcards/System_Failure_Modes
QUESTION: Besides software errors, hardware errors and disk crashes, list *three* additional types of failures that must be dealt with in a distributed environment.
??
SOLUTION:
Three additional failure types are:
8.  Failure of a site.
9.  Loss of messages.
10.  Failure of a communication link/Network partition.
<!--SR:!2025-02-17,4,270-->

#flashcards/System_Failure_Modes
QUESTION: If two sites A and B are *not* directly connected, how are messages routed between them?
??
SOLUTION:
Messages must be routed through a sequence of communication links.
<!--SR:!2025-02-17,4,270-->

#flashcards/System_Failure_Modes
QUESTION: Define what is meant by a "network partition" in a distributed system.
??
SOLUTION:
A network partition occurs when the system is split into two (or more) subsystems (partitions) that lack any connection between them. A partition may even consist of a single node.
<!--SR:!2025-02-17,4,270-->

#flashcards/Commit_Protocols
QUESTION: The most widely used commit protocol in distributed database is called:
??
SOLUTION:
Two-Phase Commit (2PC)
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION: In the first phase of 2PC, the coordinator sends a _______ message to all participating sites.
OPTIONS:
A) Commit
B) Abort
C) Prepare
D) Ready
??
SOLUTION:
C) Prepare
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION: A site can unilaterally abort a transaction *T* before sending which message to the coordinator in 2PC?
OPTIONS:
A)  `<abort T>`
B)  `<commit T>`
C)  `<ready T>`
D)  `<no T>`
??
SOLUTION:
C) `<ready T>`
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION:  If a participating site in 2PC fails *before* responding to a `prepare T` message, what does the coordinator assume?
??
SOLUTION:
The coordinator assumes that the site responded with an `<abort T>` message.
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION: A participating site that fails and has a `<ready T>` record in its log, but no `<commit T>` or `<abort T>`, must do what upon recovery?
OPTIONS:
A) Immediately execute `redo(T)`.
B) Immediately execute `undo(T)`.
C) Consult the coordinator (or other sites) to determine the fate of T.
D) Nothing; the transaction is already completed.
??
SOLUTION:
C) Consult the coordinator (or other sites) to determine the fate of T.
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION: What is the "blocking problem" in the context of the Two-Phase Commit protocol?
??
SOLUTION:
The blocking problem occurs when the coordinator fails, and participating sites have `<ready T>` records but no decision (commit or abort). These sites must wait for the coordinator to recover, potentially holding resources and blocking other transactions.
<!--SR:!2025-02-17,4,270-->

#flashcards/Two_Phase_Commit
QUESTION: How does adding lock information to the `<ready T, L>` log record help with recovery in 2PC and improve performance?
??
SOLUTION:
It allows the site to reacquire locks for in-doubt transactions after local recovery, enabling normal transaction processing to begin *before* the in-doubt transactions are resolved (committed or rolled back).
<!--SR:!2025-02-17,4,270-->

#flashcards/Three_Phase_Commit
QUESTION:  The Three-Phase Commit (3PC) protocol is designed to avoid the _______ problem, under certain assumptions.
??
SOLUTION:
The Three-Phase Commit (3PC) protocol is designed to avoid the *blocking* problem, under certain assumptions.
<!--SR:!2025-02-17,4,270-->

#flashcards/Alternative_Transaction_Models
QUESTION: Persistent messages are guaranteed to be delivered to the recipient _______, if the sending transaction commits.
OPTIONS:
A) At least once
B) At most once
C) Exactly once
D) Zero or more times
??
SOLUTION:
C) Exactly once
<!--SR:!2025-02-17,4,270-->

#flashcards/Alternative_Transaction_Models
QUESTION:  Why is eliminating blocking important for transactions that cross organizational boundaries?
??
SOLUTION:
Few organizations would agree to support two-phase commit for transactions originating outside the organization because failures could result in blocking of access to local data for an indeterminate amount of time.
<!--SR:!2025-02-17,4,270-->

#flashcards/Concurrency_Control
QUESTION: In the single lock-manager approach, all lock and unlock requests are made at:
OPTIONS:
A) Every site where a replica exists.
B) The site where the transaction originated.
C) A single designated site.
D) The primary copy site.
??
SOLUTION:
C) A single designated site.
<!--SR:!2025-02-17,4,270-->

#flashcards/Concurrency_Control
QUESTION: One disadvantage of the single lock-manager approach is that the designated site can become a _______.
??
SOLUTION:
One disadvantage of the single lock-manager approach is that the designated site can become a *bottleneck*.
<!--SR:!2025-02-17,4,270-->

#flashcards/Concurrency_Control
QUESTION: The Majority Protocol requires a transaction to obtain a lock on what before operating on a data object?
??
Solution:
The majority protocol requires that before operating on a data object a transaction must obtain locks on *more than half* of the replicas.
<!--SR:!2025-02-17,4,270-->

#flashcards/Concurrency_Control
QUESTION: The _______ protocol assigns each site a nonnegative weight and assigns a read and write quorum.
??
SOLUTION:
The *quorum consensus* protocol assigns each site a nonnegative weight and assigns a read and write quorum.
<!--SR:!2025-02-17,4,270-->

#flashcards/Timestamping
QUESTION: In a distributed system, how is a *globally* unique timestamp generated from a local timestamp and a site identifier?
??
SOLUTION:
The globally unique timestamp is generated by concatenating the local timestamp with the site identifier, with the site identifier in the *least significant* position.
<!--SR:!2025-02-17,4,270-->

#flashcards/Timestamping
QUESTION: Why is the site identifier placed in the *least significant* position when generating a global timestamp?
??
SOLUTION:
This is to ensure that global timestamps generated at one site are not always greater than those generated at another site. This helps to maintain fairness.
<!--SR:!2025-02-17,4,270-->
