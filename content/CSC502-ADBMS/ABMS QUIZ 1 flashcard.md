Okay, here's the first set of quiz questions based on the provided PDF content, formatted as requested:

#flashcards/Primary_Foreign_Key_Relationship
QUESTION:  A primary key, when combined with a foreign key, creates what kind of relationship between tables?
OPTIONS:
A) Parent-child relationship
B) Many-to-many relationship
C) Network model
D) None of the above
??
SOLUTION:
A) Parent-child relationship. This is the standard relationship formed, establishing a link between the primary key in one table and the foreign key in another.

#flashcards/SQL_Queries
QUESTION: Consider the SQL query: `Select deptName from Employee where sex='M' group by deptName having avg (salary)>(select avg (salary) from Employee)`.  What does this query return?
OPTIONS:
A) The names of departments where the average male salary is greater than the overall average salary in the company.
B) The names of departments where the average salary (of all employees) is greater than the overall average salary.
C) The names of departments where the average male salary is greater than the average salary of all employees in that *specific* department.
D) The names of departments where the average male salary is greater than the average salary of all male employees in the company.
??
SOLUTION:
A) The names of departments where the average male salary is greater than the overall average salary in the company. The outer query's `having` clause compares the average male salary of each department to the result of the subquery, which calculates the average salary across *all* employees in the `Employee` table.

#flashcards/Disk_Capacity_Calculation
QUESTION: A disk pack has 16 surfaces, 128 tracks per surface, and 256 sectors per track. Each sector stores 512 bytes. What are the total capacity of the disk pack and the number of bits required to address a specific sector, respectively?
OPTIONS:
A) 256 MB, 19 bits
B) 256 MB, 28 bits
C) 512 MB, 20 bits
D) 64 GB, 28 bits
??
SOLUTION:
A) 256 MB, 19 bits.
*   **Capacity Calculation:**
    *   Total sectors = 16 surfaces * 128 tracks/surface * 256 sectors/track = 524288 sectors
    *   Total capacity = 524288 sectors * 512 bytes/sector = 268435456 bytes = 256 MB (since 1 MB = 1024 * 1024 bytes)
*   **Bits for Sector Addressing:**
    *   We need to find the smallest integer  `n`  such that  $2^n \ge 524288$
    *   $2^{19} = 524288$, so 19 bits are required.

#flashcards/B+_Tree_Degree
QUESTION: A B+ tree index is built on the `Name` attribute of the `STUDENT` relation.  Names are 8 bytes, disk blocks are 512 bytes, and index pointers are 4 bytes. What is the best choice for the degree (number of pointers per node) of the B+ tree?
OPTIONS:
A) 24
B) 42
C) 34
D) 43
??
SOLUTION:
D) 43
Let `p` be the degree of the B+ tree. The size of a node is limited by the block size (512 bytes). Each node contains `p` pointers and `p-1` keys.
So, $4p + 8(p-1) \le 512$
$4p + 8p - 8 \le 512$
$12p \le 520$
$p \le \frac{520}{12} \approx 43.33$
Since the degree must be an integer, the largest possible value for `p` is 43.

#flashcards/Referential_Integrity
QUESTION:  Given relations R(a, b, c) and S(d, e, f), where 'd' in S is a foreign key referencing the primary key 'a' of R. Which of the following operations could violate referential integrity?
OPTIONS:
A) Insert into R and Delete from S
B) Insert into S and Delete from R
C) Delete from R only
D) Insert into S only
??
SOLUTION:
B) Insert into S and Delete from R.
*   Inserting into S with a value of 'd' that doesn't exist as 'a' in R violates referential integrity.
*   Deleting from R a row where the value of 'a' is referenced by 'd' in some row of S violates referential integrity.

#flashcards/Clustering_Index
QUESTION: Select the *correct* statements about clustering indexes.
OPTIONS:
A) A clustering index is defined on fields that are of type key and ordering.
B) A clustering index is defined on fields that are of type non-key and non-ordering.
C) A clustering index is defined on fields that are of type key and non-ordering
D) A clustering index is defined on fields that are of type non-key and ordering
??
SOLUTION: A and D are correct.
A clustering index is defined on fields that are of type key and ordering. OR, a clustering index is defined on non-key and ordering.

#flashcards/B+_Tree_Leaf_Order
QUESTION:  In a B+ tree, the block size is 1KB (1024 bytes), data record pointers are 7 bytes, value fields are 9 bytes, and block pointers are 6 bytes. What is the order of a leaf node?
OPTIONS:
A) 68
B) 86
C) 46
D) 63
??
SOLUTION:
D) 63
Let `n` be the order of the leaf node.  Leaf nodes store (value, data record pointer) pairs.
The space occupied by a leaf node is:  $n * (9 + 7) + 6 \le 1024$  (The +6 is for the block pointer to the next leaf node).
$16n + 6 \le 1024$
$16n \le 1018$
$n \le \frac{1018}{16} = 63.625$
Since `n` must be an integer, the maximum value (order) is 63.

#flashcards/ER_Diagram_to_Relational_Model
QUESTION: Two entities, P1 and P2, have single-valued attributes.  R1 is a one-to-many relationship from P1 to P2, and R2 is a many-to-many relationship between P1 and P2. R1 and R2 have no attributes of their own. What is the *minimum* number of tables needed to represent this in the relational model?
OPTIONS:
A) 4
B) 5
C) 3
D) 2
??
SOLUTION:
C) 3
*   One table for P1.
*   One table for P2.
*   One table for the many-to-many relationship R2 (since it cannot be merged into either P1 or P2).  The one-to-many relationship R1 can be represented by including the primary key of P1 as a foreign key in the table for P2.

#flashcards/Normal_Forms
QUESTION: Which of the following statements about normal forms is FALSE?
OPTIONS:
A) Lossless, dependency-preserving decomposition into 3NF is always possible.
B) Any relation with two attributes is in BCNF.
C) Lossless, dependency-preserving decomposition into BCNF is always possible.
D) BCNF is stricter than 3NF.
??
SOLUTION:
C) Lossless, dependency-preserving decomposition into BCNF is *not* always possible. This is a well-known limitation of BCNF.

#flashcards/Relational_Schema_Normalization
QUESTION: The relation schema `StudentPerformance(name, courseNo, rollNo, grade)` has the following functional dependencies:
```
name, courseNo -> grade
rollNo, courseNo -> grade
name -> rollNo
rollNo -> name
```
What is the highest normal form of this relation schema?
OPTIONS:
A) 4NF
B) 2NF
C) BCNF
D) 3NF
??
SOLUTION:
B) 2NF.
*   The candidate keys are {name, courseNo} and {rollNo, courseNo}.
*   `name -> rollNo` and `rollNo -> name` violate BCNF and 3NF because `name` and `rollNo` are parts of candidate keys, but not full keys themselves. They are determinants but not superkeys.
   However, they do not violate 2NF definition.

#flashcards/Functional_Dependencies_Instance
QUESTION: Given the relational instance:

| X   | Y   | Z   |
| --- | --- | --- |
| 2   | 5   | 3   |
| 2   | 6   | 4   |
| 2   | 7   | 4   |
| 4   | 3   | 3   |
Which of the following functional dependencies are satisfied by this instance? (Select all that apply)
OPTIONS:
A) Y -> X
B) Z -> Y
C) YZ -> X
D) XY -> Z
E) X -> Z
F) XZ -> Y
G) Y -> Z
??
SOLUTION:
A, D, and G are correct.
A) Y -> X : For every Y value, there is only one corresponding X. 5->2, 6->2, 7->2, 3->4
D) XY -> Z: For every unique combination of X and Y, there is a single Z
G) Y -> Z: For every Y, only one Z is NOT true. For instance Y=6, Z=4, and Y=7 has Z=4.

#flashcards/Functional_Dependency_Closure
QUESTION: Given the functional dependencies:  AB->CD, AF->D, DE->F, C->G, F->E, G->A. Which of the following is FALSE?
OPTIONS:
A) {CF}+ = {ACDEFG}
B) {BG}+ = {ABCDG}
C) {AF}+ = {ACDEFG}
D) {AB}+ = {ABCDFG}
??
SOLUTION:
C) is False
*   **{CF}+:**  Start with CF.  C->G, so add G: CFG.  F->E, so add E: CFGE.  G->A, so add A: CFGEA.  AF->D, add D, ACDEFG.
*   **{BG}+:** Start with BG. G->A, so add A: BGA. AB->CD, so add C and D: BGACD
*    **{AF}+:** Start with AF, AF->D, add D, so AFD. D and E gives F, already have F, and F gives E. Add E, so AFDE. DE->F, and F->E, already present, and E->Nothing. C->G, G->A. So, Add G and A, Result is AFDEG. *Since C is not present, this is not equal to {ACDEFG}*
* **{AB}+**: Start with AB. AB->CD, add C,D. ABCD. C gives G, add G. ABCDG. G gives A. F gives E, need D to go to E, which we have!. AB->CD,AF->D, DE->F, C->G, F->E, G->A. so, {AB}+ contains A,B,C,D,F,G.

#flashcards/B+_Tree_vs_Binary_Search_Tree
QUESTION: Why are B+ trees preferred over binary search trees for indexing database relations?
OPTIONS:
A) Data transfer from disks is in blocks.
B) Database relations have a large number of records.
C) B+ trees require less memory than binary search trees.
D) Database relations are sorted on the primary key.
??
SOLUTION:
A) Data transfer from disks is in blocks.  B+ trees are optimized for disk access, minimizing the number of disk reads required to locate a record.  Binary search trees do not have this optimization and can lead to many disk accesses for large datasets. Although B and B+ is efficient for large records (choice B), The primary reason is data transfer from disks is in blocks.

#flashcards/B+_Tree_Splits
QUESTION:  Key values 10, 3, 6, 8, 4, 2, 1 are inserted into an initially empty B+ tree. The order of internal nodes is 3 (maximum 3 pointers), and the order of leaf nodes is 2 (maximum 2 data items). How many times will leaf nodes split?
OPTIONS:
A) 3
B) 5
C) 4
D) 2
??
SOLUTION:
A) 3
1.  **10, 3:** Leaf node [3, 10]
2.  **6:** Leaf node splits: [3, 6], [10] - *Split 1*
3.  **8:** Leaf nodes: [3, 6], [8, 10]
4.  **4:** Leaf nodes: [3, 4], [6], [8, 10] - *Split 2*
5. **2**: Leaf nodes: [2,3], [4,6], [8,10]
6. **1**: Leaf nodes: [1,2], [3], [4,6], [8,10] *Split 3*

#flashcards/SQL_Query_Equivalence
QUESTION: Consider the table `employee(empId, name, department, salary)`.  Two queries are designed to find employees with a higher salary than *anyone* in department 5:
Q1: `Select e.empId From Employee e where not exists (Select * From employee s Where s.department ="5" and s.salary>=e.salary)`
Q2: `Select e.empId From employee e where e.salary > Any(Select distinct salary From employee s Where s.department="5")`
Which query is correct?
OPTIONS:
A) Q1 is the correct query
B) Q2 is the correct query
C) Neither Q1 nor Q2 is the correct query.
D) All of the above
??
SOLUTION:
A) Q1 is the correct query. Q1 uses a correlated subquery with `NOT EXISTS` to check if there are any employees in department 5 with a salary greater than or equal to the current employee's salary. If no such employee exists, the current employee's `empId` is selected.  Q2 uses `ANY`, which would select employees whose salary is greater than *at least one* employee in department 5, not necessarily *all* employees in department 5.

#flashcards/Decomposition_Testing
QUESTION: Relation R is decomposed using functional dependencies F, and relation S is decomposed using functional dependencies G. One decomposition is BCNF, the other is 3NF, but it's unknown which is which. To guarantee identification, which test should be used (assuming closures of F and G are available)?
OPTIONS:
A) Lossless-join
B) Dependency-preservation
C) 3NF Definition
D) BCNF definition
??
SOLUTION:
D) BCNF definition. Check each dependency in the closure of F and G against the decomposed relations. If *any* dependency violates the BCNF condition (determinant must be a superkey) in a decomposition, then that decomposition is *not* BCNF.  The one that *doesn't* violate BCNF is the BCNF decomposition, and by elimination, the other is the 3NF decomposition.

#flashcards/Multivalued_Dependencies
QUESTION: Consider these implications about functional and multivalued dependencies. How many are valid?
(i) If P->>Q and P->>R then P->QR
(ii) If P->Q and P->R then P->>QR
(iii) If P->>QR then P->Q then P->>R
(iv) If P->QR then P->>Q and P->> *R, where C is a typo and it should be R*
OPTIONS:
A) 2
B) 1
C) 0
D) 3
??
SOLUTION:
B) 1.  Only (iv) is generally valid. It is a property that if a functional dependency P->QR holds, then P multidetermines both Q and R.

#flashcards/SQL_Null_Comparisons
QUESTION: In SQL, relations can have `NULL` values.  Comparisons with `NULL` are usually treated as `unknown`.  If we change the rules so that *all* comparisons with `NULL` are treated as `false`, which of the following pairs are *not* equivalent?
OPTIONS:
A) p=5 and not(not(p=5))
B) p=5 and p>4 and p<6, where p is an integer
C) None of the above
D) p≠5 and not(p=5)
??
SOLUTION:
D) p≠5 and not(p=5).  If `p` is `NULL`, then `p≠5` evaluates to `false` (because we're treating all comparisons with `NULL` as `false`).  However, `not(p=5)` also evaluates to `not(false)`, which is `true`. Therefore, they are *not* equivalent in this scenario.

#flashcards/Schema_Decomposition_NF
QUESTION: Consider schema R=(P Q R S) with dependencies P→Q, Q→R, R→S, and S→P. Let R be decomposed into R1 and R2, such that R1 ∩ R2 = ∅. What is the Normal Form of this Decomposition?
OPTIONS:
A) not in 2NF
B) None of the above
C) in 3NF
D) not in 3NF
??
SOLUTION:
A and D. The correct answers, Not in 2NF, Not in 3NF.
Since the intersection is empty, there is no common attribute. This is the worst case of decomposition. The original relation R is in BCNF (and all lower normal forms). Since the intersection is null, all functional dependencies are lost. Therefore this decomposed relation is Not in 2NF, 3NF or BCNF.

#flashcards/Prime_Attribute_Dependency
QUESTION:  Which statement is FALSE?

OPTIONS:
A) A prime attribute can be transitively dependent on a key in a 3NF relation.
B) Any relation with two attributes is in BCNF.
C) A prime attribute can be transitively dependent on a key in a BCNF relation.
D) A relation in which every key has only one attribute is in 2NF.
??
SOLUTION:
C) A prime attribute can be transitively dependent on a key in a BCNF relation. This is false.  In BCNF, *no* attribute (prime or non-prime) can be transitively dependent on a key.  Transitive dependency is eliminated in BCNF.
