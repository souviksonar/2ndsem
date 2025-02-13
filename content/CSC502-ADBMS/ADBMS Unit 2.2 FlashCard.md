

#flashcards/Query_Processing_Overview
QUESTION: What are the three basic steps in query processing?
OPTIONS:
A) Parsing, Optimization, Execution
B) Translation, Optimization, Evaluation
C) Parsing and translation, Optimization, Evaluation
D) Compilation, Optimization, Execution
??
SOLUTION:
The correct answer is C. The basic steps are: 1. Parsing and translation, where the query is converted into its internal form and then into relational algebra. 2. Optimization, where the best evaluation plan is chosen. 3. Evaluation, where the query-execution engine takes the plan and executes it.

#flashcards/Query_Optimization
QUESTION:  The relational algebra expression $\sigma_{salary < 75000}(\Pi_{salary}(instructor))$ is equivalent to which of the following expressions?
OPTIONS:
A)  $\Pi_{salary}(\sigma_{salary >= 75000}(instructor))$
B)  $\Pi_{salary}(\sigma_{salary < 75000}(instructor))$
C) $\sigma_{salary > 75000}(\Pi_{salary}(instructor))$
D)  $\sigma_{salary = 75000}(\Pi_{salary}(instructor))$
??
SOLUTION:
The correct answer is B.  This demonstrates the principle of pushing down selections in a query tree to optimize execution, as selecting before projecting reduces the number of tuples processed.

#flashcards/Query_Cost_Metrics
QUESTION:  In query cost estimation, which factor is typically considered the most dominant?
OPTIONS:
A) CPU cost
B) Network communication cost
C) Disk access cost
D) Memory access cost
??
SOLUTION:
The correct answer is C. Disk access is usually the most significant contributor to query cost because disk I/O is significantly slower than other operations.

#flashcards/Selection_Operations
QUESTION: What is the estimated cost, in terms of block transfers, for a linear search (Algorithm A1) on a relation `r` where the selection is on a key attribute, and `b_r` represents the number of blocks containing records from relation `r`?
OPTIONS:
A) $b_r + 1$
B) $b_r$
C) $(b_r / 2) + 1$
D) $2 * b_r$
??
SOLUTION:
The correct answer is C. Since it's a key attribute, the search can stop once the record is found. On average, half the blocks will be searched. We add 1 for the initial seek.

#flashcards/Selection_Using_Indices
QUESTION:  For a primary index with equality on a non-key attribute (Algorithm A3), what is the cost in terms of  $t_T$ (time to transfer one block), $t_S$ (time for one seek), $h_i$ (height of the index), and $b$ (number of blocks containing matching records)?
OPTIONS:
A)  $(h_i + 1) * (t_T + t_S)$
B)  $h_i * (t_T + t_S) + t_S + t_T * b$
C)  $(h_i + b) * (t_T + t_S)$
D) $h_i + b$
??
SOLUTION:
The correct answer is B.  The cost includes traversing the index ($h_i * (t_T + t_S)$), one seek to get to the data blocks ($t_S$), and then reading the $b$ blocks containing the matching records ($t_T * b$).

#flashcards/Selection_Using_Indices_Secondary
QUESTION:  When using a secondary index for equality selection on a *non-candidate* key, retrieving *n* matching records, the cost can be very expensive. What is the general cost formula in this case, given $h_i$ is the height of the index, and $t_T$ and $t_S$ are the times for block transfer and seek, respectively?
OPTIONS:
A) $(h_i + 1) * (t_T + t_S)$
B) $h_i * (t_T + t_S) + t_S + t_T * n$
C) $(h_i + n) * (t_T + t_S)$
D)  $n * (h_i + 1) * (t_T + t_S)$
??
SOLUTION:
The correct answer is C. Each matching record might reside on a different block, leading to a potential seek and block transfer for each.

#flashcards/Complex_Selections
QUESTION:  For a conjunctive selection $\sigma_{\theta_1 \land \theta_2 \land ... \land \theta_n}(r)$, if using Algorithm A7 (conjunctive selection using one index), which strategy is employed?
OPTIONS:
A)  Always use a composite index.
B) Choose the combination of $\theta_i$ and algorithm (A1-A7) that yields the least cost for $\sigma_{\theta_i}(r)$, then test other conditions.
C)  Always use a linear scan.
D) Use the index that corresponds to the first condition, $\theta_1$.
??
SOLUTION:
The correct answer is B.  The strategy aims to minimize cost by selecting the most efficient single-condition selection first.

#flashcards/Sorting
QUESTION: External sort-merge is preferred for sorting relations that do not fit in memory. If *M* denotes the memory size in pages, what is the initial step in external sort-merge?
OPTIONS:
A) Merge all runs in a single pass.
B) Create sorted runs of size M.
C) Directly apply a multi-way merge.
D) Sort the entire relation using quicksort.
??
SOLUTION:
The correct answer is B.  The relation is broken down into sorted runs of size *M* (memory size), which are then merged.

#flashcards/External_Sort_Merge_Passes
QUESTION: If *N* is the initial number of runs and *M* is the memory size (in pages), and $N \ge M$, how many runs are merged in each pass of the external sort-merge algorithm (assuming $b_b$ buffer blocks per run)?
OPTIONS:
A)  N
B) M
C) M - 1
D) M/b_b - 1
??
SOLUTION:
The correct answer is D. Up to $M/b_b -1 $ runs can be merged in a single pass. One block is needed for the output buffer.

#flashcards/External_Sort_Merge_Cost
QUESTION: What is the total number of block transfers for external sorting (approximately) if $b_r$ is the number of blocks in the relation, $M$ is the number of memory blocks, and we use $b_b$ buffer blocks?
OPTIONS:
A)  $b_r * (2 * \lceil \log_{M-1}(b_r / M) \rceil + 1)$
B)  $b_r * \lceil \log_{M-1}(b_r / M) \rceil$
C) $b_r * (2 * \lceil \log_{M/b_b-1}(b_r / M) \rceil + 1)$
D) $2 * b_r$
??
SOLUTION:
The correct answer is C. This considers the block transfers for creating initial runs and for each merge pass. The "+ 1" accounts for the initial run creation.

#flashcards/Join_Operations
QUESTION: Which join algorithm is suitable for *any* kind of join condition (theta join)?
OPTIONS:
A) Merge-join
B) Hash-join
C) Nested-loop join
D) Indexed nested-loop join
??
SOLUTION:
The correct answer is C. Nested-loop join can handle any join condition, although it can be very inefficient.

#flashcards/Nested_Loop_Join_Cost
QUESTION: In the worst-case scenario for a nested-loop join of relations `r` and `s`, with `n_r` tuples in `r` and `b_s` blocks in `s`, and only enough memory for one block of each relation, what is the approximate number of *block transfers*?
OPTIONS:
A) $n_r + b_s$
B) $n_r * b_s$
C) $n_r * b_s + b_r$
D) $b_r + b_s$
??
SOLUTION:
The correct answer is C. For each tuple in `r`, the entire `s` relation (in blocks) is scanned.

#flashcards/Block_Nested_Loop_Join
QUESTION:  In a block nested-loop join, how does the algorithm proceed compared to the basic nested-loop join?
OPTIONS:
A)  It uses an index on the inner relation.
B) It compares each tuple of the outer relation with each tuple of the inner relation.
C) It compares each *block* of the outer relation with each *block* of the inner relation.
D) It uses a hash function to partition the relations.
??
SOLUTION:
The correct answer is C.  This reduces the number of scans of the inner relation.

#flashcards/Indexed_Nested_Loop_Join
QUESTION: In an indexed nested-loop join, what replaces file scans under ideal conditions?
OPTIONS:
A) Hash lookups
B) Index lookups
C) Sort operations
D) Merge operations
??
SOLUTION:
The correct answer is B. An index on the inner relation's join attribute allows for efficient lookups.

#flashcards/Merge_Join_Requirement
QUESTION: What type of join(s) can merge-join be used for?
OPTIONS:
A) Only equi-joins
B) Only natural joins
C) Equi-joins and natural joins
D) Any theta join
??
SOLUTION:
The correct answer is C. Merge-join relies on the join attributes being comparable for sorting.

#flashcards/Hash_Join_Applicability
QUESTION: For what types of joins is hash-join applicable?
OPTIONS:
A) Only theta joins
B) Only natural joins
C) Equi-joins and natural joins
D) All join types
??
SOLUTION:
The correct answer is C. Hash-join works by hashing the join attributes to the same bucket.

#flashcards/Hash_Join_Algorithm
QUESTION: In the hash-join algorithm, what are the roles of the two relations, `r` and `s`, typically called?
OPTIONS:
A) Left and Right input
B) Build and Probe input
C) Inner and Outer input
D) Sorted and Unsorted input
??
SOLUTION:
The correct answer is B.  's' is typically the build input (used to create the hash table), and 'r' is the probe input (used to probe the hash table).

#flashcards/Hash_Join_Recursive_Partitioning
QUESTION: When is recursive partitioning required in hash-join?
OPTIONS:
A) Always
B) When the build relation fits in memory
C) When the number of partitions *n* is greater than the number of memory pages *M*
D) When the probe relation is larger than the build relation
??
SOLUTION:
The correct answer is C.  If a partition doesn't fit in memory, it needs to be further partitioned.

#flashcards/Hash_Join_Overflow
QUESTION: What is hash-table overflow in the context of hash-join?
OPTIONS:
A) When the hash function generates too many collisions.
B) When a partition of the build relation (s_i) does not fit in memory.
C) When the probe relation is too large.
D) When the memory buffer is full.
??
SOLUTION:
The correct answer is B. This requires overflow resolution techniques.

#flashcards/Other_Operations_Duplicate_Elimination
QUESTION: Which two techniques can be used for duplicate elimination?
OPTIONS:
A) Indexing and Hashing
B) Sorting and Indexing
C) Hashing and Sorting
D) Partitioning and Sorting
??
SOLUTION:
C. Both sorting (bringing duplicates together) and hashing (placing duplicates in the same bucket) can be used.

#flashcards/Other_Operations_Aggregation
QUESTION:  For the `AVG` aggregate function, what values are typically kept during optimized aggregation processing?
OPTIONS:
A) Only the sum
B) Only the count
C) The sum and the count
D) The minimum and maximum values
??
SOLUTION:
The correct answer is C. The average can be calculated at the end by dividing the sum by the count.

#flashcards/Set_Operations_Hashing
QUESTION: When performing set operations (union, intersection, difference) using hashing, how are the relations initially processed?
OPTIONS:
A)  They are sorted.
B) They are joined using a nested-loop join.
C) They are partitioned using the same hash function.
D) An index is built on both relations.
??
SOLUTION:
The correct answer is C. This ensures that potentially matching tuples end up in corresponding partitions.

#flashcards/Outer_Join_Modification_Merge_Join
QUESTION: How can a merge-join algorithm be modified to compute a left outer join (r ⟕ s)?
OPTIONS:
A) Only output matching tuples.
B) Output `t_r` padded with nulls for every tuple `t_r` from `r` that *does not* match any tuple in `s`.
C) Output all tuples from 's' regardless of match.
D) Reverse the order of 'r' and 's'.
??
SOLUTION: The correct answer is B. This ensures that all tuples from the left relation ('r') are included in the result.

#flashcards/Evaluation_of_Expressions_Materialization
QUESTION: What does "materialization" mean in the context of query evaluation?
OPTIONS:
A) Passing tuples directly between operations.
B) Storing the results of intermediate expressions on disk.
C) Using indexes to speed up evaluation.
D) Optimizing the query plan.
??
SOLUTION:
The correct answer is B. Materialization involves storing intermediate results, which can be costly.

#flashcards/Evaluation_of_Expressions_Pipelining
QUESTION: What is the primary advantage of pipelining over materialization?
OPTIONS:
A) It always uses less memory.
B) It avoids storing temporary relations on disk.
C) It is always applicable.
D) It is simpler to implement.
??
SOLUTION:
The correct answer is B. Pipelining passes results directly, avoiding the I/O cost of materialization.

#flashcards/Pipelining_Types
QUESTION: What are the two main ways pipelines can be executed?
OPTIONS:
A) Top-down and Bottom-up
B) Demand-driven and Producer-driven
C) Serial and Parallel
D) Indexed and Non-indexed
??
SOLUTION:
The correct answer is B. These describe how tuples are requested and produced within the pipeline.

#flashcards/Pipelining_Iterator_Model
QUESTION: In demand-driven pipelining, what is the common interface used to implement operations?
OPTIONS:
A) Cursor
B) Iterator
C) Function
D) Procedure
??
SOLUTION:
The correct answer is B.  An iterator provides `open()`, `next()`, and `close()` methods.

#flashcards/Pipelining_Limitations
QUESTION: Which of the following join algorithms is *not* inherently suitable for pipelining without modification?
OPTIONS:
A) Indexed nested-loop join
B) Block nested-loop join
C) Hash-join
D) Nested-loop join
??
SOLUTION:
The correct answer is C.  Hash-join, in its basic form, requires building a hash table before producing results, making it less suitable for pure pipelining.  Hybrid hash-join addresses this.

#flashcards/Query_Cost_Formula_Components
QUESTION: The basic query cost formula includes terms for block transfers and seeks. What is the time to transfer one block often represented as?
OPTIONS:
  A) $t_S$
  B) $t_T$
  C) $b_r$
  D) $h_i$
??
SOLUTION: The correct answer is B. $t_T$ is used for the time to transfer one block.

#flashcards/Hybrid_Hash_Join_Memory
QUESTION: Hybrid hash-join is most useful when memory size (M) and the size of build relation ($b_s$) relate as:
OPTIONS:
  A) $M << \sqrt{b_s}$
  B) $M = \sqrt{b_s}$
  C) $M >> \sqrt{b_s}$
  D) $M = b_s$
??
SOLUTION: C. The formula indicates M should be considerably larger that the square root of the build relation size.
