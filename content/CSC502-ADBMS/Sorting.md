


> [!NOTE] Title
> - *Mini-topic:* External Sort-Merge Algorithm (Page 701)
> 	* *Micro-topic:* Figure 15.4 External sorting using sort-merge. (Page 703)
> - *Mini-topic:* Cost Analysis of External Sort-Merge (Page 702)

^a903bf

## External Sort-Merge Algorithm (Page 701)

The External Sort-Merge Algorithm is the most common technique for sorting relations that don't fit in memory. It works in two main stages:

1.  **Run Creation Stage:**
    *   Read `M` blocks of the relation into memory (where `M` is the number of available memory blocks).
    *   Sort the in-memory data using an efficient internal sorting algorithm (like quicksort).
    *   Write the sorted data (a "run") to a temporary file on disk.
    *   Repeat until the entire relation is processed, creating multiple sorted runs (R<sub>i</sub>).

2.  **Merge Stage:**
    *   If Number of Run (N) <= M, one pass merge is enough.
    *   If the number of runs (N) is less than or equal to M, merge them in a single pass using an N-way merge:
        *   Read one block from each run into memory buffers.
        *   Repeatedly find the smallest tuple among all buffers (considering the sort order).
        *   Write the smallest tuple to the output.
        *   If a buffer becomes empty, read the next block from the corresponding run (if any).
    *   If N > M, perform merge in multiple passes.
    *   If the number of runs is greater than M, perform multiple merge passes:
        *   Each pass merges at most `M-1` runs (because one buffer block is for output).
        *   Repeat passes until the number of runs is less than M.
        *   A final pass merges the remaining runs into the sorted result.

### Example
![[CSC502-ADBMS/media/media/2.2 Query procesing.webp]]

[[2.2 Query procesing.pdf#page=18&rect=150,22,591,490|2.2 Query procesing, p.18]]

## Cost Analysis of External Sort-Merge (Page 702)

The cost of external sort-merge is dominated by disk I/O. We can estimate it as follows:

* **b<sub>r</sub>:** Number of blocks containing the relation `r`.
* **M:** number of blocks in the main memory buffer available for sorting.
* **b<sub>b</sub>** number of blocks for buffering input run.

1.  **Run Creation:**
    * Reads every block and writes it out: $2 * b_r$ block transfers.
    * Number of initial runs: $\lceil \frac{b_r}{M} \rceil$

2.  **Merge Stage:**
    * Each pass (except possibly the last) reads and writes every block.
    * With each pass, number of runs decreases by factor of ($\lfloor M/b_b \rfloor -1$).
    * Number of merge passes (excluding last pass): $\lceil \log_{\lfloor M/b_b \rfloor -1} (b_r/M) \rceil$
    * Total number of block transfer except last pass = $2b_r \cdot \lceil \log_{\lfloor M/b_b \rfloor -1} (b_r/M) \rceil$

3.  **Total Block Transfers:** $b_r(2\lceil \log_{\lfloor M/b_b \rfloor -1} (b_r/M) \rceil + 1)$

4. **Disk Seeks:**
    * Run generation phase: $2\lceil b_r / M \rceil$
    * Each merge pass read input: $\lceil b_r/b_b\rceil$ seeks
    * Each merge pass output, if on same disk: $2\lceil b_r/b_b\rceil$ seeks.
    * Total Seeks (excluding the final pass): $2\lceil b_r / M \rceil + \lceil b_r/b_b\rceil(2 \cdot \lceil \log_{\lfloor M/b_b \rfloor -1} (b_r/M) \rceil-1)$
