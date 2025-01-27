

## **1. PARALLEL AND DISTRIBUTED DATABASES**

*   **Q: What is a parallel database system?**

    *   **A:** A parallel database system is one that seeks to improve performance through parallel implementation of various operations such as loading data, building indexes, and evaluating queries.
*   **Q: What is a distributed database system?**

    *   **A:** In a distributed database system, data is physically stored across several sites, and each site is typically managed by a DBMS that is capable of running independently of the other sites.

## **1.1 ARCHITECTURES FOR PARALLEL DATABASES**

*   **Q: What are the three main architectures proposed for building parallel databases?**

    *   **A:** The three main architectures are:
        1. Shared-memory system
        2. Shared-disk system
        3. Shared-nothing system
*   **Q: Briefly describe the shared-memory architecture.**

    *   **A:** In a shared-memory system, multiple CPUs are attached to an interconnection network and can access a common region of main memory.
*   **Q: Briefly describe the shared-disk architecture.**

    *   **A:** In a shared-disk system, each CPU has a private memory and direct access to all disks through an interconnection network.
*   **Q: Briefly describe the shared-nothing architecture.**

    *   **A:** In a shared-nothing system, each CPU has local main memory and disk space, but no two CPUs can access the same storage area; all communication between CPUs is through a network connection.
*   **Q: What are the advantages of shared nothing architecture?**
    *   **A:** a) Linear Speed Up: the time taken to execute operations decreases in proportion to the increase in the number of CPU's and disks
        b) Linear Scale Up: the performance is sustained if the number of CPU's and disks are increased in proportion to the amount of data.

## **1.2 PARALLEL QUERY EVALUATION**

*   **Q: What is a relational query execution plan?**

    *   **A:** A relational query execution plan is a graph of relational algebra operators, and the operators in a graph can be executed in parallel.
*   **Q: What is pipelined parallelism?**

    *   **A:** If an operator consumes the output of a second operator, we have pipelined parallelism.
*   **Q: What is Data Partitioned parallel Evaluation?**

    *   **A:** Each individual operator can also be executed in parallel by partitioning the input data and then working on each partition in parallel and then combining the result of each partition. This approach is called Data Partitioned parallel Evaluation.
*   **Q: What are the ways in which data partitioning can be done?**

    *   **A:** Data partitioning can be done in the following ways:
        1. Round Robin Partitioning
        2. Hash Partitioning
        3. Range Partitioning
*   **Q: Explain Round Robin Partitioning.**

    *   **A:** If there are *n* processors, the *i*th tuple is assigned to processor *i* mod *n*.
*   **Q: Explain Hash Partitioning.**

    *   **A:** A hash function is applied to (selected fields of) a tuple to determine its processor.
*   **Q: Explain Range Partitioning.**

    *   **A:** Tuples are sorted (conceptually), and *n* ranges are chosen for the sort key values so that each range contains roughly the same number of tuples; tuples in range *i* are assigned to processor *i*.
*   **Q: What is data skew in range partitioning?**

    *   **A:** Range partitioning can lead to data skew; that is, partitions with widely varying numbers of tuples across partitions or disks. Skew causes processors dealing with large partitions to become performance bottlenecks.

## **1.3 PARALLELIZING INDIVIDUAL OPERATIONS**

*   **Q: How can bulk loading and scanning be parallelized?**

    *   **A:** Pages can be read in parallel while scanning a relation, and the retrieved tuples can then be merged if the relation is partitioned across several disks. If a relation has associated indexes, any sorting of data entries required for building the indexes during bulk loading can also be done in parallel.
*   **Q: How can sorting be parallelized?**

    *   **A:** Sorting could be done by redistributing all tuples in the relation using range partitioning. Each processor then sorts the tuples assigned to it, and the sorted results can be combined.
*   **Q: How can joins be parallelized?**

    *   **A:** The join operation can be parallelized by decomposing it into a collection of *k* smaller joins by partitioning both relations (e.g., A and B) into a collection of *k* logical partitions. If the same partitioning function is used for both relations, the union of the *k* smaller joins will compute the join of A and B.

## **1.4 DISTRIBUTED DATABASES**

*   **Q: What is the abstract idea of a distributed database?**

    *   **A:** The abstract idea of a distributed database is that the data should be physically stored at different locations, but its distribution and access should be transparent to the user.
*   **Q: What are the two main properties a distributed database should exhibit?**

    *   **A:**
        1. Distributed Data Independence: The user should be able to access the database without needing to know the location of the data.
        2. Distributed Transaction Atomicity: The concept of atomicity should be distributed for the operation taking place at the distributed sites.
*   **Q: What is a Homogeneous Distributed Database?**
    *   **A:** Homegeneous Distributed Database is where the data stored across multiple sites is managed by same DBMS software at all the sites.
*   **Q: What is a Heterogeneous Distributed Database?**
    *   **A:** Heterogeneous Distributed Database is where multiple sites which may be autonomous are under the control of different DBMS software.
*   **Q: What are the three architectures of DDBs?**
    *   **A:**  Client-Server, Collaborating Server, and Middleware.
*   **Q: Describe the Client-Server architecture in distributed databases.**

    *   **A:** A Client-Server system has one or more client processes and one or more server processes. Clients are responsible for user-interface issues, and servers manage data and execute transactions.
*   **Q: Describe the Collaborating Server architecture.**

    *   **A:** In a Collaborating Server system, we can have a collection of database servers, each capable of running transactions against local data, which cooperatively execute transactions spanning multiple servers.
*   **Q: Describe the Middleware architecture.**

    *   **A:** A Middleware system is a special server, a layer of software that coordinates the execution of queries and transactions across one or more independent database servers.
*   **Q: What are the advantages of Client-Server architecture?**
    *   **A:** 1. Simple to implement because of the centralized server and separation of functionality.
        2. Expensive server machines are not underutilized with simple user interactions which are now pushed on to inexpensive client machines.
        3. The users can have a familiar and friendly client side user interface rather than unfamiliar and unfriendly server interface

## **1.5 STORING DATA IN DDBS**

*   **Q: What are the two main concepts involved in data storage in DDBs?**

    *   **A:** Fragmentation and Replication.
*   **Q: What is fragmentation in distributed databases?**

    *   **A:** Fragmentation is the process in which a relation is broken into smaller relations called fragments and possibly stored at different sites.
*   **Q: What are the two types of fragmentation?**

    *   **A:**
        1. Horizontal Fragmentation
        2. Vertical Fragmentation
*   **Q: Explain Horizontal Fragmentation.**

    *   **A:** In Horizontal Fragmentation, the original relation is broken into a number of fragments, where each fragment is a subset of rows. The union of the horizontal fragments should reproduce the original relation.
*   **Q: Explain Vertical Fragmentation.**

    *   **A:** In Vertical Fragmentation, the original relation is broken into a number of fragments, where each fragment consists of a subset of columns. The system often assigns a unique tuple id to each tuple in the original relation so that the fragments, when joined again, should form a lossless join.
*   **Q: What is replication in distributed databases?**

    *   **A:** Replication occurs when we store more than one copy of a relation or its fragment at multiple sites.
*   **Q: What are the advantages of replication?**

    *   **A:**
        1. Increased availability of data
        2. Faster query evaluation
*   **Q: What is distributed catalog management concerned with?**
    *   **A:** It's related to the unique identification of each fragment that has been either partitioned or replicated.
*   **Q: How a global name can be assigned to an object in a distributed environment?**
    *   **A:** This can be implemented by using the following two
        fields:-
        1. Local name field – locally assigned name by the site where
        the relation is created. Two objects at different sites can
        have same local names.
        2. Birth site field - indicates the site at which the relation is
        created and where information about its fragments and
        replicas is maintained.
*   **Q: What is the use of a Catalog Structure?**
    *   **A:** A centralized system catalog is used to maintain the
        information about all the transactions in the distributed
        database but is vulnerable to the failure of the site
        containing the catalog.
*   **Q: What is Distributed Data Independence?**
    *   **A:** It means that the user should be able to query the
        database without needing to specify the location of the
        fragments or replicas of a relation which has to be done
        by the DBMS

## **1.5.4 Distributed query processing:**

*   **Q: What are the factors which complicate query processing in a distributed system?**
    *   **A:** One of the factors is cost of transferring the data over network.
    This data includes the intermediate files that are transferred to
    other sites for further processing or the final result files that may
    have to be transferred to the site where the query result is
    needed.
*   **Q: What is the optimization goal of a DDBMS query optimization algorithm?**
    *   **A:** Hence, DDBMS query optimization algorithms consider the goal
        of reducing the amount of data transfer as an optimization
        criterion in choosing a distributed query execution strategy.
*   **Q: What are Nonjoin Queries in a Distributed DBMS?**
    *   **A:** Non Join queries are basically select queries which can be performed on horizontally or vertically fragmented data. The DBMS will answer this query by evaluating it both sites and then taking the union of the answer.
*   **Q: Why Joins of a relation at different sites can be very expensive?**
    *   **A:** Because large amount of data need to be transferred over the network if the join is not planned properly.

## **1.5.4.3 Ship to one site:**

*   **Q: What are the three possibilities to compute the result at one site?**
    *   **A:** There are three possibilities to compute the result at one site:
    • Ship the Sailors from London to Paris and carry out the join.
    • Ship the Reserves form Paris to London and carry out the
    join.
    • Ship both i.e. Sailors and Reserves to the site where the
    query was posed and compute the join.
*   **Q: What is the disadvantage of fetching data as needed?**
    *   **A:** A large amount of data might be transferred over the network.

## **2.5.2 Semi joins and bloomjoins:**

*   **Q: What is the main objective of a Semijoin?**
    *   **A:** Identify the tuples that are guaranteed not to join with any other tuples and avoid shipping them.
*   **Q: What are the steps involved in a Semijoin?**
    *   **A:** The basic idea of Semijoins can be proceed in three steps:

1. At London compute the projection of Sailors onto the join columns, and ship this projection to Paris.
2. At Paris, compute the natural join of the projection received from the first site with the Reserves relation. The result of this join is called the reduction of Reserves with respect to Sailors because only those Reserves tuples in the reduction will join with tuples in the Sailors relation. Therefore, ship the reduction of Reserves to London, rather than the entire Reserves relation.
3. At London, compute the join of the reduction of Reserves with Sailors.

*   **Q: When is Semijoin especially useful?**
    *   **A:** Semijoin is especially useful in conjunction with a selection on one of the relations.
*   **Q: What is a Bloomjoin?**
    *   **A:** A Bloomjoin is similar to a semijoin, but instead of shipping the projection of the join column, a bit-vector is created and shipped. The bit-vector is used to filter out tuples that will definitely not join, thus reducing the amount of data transferred.
*   **Q: What are the steps of a Bloomjoin?**
    *   **A:** Step 1:
        The main difference is that a bit-vector is shipped in first step,
        instead of the projection of Sailors.

        A bit-vector (some chosen tuple) of size k is computed by
        hashing each tuple of Sailors into the range 0 to k-1 and
        setting bit I to 1 if some tuple hashes to I and 0 otherwise.

        Step 2:
        The reduction of Reserves is computed by hashing each tuple
        of Reserves (using the sid field) into the range 0 to k-1, using
        the same hash function which is used to construct the bit-
        vector and discard the tuples whose hash values corresponds
        to 0 bit.

        Because no Sailors tuples hash to such an i and no Sailors
        tuples can join with any Reserves tuple that is not in the
        reduction.
*   **Q: What are the challenges associated with Cost-Based Query Optimization in a distributed database?**
    *   **A:** Communication cost must be considered. If we have several
        copies of a real time then we will have to decide which copy to
        use.

        If the individual sites are run under the control of different DBMS
        then the autonomy of each site must be respected while doing
        global query planning.

## **1.6 DISTRIBUTED CONCURRENCY CONTROL AND RECOVERY**

*   **Q: What are the main issues with respect to distributed transactions?**

    *   **A:**
        1. Distributed Concurrency Control: How to manage locks and detect deadlocks in a distributed environment.
        2. Distributed Recovery: Ensuring that either all or none of a transaction's actions persist across multiple sites, even in the presence of failures.
*   **Q: What are some problems that arise in a distributed DBMS environment for currency control and recovery?**
    *   **A:** These includes the following:
    Dealing with multiple copies of the data items:
    Failure of individual sites:
    Failure of communication links:
*   **Q: What are the different ways in which lock management can be distributed?**

    *   **A:**
        1. Centralized
        2. Primary copy
        3. Fully Distributed
*   **Q: Explain Centralized lock management.**

    *   **A:** A single site is in charge of handling lock and unlock requests for all objects.
*   **Q: Explain Primary copy lock management.**

    *   **A:** One copy of each object is designated as the primary copy. All requests to lock or unlock a copy of these objects are handled by the lock manager at the site where the primary copy is stored.
*   **Q: Explain Fully Distributed lock management.**

    *   **A:** Requests to lock or unlock a copy of an object stored at a site are handled by the lock manager at the site where the copy is stored.
*   **Q: What is a distributed deadlock?**

    *   **A:** A distributed deadlock occurs when transactions at different sites are waiting for each other in a cycle, where each transaction is waiting for a lock held by another transaction at a different site.
*   **Q: What are the algorithms to detect distributed deadlocks?**
    *   **A:** 1. Centralized Algorithm
        2. Hierarchical Algorithm
        3. Simple Algorithm
*   **Q: How does the centralized algorithm for distributed deadlock detection work?**

    *   **A:** It consists of periodically sending all local waits-for graphs to some one site that is responsible for global deadlock detection. At this site, the global waits-for graphs is generated by combining all local graphs.
*   **Q: How does the hierarchical algorithm for distributed deadlock detection work?**

    *   **A:** This algorithm groups the sites into hierarchies, and each node in the hierarchy constructs a waits-for graph that reveals deadlocks involving only sites contained in the subtree rooted at that node.
*   **Q: How does the simple algorithm for distributed deadlock detection work?**
    *   **A:**  If a transaction waits longer than some chosen time-out interval, it is aborted.
*   **Q: Why is recovery more complicated in a distributed DBMS?**

    *   **A:** Recovery is more complicated because new kinds of failures can arise (communication link failures, remote site failures), and either all sub-transactions of a given transaction must commit or none must commit, despite any combination of site and link failures.
*   **Q: What is the Two-Phase Commit (2PC) protocol?**

    *   **A:** The Two-Phase Commit protocol is a protocol used to ensure that all sub-transactions of a distributed transaction either commit or abort uniformly.
*   **Q: What are the two phases of the 2PC protocol?**

    *   **A:**
        1. **Prepare phase:** The coordinator sends a "Prepare" message to each subordinate. Subordinates respond with "Yes" (ready to commit) or "No" (abort).
        2. **Commit/Abort phase:** If the coordinator receives "Yes" from all subordinates, it sends a "Commit" message. Otherwise, it sends an "Abort" message. Subordinates acknowledge the final decision.