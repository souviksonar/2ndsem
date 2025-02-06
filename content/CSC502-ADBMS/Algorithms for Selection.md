
> [!NOTE] Title
> * *Micro-topic:* A1 (linear search) (Page 695)
> * *Micro-topic:* A2 (clustering index, equality on key) (Page 697)
> * *Micro-topic:* A3 (clustering index, equality on non-key) (Page 697)
> * *Micro-topic:* A4 (secondary index, equality) (Page 697)
> * *Micro-topic:* A5 (clustering index, comparison) (Page 698)
> * *Micro-topic:* A6 (secondary index, comparison) (Page 698)

^13da48

### H4: A1 (Linear Search)

*   **Concept:** The most basic approach. The system scans each block of the relation's file and tests every record against the selection condition.
*   **Applicability:** Always applicable, regardless of file ordering, index availability, or selection condition.
*   **Cost:**
    *   **Block Transfers:** $b_r$ (where $b_r$ is the number of blocks in the relation's file)
    *   **Seeks:** 1 (for the initial seek to start the file scan; additional seeks may be required if the file blocks are not stored contiguously, cost are negligible ).
    * If the selection is equality on a key.
        * Average cost:
            * **Block Transfers:** $b_r/2$
        * Because the search can end when that tuple is found.

*   **Notes:** Simple but can be inefficient for large relations, especially if only a few tuples satisfy the selection condition.

### H4: A2 (Clustering Index, Equality on Key)

*   **Concept:** Uses a B+-tree clustering (primary) index on a key attribute with an equality condition (e.g., `WHERE ID = '12345'`).
*   **Applicability:** Requires a clustering index on the attribute involved in the equality condition.
*  **Assumption**:
    * To model the common situation that the internal nodes of the index are in
the in-memory buffer, $h_i$ can be set to 1.
*   **Cost:**
    *   **Block Transfers:** $(h_i + 1) * (t_T + t_S)$ (where $h_i$ is the height of the B+-tree)
        *   $h_i$ transfers to traverse the index to the leaf.
        *   1 transfer to fetch the record.
    *   **Seeks:** $h_i + 1$ (one seek per level of the tree, plus one for the data block).

*   **Notes:** Very efficient for retrieving a single record based on a key.

### H4: A3 (Clustering Index, Equality on Non-Key)

*   **Concept:** Uses a clustering B+-tree index on a non-key attribute with an equality condition (e.g., `WHERE dept_name = 'Music'`).
*   **Applicability:** Requires a clustering index on the attribute. Because the file is sorted by the non-key clustering index, all tuples with the same indexed attribute value are stored consecutively.
*   **Cost:**
    *   **Block Transfers:** $h_i * (t_T + t_S) + t_S + b * t_T$
        *   $h_i$ transfers to traverse the index to the first leaf with a matching value.
        *   $b$ transfers to read the contiguous blocks containing all matching records (b is number of block containing records).
    *   **Seeks:** $h_i$ seeks for each level of the B+-tree, 1 seek for the first block.
*   **Notes:** Efficient if many records satisfy the condition.

### H4: A4 (Secondary Index, Equality)

*   **Concept:** Uses a secondary (non-clustering) B+-tree index on any attribute (key or non-key) with an equality condition.
*   **Applicability:** Requires a secondary index on the attribute.
*   **Cases:**
    *   **Equality on Key:**
        *   **Cost:** $(h_i + 1) * (t_T + t_S)$. Identical to A2.
    *   **Equality on Non-Key:**
        *   **Worst-Case Cost:** $(h_i + n) * (t_T + t_S)$ (where n is the number of records retrieved).
        *   $h_i$ I/O operations to traverse the index.
            *   Up to $n$ I/O operations to fetch records (one per record, as records may reside on different blocks with no guaranteed order).
        *   Best-Case Cost: will be much less than worst-case in large in-memory buffer.
*   **Notes:** Can be very expensive for non-key attributes if many records match, because each record retrieval may require a separate disk I/O. If secondary index is used on a B+-tree file organization or other file organizations that may require relocation of records, accessing a record through such a secondary index is more expensive.

### H4: A5 (Clustering Index, Comparison)

*   **Concept:** Uses a clustering B+-tree index with a comparison condition (>, >=, <, <=).
*   **Applicability:** Requires a clustering index on the attribute in the comparison.
*   **Cases:**
    *   **$A >= v$ or $A > v$:**
        *   Use the index to find the first tuple where $A >= v$.
        *   Scan the file forward from that point.
    *   **$A < v$ or $A <= v$:**
        *   Scan the file from the beginning until a tuple is found where $A >= v$ or $A >v$, respectively. Do not require index lookup.
        * Index is not useful.
    * **Cost**:
        * Identical to A3, equality on non-key.

### H4: A6 (Secondary Index, Comparison)

*   **Concept:** Uses a secondary B+-tree index with a comparison condition.
*   **Applicability:** Requires a secondary index on the attribute in the comparison.
*   **Process:** Scan index leaf nodes, retrieving records, from the smallest value up to *v* (for < and <=), or from *v* up to the maximum value (for > and >=).
* **Cost:**
        *   *Worst-Case Cost:* $(h_i + n) * (t_T + t_s)$ (where n is the number of records fetched)
    *   **Notes:** Can be *very* inefficient if many records match, because each record may require a separate disk I/O. Should only be used if very few records match.

