1.  **Equivalence of Relational Algebra Expressions:**

    $\sigma_{salary < 75000}(\Pi_{salary}(instructor)) \equiv \Pi_{salary}(\sigma_{salary < 75000}(instructor))$

2.  **Basic Cost Estimation:**

    $b * t_T + S * t_S$
    (where *b* is the number of block transfers, $t_T$ is the time to transfer one block, *S* is the number of seeks, and $t_S$ is the time for one seek)

3.  **Linear Search (A1) - General Case:**

    Cost = $b_r + 1$  (where $b_r$ is the number of blocks in relation r)

4.  **Linear Search (A1) - Selection on Key Attribute:**

    Cost = $(b_r / 2) + 1$

5.  **Primary Index, Equality on Key (A2):**

    Cost = $(h_i + 1) * (t_T + t_S)$  (where $h_i$ is the height of the index)

6.  **Primary Index, Equality on Nonkey (A3):**

    Cost = $h_i * (t_T + t_S) + t_S + t_T * b$ (where *b* is the number of blocks containing matching records)

7.  **Secondary Index, Equality on Nonkey (A4) - Single Record (Candidate Key):**

     Cost = $(h_i + 1) * (t_T + t_S)$

8.  **Secondary Index, Equality on Nonkey (A4) - Multiple Records:**

    Cost = $(h_i + n) * (t_T + t_S)$ (where *n* is the number of matching records)

9. **Conjunction:**
    $\sigma_{\theta_1 \land \theta_2 \land ... \land \theta_n}(r)$

10. **Disjunction:**

     $\sigma_{\theta_1 \lor \theta_2 \lor ... \lor \theta_n}(r)$

11. **Negation:**
    $\sigma_{\neg \theta}(r)$

12. **Number of Merge Passes (External Sort-Merge):**

     $\lceil \log_{\lfloor M/b_b \rfloor - 1}(b_r / M) \rceil$ (where M is memory size, $b_b$ is buffer block per run and $b_r$ blocks for relation r)

13. **Total Block Transfers (External Sort-Merge):**

     $b_r * (2 * \lceil \log_{\lfloor M/b_b \rfloor - 1}(b_r / M) \rceil + 1)$

14. **Total Number of Seeks (External Sort-Merge):**

    $2 \lceil b_r / M \rceil + \lceil b_r / b_b \rceil * (2 \lceil \log_{\lfloor M/b_b \rfloor - 1}(b_r / M) \rceil - 1)$

15. **Nested-Loop Join (Worst Case Block Transfers):**

    $n_r * b_s + b_r$ (where $n_r$ is the number of tuples in r, $b_s$ is the number of blocks in s, and $b_r$ is number of blocks in r)

16. **Nested-Loop Join (Worst Case Seeks):**

    $n_r + b_r$

17. **Nested-Loop Join (Smaller Relation in Memory):**

    $b_r + b_s$ (block transfers and 2 seeks)

18. **Block Nested-Loop Join (Worst Case):**

     $b_r * b_s + b_r$ (block transfers) + $2 * b_r$ (seeks)

19. **Block Nested-Loop Join (Best Case):**

     $b_r + b_s$ (block transfers) + 2 (seeks)

20. **Improved Block Nested-Loop Join:**

      Cost = $\lceil b_r / (M-2) \rceil * b_s + b_r$ (block transfers) + $2 \lceil b_r / (M-2) \rceil$ (seeks)

21. **Indexed Nested-Loop Join:**

      Cost = $b_r * (t_T + t_S) + n_r * c$  (where *c* is the cost of traversing the index and fetching matching tuples)

22. **Merge-Join Cost:**

     $b_r + b_s$ (block transfers) + $\lceil b_r / b_b \rceil + \lceil b_s / b_b \rceil$ (seeks) + (cost of sorting if relations are unsorted)

23. **Hash function mapping**

     $h$ maps $JoinAttrs$ values to $\{0, 1,..., n\}$

24. **Partitioning tuples**
     Each tuple $t_r \in r$ is put in partition $r_i$ where $i = h(t_r[JoinAttrs])$.
     Each tuple $t_s \in s$ is put in partition $s_i$, where $i = h(t_s[JoinAttrs])$.

25. **Number of Partitions (Hash-Join, Fudge Factor):**

     $n = \lceil b_s / M \rceil * f$  (where *f* is a fudge factor, typically around 1.2)

26. **Number of Passes for Recursive Partitioning (Hash-Join):**
    $\lceil log_{\lfloor M/b_b \rfloor -1}(b_s/M) \rceil$

27. **Cost of Hash-Join (No Recursive Partitioning):**

     $3(b_r + b_s) + 4 * n_h$ (block transfers) + $2(\lceil b_r / b_b \rceil + \lceil b_s / b_b \rceil)$ (seeks)

28. **Cost of Hash-Join (With Recursive Partitioning):**

    $2(b_r + b_s) \lceil \log_{\lfloor M/b_b \rfloor - 1}(b_s / M) \rceil + b_r + b_s$ (block transfers) +
    $2(\lceil b_r / b_b \rceil + \lceil b_s / b_b \rceil) \lceil \log_{\lfloor M/b_b \rfloor - 1}(b_s / M) \rceil$ (seeks)

29. **Cost of Hash-Join (Build Input in Memory):**

    $b_r + b_s$

30. **Complex Joins (Conjunctive)**

     $r \bowtie_{\theta_1 \land \theta_2 \land ... \land \theta_n} s$

31.  **Complex Joins simplification**

       $r \bowtie_{\theta_i} s$

32. **Condition simplification:**
      $\theta_1 \land ... \land \theta_{i-1} \land \theta_{i+1} \land ... \land \theta_n$
33. **Complex Joins (Disjunctive)**

    $r \bowtie_{\theta_1 \lor \theta_2 \lor ... \lor \theta_n} s$
34. **Complex Joins expanded**

    $(r \bowtie_{\theta_1} s) \cup (r \bowtie_{\theta_2} s) \cup ... \cup (r \bowtie_{\theta_n} s)$
35. **Outer Join Notation**
     $r \rightrightarrows \xleftarrow{} s$
36. **Non participating tuples**
    In $r \rightrightarrows \xleftarrow{} s$, non participating tuples are those in $r - \Pi_R(r \bowtie s)$

37.  **Index Entry Structure:**

    `search-key | pointer` (This isn't a formula, but a representation of structure)

38.  **B+-Tree Properties (Children):**

    Each node that is not a root or a leaf has between $\lceil n/2 \rceil$ and $n$ children.

39.  **B+-Tree Properties (Leaf Node Values):**

    A leaf node has between $\lceil (n-1)/2 \rceil$ and $n-1$ values.

40.  **B+-Tree Properties (Root - Non-Leaf):**

    If the root is not a leaf, it has at least 2 children.

41.  **B+-Tree Properties (Root - Leaf):**

    If the root is a leaf, it can have between 0 and $(n-1)$ values.

42.  **B+-Tree Node Key Ordering:**

    $K_1 < K_2 < K_3 < ... < K_{n-1}$

43.  **Leaf Node Pointer Ordering (L<sub>i</sub> and L<sub>j</sub> are leaf nodes, i < j):**

    $L_i$'s search-key values are less than or equal to $L_j$'s search-key values.

44.  **Non-Leaf Node Pointer Rules (P<sub>1</sub>):**

    All the search-keys in the subtree to which $P_1$ points are less than $K_1$.

45.  **Non-Leaf Node Pointer Rules (P<sub>i</sub>, 2 ≤ i ≤ n-1):**

     All the search-keys in the subtree to which $P_i$ points have values greater than or equal to $K_{i-1}$ and less than $K_i$.

46. **Non-Leaf Node Pointer Rules (P<sub>n</sub>):**

    All the search-keys in the subtree to which $P_n$ points have values greater than or equal to $K_{n-1}$.

47. **B+-Tree Height Bound:**

   If there are K search-key values, the height is no more than $\lceil \log_{\lceil n/2 \rceil}(K) \rceil$

48. **Specific B+-Tree Height Calculation (Example):**

    $log_{50}(1,000,000) = 4$

49. **Non-Unique Key Search Range:**
    Search for $a_i = v$ becomes a range search on the composite key, with range $(v, -\infty)$ to $(v, +\infty)$.

50. **Splitting Leaf Node, number of values in the orignal node**
    Place the first $\lceil n/2 \rceil$ in the original node
51. **Splitting a non-leaf node**
   Copy $P_1, K_1, ..., K_{\lceil n/2 \rceil -1}, P_{\lceil n/2 \rceil}$ from M back to N.
   Copy $P_{\lceil n/2 \rceil+1}, K_{\lceil n/2 \rceil +1}, ..., K_n, P_{n+1}$from M to newly allocated node $N'$.
    Insert $(K_{\lceil n/2 \rceil}, N')$ into parent N.

52. **LSM Tree Level Size Threshold**

  Size threshold for $L_{i+1}$ tree is $k$ times size threshold for $L_i$ tree

53. **Bitmap Index - AND Operation:**

    $100110 \ AND \ 110011 = 100010$

54. **Bitmap Index - OR Operation:**

    $100110 \ OR \ 110011 = 110111$

55. **Bitmap Index - NOT Operation:**

    $NOT \ 100110 = 011001$

56. **Bitmap Index - Example Query:**

    Males with income level L1:  $10010 \ AND \ 10100 = 10000$
57. **Lexicographic Ordering Condition**
    $(a_1, a_2) < (b_1, b_2)$ if either $a_1 < b_1$ or $a_1 = b_1$ and $a_2 < b_2$.
58. **B+-Tree redistribution:**
     Involving 2 siblings in redistribution results in each node having at least $\lceil 2n/3 \rceil$ entries.
