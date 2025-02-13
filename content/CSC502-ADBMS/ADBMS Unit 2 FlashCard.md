#flashcards/Basic_Concepts
QUESTION: What is a search key in the context of database indexing?
OPTIONS:
A) An encryption key for database security.
B) An attribute or set of attributes used to look up records in a file.
C) A unique identifier for a database table.
D) A password for accessing the database.
??
SOLUTION:
B) A search key is an attribute or set of attributes used to look up records in a file. This is fundamental to how indexing works.

#flashcards/Basic_Concepts
QUESTION:  Index entries typically consist of what two components?
OPTIONS:
??
SOLUTION:
Index entries consist of a `search-key` and a `pointer`.

#flashcards/Index_Types
QUESTION:  What are the two basic kinds of indices?
OPTIONS:
A) Primary and Secondary
B) Clustered and Non-clustered
C) Ordered and Hash
D) Dense and Sparse
??
SOLUTION:
C) The two basic kinds of indices are Ordered indices (where search keys are stored in sorted order) and Hash indices (where search keys are distributed uniformly across "buckets").

#flashcards/Index_Evaluation
QUESTION: List four metrics used to evaluate the effectiveness of an index.
OPTIONS:
??
SOLUTION:
Four common metrics are:
1.  Access time
2.  Insertion time
3.  Deletion time
4.  Space overhead

#flashcards/Ordered_Indices
QUESTION:  A primary index is also known as a ________ index.
OPTIONS:
??
SOLUTION:
A primary index is also known as a `clustering` index.

#flashcards/Ordered_Indices
QUESTION: What is the key difference between a primary index and a secondary index?
OPTIONS:
A) A primary index is always on the primary key, while a secondary index is on any other attribute.
B) A primary index specifies the sequential order of the file, while a secondary index does not.
C) A primary index is dense, while a secondary index is sparse.
D) A primary index uses a B-tree, while a secondary index uses hashing.
??
SOLUTION:
B) A primary index's search key specifies the sequential order of the file, whereas a secondary index specifies an order *different* from the sequential order.

#flashcards/Dense_Indices
QUESTION: In a dense index, how many index records are present relative to the search-key values in the file?
OPTIONS:
A) One index record for each block in the file.
B) One index record for every search-key value in the file.
C) Index records only for some search-key values.
D) The number of index records is independent of the search-key values.
??
SOLUTION:
B) A dense index has one index record for *every* search-key value in the file.

#flashcards/Sparse_Indices
QUESTION:  A sparse index contains index records for ______ some search-key values.
OPTIONS:
??
SOLUTION:
A sparse index contains index records for `only` some search-key values.

#flashcards/Sparse_Indices
QUESTION: When is a sparse index applicable?
OPTIONS:
A) When records are not sequentially ordered.
B) When records are sequentially ordered on the search key.
C) When fast insertion is required.
D) When the index must fit entirely in memory.
??
SOLUTION:
B) Sparse indices are applicable when records are sequentially ordered on the search-key.

#flashcards/Secondary_Indices
QUESTION: Secondary indices must be dense. (True/False)
OPTIONS:
A) True
B) False
??
SOLUTION:
A) True. Secondary Indices have to be dense as per slide 10.

#flashcards/Multilevel_Indices
QUESTION: What is the purpose of using a multilevel index?
OPTIONS:
A) To improve the security of the database.
B) To reduce the space required to store the index.
C) To allow efficient access to the index when it is too large to fit in memory.
D) To provide redundancy in case of index corruption.
??
SOLUTION:
C) Multilevel indices are used when the index is too large to fit in main memory, allowing efficient access by treating the index itself as a file.

#flashcards/Multilevel_Indices
QUESTION: In a multilevel index, the top-level index is typically a ______ index of the lower-level index.
OPTIONS:
??
SOLUTION:
In a multilevel index, the top-level index is typically a `sparse` index of the lower-level index.

#flashcards/Bplus_trees
QUESTION:  In a B+-tree, all paths from the root to a leaf node have the same ______.
OPTIONS:
??
SOLUTION:
In a B+-tree, all paths from the root to a leaf node have the same `length`.

#flashcards/Bplus_Trees
QUESTION: What is the minimum number of children a non-root, non-leaf node in a B+-tree of order *n* can have?
OPTIONS:
A)  $n$
B)  $n - 1$
C)  $\lceil n/2 \rceil$
D)  $2$
??
SOLUTION:
C) $\lceil n/2 \rceil$.  This ensures the tree remains balanced.

#flashcards/Bplus_Trees
QUESTION:  A leaf node in a B+-tree of order *n* must have between _______ and _______ values.
OPTIONS:
??
SOLUTION:
A leaf node in a B+-tree of order *n* must have between  $\lceil (n-1)/2 \rceil$ and $n-1$ values.

#flashcards/Bplus_tree_Nodes
QUESTION: In a B+-tree, if $K_i$ represents the search-key values in a non-leaf node, what is the ordering relationship between them?
OPTIONS:
A) $K_1 > K_2 > K_3 > ... > K_{n-1}$
B) $K_1 < K_2 < K_3 < ... < K_{n-1}$
C) No specific order is required.
D) The order depends on the insertion sequence.
??
SOLUTION:
B) $K_1 < K_2 < K_3 < ... < K_{n-1}$. The search-key values in a B+-tree node are ordered.

#flashcards/Bplus_tree_Leaf_Nodes
QUESTION:  In a B+-tree leaf node, the pointer $P_i$ (for $1 \le i \le n-1$) points to what?
OPTIONS:
??
SOLUTION:
In a B+-tree leaf node, the pointer  $P_i$ points to a file record with search-key value $K_i$.

#flashcards/Bplus_tree_NonLeaf_Nodes
QUESTION: In a B+-tree non-leaf node, what is the relationship between the search keys in the subtree pointed to by $P_1$ and the value of $K_1$?
OPTIONS:
A) All search keys in the subtree are greater than $K_1$.
B) All search keys in the subtree are less than $K_1$.
C) All search keys in the subtree are equal to $K_1$.
D) There is no relationship.
??
SOLUTION:
B) All search keys in the subtree pointed to by $P_1$ are *less than* $K_1$.

#flashcards/Bplus_tree_Queries
QUESTION:  What is the maximum height of a B+-tree with $K$ search-key values and a node order of $n$?
OPTIONS:
??
SOLUTION:
The maximum height is $\lceil \log_{\lceil n/2 \rceil}(K) \rceil$.

#flashcards/Bplus_tree_Queries
QUESTION: The find(v) function for B+ trees returns _______ if no record with search key value *v* exists.
OPTIONS:
??
SOLUTION:
The find(v) function returns `null` if no record with search key value *v* exists.

#flashcards/Bplus_tree_Updates
QUESTION: When inserting a new entry into a B+-tree, if a leaf node is full, what happens?
OPTIONS:
A) The insertion fails.
B) The node is split.
C) The tree is rebalanced globally.
D) A new root node is created.
??
SOLUTION:
B) The node is split, and the split may propagate up the tree.

#flashcards/Bplus_tree_Updates_Insertion
QUESTION: After splitting a leaf node during insertion in a B+-tree, what is inserted into the parent node?
OPTIONS:
A) The smallest key value from the original node.
B) The largest key value from the original node.
C) The smallest key value from the new node, and a pointer to the new node.
D) The largest key value from the new node, and a pointer to the new node.
??
SOLUTION:
C) The smallest key value from the new node, and a pointer to the new node, are inserted into the parent.

#flashcards/Bplus_tree_Updates_Deletion
QUESTION:  When deleting an entry from a B+-tree, if a node becomes underfull (has too few entries), what might happen?
OPTIONS:
A) The tree is immediately rebalanced globally.
B) Siblings are merged, or pointers are redistributed.
C) The deletion is postponed.
D) The root node is deleted.
??
SOLUTION:
B) Siblings may be merged, or pointers may be redistributed between siblings, to maintain the tree's balance properties.

#flashcards/Bplus_tree_Complexity
QUESTION:  What is the worst-case time complexity of inserting or deleting an entry in a B+-tree with K entries and maximum fanout n, in terms of I/O operations?
OPTIONS:
??
SOLUTION:
The worst-case complexity is $O(\log_{\lceil n/2 \rceil}(K))$.

#flashcards/Hashing
QUESTION: What is a "bucket" in the context of static hashing?
OPTIONS:
A) A linked list of overflow records.
B) A unit of storage containing one or more records (or entries).
C) A hash function.
D) The range of possible hash values.
??
SOLUTION:
B) A bucket is a unit of storage that can contain one or more records (or entries, in the case of a hash index).

#flashcards/Hashing_Overflow
QUESTION: What is "overflow chaining" in the context of hash index management?
OPTIONS:
A) Using a chain of hash functions to handle collisions.
B) Linking overflow buckets together in a linked list.
C) Rehashing the entire index when a bucket overflows.
D) Increasing the size of the hash table.
??
SOLUTION:
B) Overflow chaining involves linking overflow buckets of a given bucket together in a linked list.

#flashcards/Dynamic_Hashing
QUESTION: What is a major disadvantage of static hashing compared to dynamic hashing?
OPTIONS:
A) Static hashing is slower for lookups.
B) Static hashing cannot handle insertions.
C) Static hashing requires periodic reorganization as the database grows or shrinks.
D) Static hashing is more complex to implement.
??
SOLUTION:
C) Static hashing's fixed bucket address space leads to performance degradation or wasted space as the database changes size, requiring expensive reorganization.

#flashcards/Multiple_Key_Access
QUESTION: For the query `select ID from instructor where dept_name = "Finance" and salary = 80000`, using separate indices on `dept_name` and `salary`, describe one possible query processing strategy.
OPTIONS:
??
SOLUTION:
One strategy is:
1.  Use the index on `dept_name` to find instructors in the "Finance" department.
2.  For each of those instructors, check if their `salary` is 80000.
(Other valid strategies exist, as described in the PDF).

#flashcards/Bitmap_Indices
QUESTION:  When are bitmap indices most applicable?
OPTIONS:
A) When attributes have a large number of distinct values.
B) When attributes have a relatively small number of distinct values.
C) When frequent updates are expected.
D) When range queries are rare.
??
SOLUTION:
B) Bitmap indices are most applicable when attributes take on a relatively small number of distinct values (e.g., gender, country).

#flashcards/Spatial_Indices
QUESTION: Name one type of query commonly used with spatial data.
OPTIONS:
??
SOLUTION:
Examples include: Nearest neighbor queries, Range queries, Spatial join.
