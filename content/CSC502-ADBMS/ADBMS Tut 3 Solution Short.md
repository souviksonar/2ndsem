

**1. Explain the process of Hash Join. How is the hash function used in the join process? What are the phases of hash join?**

**Process:** Hash Join works by partitioning tuples of both relations based on a hash function applied to the join attributes. It then compares tuples only within corresponding partitions.

**Hash Function Use:** The hash function (*h*) maps join attribute values to a range of integers (0 to $n_h$). This determines which partition a tuple belongs to. A good hash function distributes tuples uniformly across partitions.

**Phases:**

1. **Partitioning (Build) Phase:** Both relations (*r* and *s*) are partitioned into $r_0, r_1, ..., r_{n_h}$ and $s_0, s_1, ..., s_{n_h}$ using the hash function *h* on the join attributes.
2. **Probing (Join) Phase:** For each partition *i*, an in-memory hash index is built on $s_i$ (build input). Then, tuples from $r_i$ (probe input) are used to probe this index, finding matching tuples.

**2. When is Hash Join preferred over Nested Loop Join? Under what conditions is Hash Join more efficient?**

**Hash Join Preference:**

*   **Equi-joins:** Hash Join is highly preferred for natural joins and equi-joins (where the join condition is equality).
*   **Larger Relations:** When relations are not very small. Nested loop join is preferred when one of the relation is very small.

**Efficiency Conditions:**

*   When there is enough memory to hold at least the smaller relation's hash partitions (with their index) in memory.
*   When the join attributes have a relatively uniform distribution (to avoid skewed partitions).

**3. What happens in a Hash Join when the smaller relation does not fit into memory? Explain how grace hash join and recursive partitioning work.**

**Smaller Relation Doesn't Fit:**

*   **Recursive Partitioning:** If the smaller (build) relation doesn't fit in memory, the hash join uses *recursive partitioning*. Both relations are partitioned into smaller sub-partitions repeatedly, using different hash functions in each pass, until each build-relation partition (and its hash index) fits in memory.

**Grace Hash Join vs. Recursive Partitioning in simple way:**

Grace hash join is just another name for the standard hash join algorithm using recursive partitioning.

**4. Explain the working of Index Nested Loop Join. How does the presence of an index improve performance?**

**Indexed Nested-Loop Join:**

*   For each tuple in the *outer* relation, an index on the *inner* relation's join attribute is used to find matching tuples directly.

**Performance Improvement:**

*   **Avoids Full Scans:** The index avoids scanning the entire inner relation for each outer tuple.
*   **Faster Lookups:** Index lookups (e.g., using a B+-tree) are significantly faster than linear scans, especially for large relations.

**5. When should we use Index Nested Loop Join instead of Hash Join? Compare performance based on data size and indexing availability.**

**When to Use Indexed Nested-Loop Join:**

*   **Small Outer Relation:** When the outer relation is very small, and the inner has an index on the join attribute.
*   **Selective Joins:** When the join condition is very selective (results in few matching tuples).
* Index is available on inner relation's join attribute.

**Performance Comparison:**

| Factor                  | Indexed Nested-Loop Join                 | Hash Join                                         |
| ----------------------- | ---------------------------------------- | ------------------------------------------------- |
| **Outer Relation Size** | Prefers small                            | Less sensitive to size                            |
| **Inner Relation Size** | Less sensitive to size(because of Index) | Size impacts partitioning and memory needs        |
| **Index Availability**  | *Requires* index on inner join attribute | Index not required (but can improve partitioning) |
| **Join Selectivity**    | Prefers highly selective joins           | Less sensitive to selectivity                     |
| **Memory**              | Requires less memory                     | Requires more memory.                             |

**6. How does an Indexed Nested Loop Join differ from a regular Nested Loop Join? Explain how index lookup reduces the number of comparisons.**

**Difference:**

*   **Regular Nested-Loop:** Scans the *entire* inner relation for *each* tuple in the outer relation.
*   **Indexed Nested-Loop:** Uses an index on the inner relation to find *only* matching tuples for each outer tuple.

**Reduced Comparisons:**

*   The index allows direct access to potentially matching tuples, avoiding comparisons with all tuples in the inner relation.

**7. When does a Nested Loop Join perform better than a Hash Join? Discuss scenarios where Nested Loop Join is preferable.**

**Nested Loop Join Preferable When:**

*   One relation is very small (especially if it fits entirely in memory).
*   Join condition is *not* an equality condition (e.g., range conditions, inequalities), where hash join cannot be used.
*   When indexed nested loop join is applicable and selection condition on outer relation is very selective.

**8. Why is Nested Loop Join considered inefficient for large datasets? How does it compare to Sort-Merge and Hash Join?**

**Inefficiency:**

*   **Quadratic Complexity:** In the worst case (no index, large relations), it has a time complexity of O($n_r * n_s$), where $n_r$ and $n_s$ are the number of tuples in the relations. This means the number of comparisons grows very rapidly with relation size.

**Comparison:**

*   **Sort-Merge Join:** Generally more efficient than nested-loop for large datasets if relations need to be sorted. Complexity is O(n log n) for sorting + O(n) for merging, where n is number of tuples.
*   **Hash Join:** Often the most efficient for large datasets with equi-joins, especially if partitioning can be done in one pass. Complexity is close to O(n) if memory is sufficient.

**9. Hash Join Numerical Problems. Consider two relations R and S: Relation R has 1,000 pages. Relation S has 500 pages. The system has 50 buffer pages. Calculate the I/O cost of performing a Grace Hash Join assuming uniform distribution.**
R has 1000 pages, S has 500 pages, M = 50.

1. **Partitioning Phase:**
    *   Number of partitions:  We need to partition S such that each partition fits within M-1 buffers (leaving 1 for input). So,  $n_h$ > 500 / (50-1) ≈ 10.2, so lets take $n_h$ = 11.

    *   I/O cost to read and write both relations: 2 * (1000 + 500) = 3000 I/Os.

2. **Join (Probing) Phase:**
     Read each partition of R and S once: 1000 + 500 = 1500 I/Os.
3. **Total I/Os:** 3000+1500 = 4500 I/Os

**10. Consider a Hash Join between two tables: Table A has 1,000,000 tuples, each 200 bytes. Table B has 500,000 tuples, each 250 bytes. The block size is 8 KB. Estimate the number of disk I/Os required for the join.**

4. **Calculate Relation Sizes in Blocks:**
    *   $b_A$ = $\lceil$(1,000,000 * 200) / 8192$\rceil$ = 24415 blocks
    *   $b_B$ = $\lceil$(500,000 * 250) / 8192$\rceil$ = 15259 blocks

5. Assume memory size M is greater than $\sqrt{b_B}$ (so recursive partitioning is not required), then Number of I/Os = 3($b_r$+$b_s$) = 3*(24415+15259) = 119022 I/Os.

**11. Index Nested Loop Join Numerical Problems. Consider a table with the following statistics. Outer relation RRR has 10,000 tuples. Inner relation SSS has 1,000,000 tuples. The index lookup cost is 2 I/Os per tuple. Compute the total cost of Index Nested Loop Join.**

*   Outer Relation Scan:  We'll assume we have to scan RRR. Let's say it takes 'x' I/Os to scan RRR.
*   Index Lookups: For each of the 10,000 tuples in RRR, we perform an index lookup costing 2 I/Os. Total index lookup cost: 10,000 * 2 = 20,000 I/Os.
*   **Total Cost:** x + 20,000 I/Os

**12. A database contains two tables: Table A has 10,000 pages. Table B has 2,000 pages. The database system has 20 buffer pages. Compute the I/O cost for Block Nested Loop Join. Compare with the cost of Simple Nested Loop Join Index Nested Loop Join with Clustered vs. Unclustered Index**
* Block Nested Loop Join Cost
    * Outer Relation A, Inner B:
        * $\lceil10000/18\rceil$ * 2000 + 10000 = 1,121,112 I/Os
     * Outer Relation B, Inner A:
         *  $\lceil2000/18\rceil$ * 10000 + 2000 = 1,113,112 I/Os.

* Simple Nested Loop Join.
     *  Using smaller relation B as outer:
          * 2000 + (nB * 10000) I/Os, where nB is number of tuples in relation B.

* Indexed Nested loop join:
     * With clustered index:
        * 2000 + (nB * 1)
     * With unclustered index:
         * 2000 + (nB * 5)

**13. Suppose an Index Nested Loop Join is being performed on the following dataset:**

*   **Outer Relation RRR: 100,000 tuples**
*   **Inner Relation SSS: 500,000 tuples**
*   **SSS is indexed using:**
    *   **Clustered index: Each lookup requires 1 I/O.**
    *   **Unclustered index: Each lookup requires 5 I/Os.**

**Question:**

*   **Compute the I/O cost for both clustered and unclustered index-based joins.**
*   **Which approach is more efficient?**

**Calculations:**

6. **Clustered Index:**
    *   Outer relation scan (assume cost = *x* I/Os to scan RRR).
    *   Index lookups: 100,000 tuples * 1 I/O/lookup = 100,000 I/Os
    *   Total Cost: *x* + 100,000 I/Os

7. **Unclustered Index:**
    *   Outer relation scan (assume cost = *x* I/Os to scan RRR).
    *   Index lookups: 100,000 tuples * 5 I/Os/lookup = 500,000 I/Os
    *   Total Cost: *x* + 500,000 I/Os

**Conclusion:** The clustered index-based join is significantly more efficient because each lookup requires fewer I/Os. The unclustered index requires many more I/Os due to the potential need to fetch data blocks for each matching tuple.
