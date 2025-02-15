

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





30.  **B+-Tree Properties (Children):**
	1. Each node that is not a root or a leaf has between $\lceil n/2 \rceil$ and $n$ children.

31.  **B+-Tree Properties (Leaf Node Values):**
	1. A leaf node has between $\lceil (n-1)/2 \rceil$ and $n-1$ values.

32.  **B+-Tree Properties (Root - Non-Leaf):**
	1. If the root is not a leaf, it has at least 2 children.

33.  **B+-Tree Properties (Root - Leaf):**
	1. If the root is a leaf, it can have between 0 and $(n-1)$ values.