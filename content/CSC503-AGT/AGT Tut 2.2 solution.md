# Merge Sort Algorithm

## Algorithm

### **MergeSort**(*A*, *p*, *r*)

**Input:** An array *A* and indices *p* and *r* such that *p* ≤ *r*.
**Output:** The array *A* sorted in ascending order from index *p* to *r*.

```
if p < r
    q = ⌊(p + r) / 2⌋
    MergeSort(A, p, q)
    MergeSort(A, q + 1, r)
    Merge(A, p, q, r)
```
---
### **Merge**(*A*, *p*, *q*, *r*)

**Input:** An array *A* and indices *p*, *q*, and *r* such that *p* ≤ *q* < *r*, and subarrays *A*[*p*..*q*] and *A*[*q*+*1*..*r*] are sorted.
**Output:** The merged sorted subarray *A*[*p*..*r*].

```
n1 = q - p + 1
n2 = r - q
Let L[1..n1 + 1] and R[1..n2 + 1] be new arrays
for i = 1 to n1
    L[i] = A[p + i - 1]
for j = 1 to n2
    R[j] = A[q + j]
L[n1 + 1] = ∞
R[n2 + 1] = ∞
i = 1
j = 1
for k = p to r
    if L[i] <= R[j]
        A[k] = L[i]
        i = i + 1
    else
        A[k] = R[j]
        j = j + 1
```

## Time Complexity Analysis using the Recursion Tree Method

### **1. Recurrence Relation:**

The time complexity of Merge Sort can be expressed by the following recurrence relation:

*$T(n) = 2T(n/2) + \Theta(n)$*

where:

*   *$T(n)$* is the time complexity for an input of size *n*.
*   *$2T(n/2)$* represents the time to sort the two halves of the array recursively.
*   *$\Theta(n)$* represents the time to merge the two sorted halves (the `Merge` procedure).

### **2. Recursion Tree:**

The recursion tree for this relation looks like this:

```
                    T(n) = cn
                   /      \
              T(n/2)    T(n/2)  = cn/2 + cn/2 = cn
             /    \      /    \
          T(n/4) T(n/4) T(n/4) T(n/4) = cn/4 + cn/4 + cn/4 + cn/4 = cn
           /  \    /  \   /  \    /  \
          ...    ...   ...   ...       = cn
                                        .
                                        .
                                        .
      T(1) T(1) ...                        = cn (logarithmic level)
```

### **3. Observations from the Tree:**

*   Each level of the tree has a total cost of *$cn$*.
*   The height of the tree is *$\log_2 n$*. This is because at each level, the problem size is halved, and we continue until we reach subproblems of size *$1$*.

### **4. Total Time Complexity:**

Since each of the *$\log_2 n$* levels costs *$cn$*, the total cost is:

*$T(n) = cn \cdot \log_2 n = \Theta(n \log n)$*

**Therefore, the time complexity of Merge Sort is *$\Theta(n \log n)$*.**
