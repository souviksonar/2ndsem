**1. PARALLEL AND DISTRIBUTED DATABASES**

*   **Parallel Database:** Improves performance by parallelizing operations (loading data, building indexes, evaluating queries).
*   **Distributed Database:** Data stored across multiple independent sites.

**1.1 ARCHITECTURES FOR PARALLEL DATABASES**

*   **Shared Memory:** CPUs share common memory.
*   **Shared Disk:** CPUs have private memory but shared access to disks.
*   **Shared Nothing:** CPUs have independent memory and disk; communicate via network. Most scalable.
    *   **Advantages:** Linear Speed Up, Linear Scale Up

**1.2 PARALLEL QUERY EVALUATION**

*   **Relational Query Execution Plan:** Graph of relational algebra operators.
*   **Pipelined Parallelism:** Operator consumes output of another operator.
*   **Data Partitioning:** Divide data horizontally across disks for parallel processing.
    *   **Round Robin:** Assign tuples to processors in a round-robin fashion.
    *   **Hash:** Use a hash function to assign tuples to processors.
    *   **Range:** Partition data based on ranges of sort key values.
        *   **Data Skew:** Uneven distribution of data, leading to performance bottlenecks.

**1.3 PARALLELIZING INDIVIDUAL OPERATIONS**

*   **Bulk Loading and Scanning:** Read pages in parallel; merge results.
*   **Sorting:** Redistribute tuples using range partitioning; sort locally.
*   **Joins:** Partition relations; perform smaller joins in parallel.

**1.4 DISTRIBUTED DATABASES**

*   **Goal:** Data physically distributed but logically integrated (transparent to user).
*   **Properties:**
    *   **Distributed Data Independence:** Access data without knowing location.
    *   **Distributed Transaction Atomicity:** Transactions atomic across sites.
*   **Types:**
    *   **Homogeneous:** Same DBMS software at all sites.
    *   **Heterogeneous:** Different DBMS software at different sites.
*   **Architectures:**
    *   **Client-Server:** Clients handle UI; servers manage data and transactions.
        *   **Advantages:** Simple, efficient client resource utilization, better UI
    *   **Collaborating Server:** Servers cooperate to execute transactions spanning multiple sites.
    *   **Middleware:** Software layer coordinating queries/transactions across independent servers.

**1.5 STORING DATA IN DDBS**

*   **Fragmentation:** Break relation into smaller fragments stored at different sites.
    *   **Horizontal:** Fragments are subsets of rows.
    *   **Vertical:** Fragments are subsets of columns.
*   **Replication:** Store copies of relations/fragments at multiple sites.
    *   **Advantages:** Increased data availability, faster query evaluation.
*   **Distributed Catalog Management:**
    *   **Naming Objects:** Using Local name and Birth site field to uniquely identify each fragment.
    *   **Catalog Structure:** Centralized, Fully Distributed
    *   **Distributed Data Independence:**  User should be able to query without knowing the location.

**1.5.4 Distributed query processing:**

*   **Factors:** Network transfer cost is significant.
*   **Optimization Goal:** Reduce data transfer.
*   **Nonjoin Queries:** select queries evaluated at different sites.
*   **Joins:** Expensive, so plan properly.

**1.5.4.3 Ship to one site:**

*   Compute join at a single site by transferring data.

**2.5.2 Semi joins and bloomjoins:**

*   **Semijoin:** Reduce data shipped by sending only necessary tuples.
    *   **Steps:** 1. Send projection. 2. Join at receiving site. 3. Send reduced data.
*   **Bloomjoin:** Similar to semijoin, but uses a bit-vector to filter out tuples.

**1.5.4.4 Cost-Based Query Optimization:**

*   **Challenges:** Communication cost, data replication, site autonomy.

**1.6 DISTRIBUTED CONCURRENCY CONTROL AND RECOVERY**

*   **Issues:**
    *   **Distributed Concurrency Control:** Manage locks, detect deadlocks across sites.
    *   **Distributed Recovery:** Ensure atomicity of transactions across sites.
*   **Problems:** Multiple data copies, site failures, communication link failures, distributed commit, distributed deadlock.
*   **Lock Management:**
    *   **Centralized:** Single site manages all locks.
    *   **Primary Copy:** Lock managed at site with primary copy.
    *   **Fully Distributed:** Lock managed at site with the copy being accessed.
*   **Distributed Deadlock Detection:**
    *   **Centralized:** Periodically send local waits-for graphs to a central site.
    *   **Hierarchical:** Group sites hierarchically; construct waits-for graphs at each level.
    *   **Simple:** Abort transaction if it waits longer than a timeout.
*   **Distributed Recovery:**
    *   **Goal:** All sub-transactions commit or none commit.
    *   **Two-Phase Commit (2PC) Protocol:**
        *   **Phase 1 (Prepare):** Coordinator asks subordinates to prepare.
        *   **Phase 2 (Commit/Abort):** Coordinator decides based on responses.
