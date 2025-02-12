
#flashcards 
**I. Distributed Data Storage and Transparency (5 Questions)**

1.  (MSQ) Which of the following are valid reasons for choosing *vertical* fragmentation over horizontal fragmentation in a distributed database?
    a)  To reduce the amount of irrelevant data accessed by common queries.
    b)  To improve security by separating sensitive attributes.
    c)  To increase data availability in the face of site failures.
    d)  To allow different sites to have different levels of access control to different parts of a relation.
    ??
    a), b), and d). Vertical fragmentation splits *attributes*, allowing separation for security and access control, and potentially reducing data transfer for queries needing only a subset of attributes. It doesn't inherently increase *availability* in the way replication or horizontal fragmentation (across sites) might.

2.  (MCQ) A distributed database uses a naming scheme where relations are named `SiteID.RelationName`.  This scheme *directly* violates which form of data transparency?
    a) Fragmentation Transparency
    b) Replication Transparency
    c) Location Transparency
    d) Network Transparency
    ??
    c) Location Transparency. The name explicitly includes the site ID, revealing the location.

3.  (MSQ)  Which of the following statements about data replication are *true* in the context of distributed systems?
    a) Full replication always provides the best performance for read-heavy workloads.
    b)  Replication can improve both read performance and data availability.
    c)  Replication introduces complexities in maintaining data consistency.
    d) The primary copy method eliminates the need for distributed concurrency control.
    ??
    b) and c).  Full replication can be overkill, even for reads. Replication *does* improve performance and availability but *complicates* consistency. The primary copy method *simplifies* concurrency control, but doesn't eliminate the need for it.

4.  (MCQ)  A distributed database administrator wants to minimize data transfer for a query that accesses a small subset of tuples from a very large relation. The relation is currently *not* fragmented. Which fragmentation strategy would be MOST beneficial?
    a)  Vertical fragmentation.
    b)  Horizontal fragmentation, strategically partitioning based on the query's selection predicate.
    c)  Full replication.
    d)  No fragmentation; use indexes instead.
    ??
    b) Horizontal fragmentation.  Strategically partitioning places the relevant tuples at a single site, minimizing transfer.

5.  (MCQ) Which type of transparency is MOST directly supported by the use of *aliases* in a distributed database system?
	a) Fragmentation Transparency
	b) Network Tranparency
	c) Location Transparency
	d) Data Transparency
    ??
	c) Location Transparency.

---

**II. Distributed Transactions and Commit Protocols (7 Questions)**

6.  (MCQ) In the Two-Phase Commit (2PC) protocol, what happens if a participant site crashes *before* sending any message to the coordinator?
    a) The coordinator assumes the participant voted "commit."
    b) The coordinator assumes the participant voted "abort."
    c) The coordinator waits indefinitely for the site to recover.
    d) The coordinator initiates a three-phase commit protocol.
    ??
    b) The coordinator assumes the participant voted "abort." (Or, more precisely, timed out, which is treated as an abort).

7.  (MSQ) Which of the following are potential drawbacks of the Three-Phase Commit (3PC) protocol compared to 2PC?
    a) Increased message overhead.
    b)  Increased risk of blocking.
    c)  More complex implementation.
    d)  Inability to handle network partitions.
    ??
    a) and c). 3PC has *more* messages and is *more* complex.  It *reduces* blocking risk (under its assumptions) but is still vulnerable to certain network partition scenarios.

8. (MSQ) Which of the following failure scenarios can lead to *blocking* in the standard Two-Phase Commit (2PC) protocol?
    a)  A participant site crashes before sending its vote.
    b)  The coordinator crashes after receiving all votes but before sending the final decision.
    c)  A participant site crashes after sending a "ready" vote but before receiving the final decision.
    d)  The network partitions, isolating the coordinator from some participants.
    ??
    b), c), and d). If a participant hasn't voted (a), the coordinator can unilaterally abort. In the other cases, surviving participants might be unsure of the outcome and blocked.

9.  (MCQ) In persistent messaging, the "exactly-once" delivery guarantee is achieved primarily through:
    a)  Using a three-phase commit protocol.
    b)  Storing messages in a replicated database and using acknowledgments.
    c)  Using a centralized message broker.
    d)  Encrypting messages to prevent loss or duplication.
    ??
    b) Storing messages in a replicated database (or other persistent storage) and using acknowledgments. The sender retries until acknowledged; the receiver checks for duplicates.

10. (MCQ) A system uses persistent messaging for inter-site communication. If a message is marked as "undeliverable" after repeated attempts, what is the typical next step?
    a)  The sending transaction is automatically committed.
    b)  The sending transaction is automatically aborted.
    c)  Application-specific exception handling code is invoked.
    d) The entire distributed system is halted.
    ??
    c) Application-specific exception handling code is invoked.  Persistent messaging doesn't dictate the *meaning* of the message, so the application must decide how to handle delivery failure.

11. (MCQ) In the context of distributed transactions, what is the primary purpose of using a *timeout* mechanism?
     a) To prevent deadlocks
     b) Detect Site failures and network partitions
     c) Ensure exactly-once message delivery
     d) Speed up transaction processing
     ??
     b) Detect Site failures and network partitions

12. (MCQ) In 2PC, what happens if a participating site sends a `<no T>` message to the coordinator?
	 a)  Coordinator sends *commit* message to all participating sites
	 b) Coordinator sends *abort* message to all participating sites
	 c) Coordinator waits for the final decision
	 d) None of the above.
    ??
    b) Coordinator sends *abort* message to all participating sites

---

**III. Concurrency Control and Deadlock Handling (7 Questions)**

1. (MSQ) Which of the following distributed locking approaches are susceptible to a *single point of failure*?
    a)  Single lock manager.
    b)  Distributed lock manager.
    c)  Primary copy.
    d)  Majority protocol.
    ??
    a) and c).  The single lock manager and the primary copy site for each data item are single points of failure.

2. (MCQ) The biased protocol for replicated data is *most* beneficial when:
    a)  Writes are much more frequent than reads.
    b)  Reads are much more frequent than writes.
    c)  Read and write frequencies are roughly equal.
    d)  The network is highly unreliable.
    ??
    b) Reads are much more frequent than writes.  It minimizes overhead for reads.

3. (MSQ) In a distributed system using timestamp-based concurrency control, which of the following techniques can help ensure that timestamps are generated "fairly" across sites?
    a)  Using a centralized timestamp server.
    b)  Using logical clocks that are advanced when a site receives a message with a higher timestamp.
    c)  Using system clocks that are perfectly synchronized using NTP (Network Time Protocol).
    d)  Using a randomly generated timestamp at each site.
    ??
    a), b) , and c).  A centralized server, logical clocks, and synchronized system clocks all contribute to fairness. Random timestamps alone do *not* guarantee fairness.

4. (MCQ) In distributed deadlock detection, a *false cycle* is most likely to be caused by:
    a)  Incorrect implementation of the deadlock detection algorithm.
    b)  Communication delays between sites.
    c)  Simultaneous failure of multiple sites.
    d)  Use of a centralized deadlock detector.
    ??
    b) Communication delays between sites.

5. (MSQ) In a distributed system, which of the following are valid approaches to *deadlock handling*?
    a)  Deadlock prevention using a global wait-for graph.
    b)  Deadlock detection and resolution.
    c)  Timeouts.
    d)  Ignoring deadlocks and relying on application-level recovery.
    ??
    a), b), and c) are all standard approaches.  (d) is sometimes used in practice, but it's not a robust solution.

6. (MSQ) Which of the following information should be included in a *wait-for* graph for deadlock detection?
    a) Transaction ID requesting a lock
    b) Transaction ID holding the lock
    c) Timestamp of the transaction.
    d) Site ID where the transaction runs
    ??
    a), b), and d)

7. (MSQ) Which of the following are the properties of *Quorum Consensus*?
    a) $Q_r + Q_w > S$
    b) $2 * Q_w > S$
    c)  $Q_r > S$
    d) $Q_w < S$
    ??
    a) and b)

---

**IV. Availability, Replication, and Coordinator Selection (6 Questions)**

8. (MCQ) The "read one, write all available" replication protocol is MOST suitable for environments where:
    a