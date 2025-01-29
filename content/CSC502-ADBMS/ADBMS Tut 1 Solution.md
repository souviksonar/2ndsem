Okay, let's solve these functional dependency problems step-by-step, using MathJax for all variables and equations:

### 1. Candidate Key(s) of R(A, B, C, D) with FDs: A -> B, B -> C, C -> D

*   **Find Closure of A:**
    *   *$A^+$* = *$\{A, B, C, D\}$* (Since *$A \rightarrow B$*, *$B \rightarrow C$*, and *$C \rightarrow D$*)
    *   *$A$* is a superkey because its closure contains all attributes.
*   **Check for Minimality:**
    *   Since no proper subset of *{A}* can determine all attributes, *A* is a candidate key.

**Answer:** The candidate key is *$\{A\}$*.

### 2. Closure of {C} and Superkey Check in R(A, B, C, D, E) with FDs: A -> BC, CD -> E, B -> D, E -> A

*   **Find Closure of C:**
    *   *$C^+$* = *$\{C\}$* (No other attribute can be determined from *$C$* alone)
*   **Superkey Check:**
    *   *$C$* is not a superkey because *$C^+$* does not contain all attributes of *R*.

**Answer:** *$C^+$* = *$\{C\}$*. *$C$* is not a superkey.

### 3. Lossless Decomposition of R(A, B, C, D) into R1(A, B, C) and R2(A, D) with FDs: A -> B, C -> D

*   **Check Common Attributes:**
    *   *R1* ∩ *R2* = *{A}*
*   **Check if Common Attributes are a Key for Either Relation:**
    *   *$A^+$* = *$\{A, B\}$* (using *$A \rightarrow B$*)
    *   *$A$* is not a key for *R1* because it doesn't determine *C*.
    *   *$A$* is a key for *R2* because it doesn't have other attributes except for itself.

**Answer:** The decomposition is **not** lossless because *A* is a key for *R2* but not for *R1*.

### 4. 2NF Check for R(A, B, C, D, E) with FDs: AB -> C, BC -> D, CD -> E

*   **Find Candidate Key:**
    *   *$(AB)^+$* = *$\{A, B, C, D, E\}$* (Using *$AB \rightarrow C$*, then *$BC \rightarrow D$*, then *$CD \rightarrow E$*)
    *   *$AB$* is a candidate key.
    *   *$(BC)^+$* = *$B,C,D,E$* (Using $BC\rightarrow D$, $CD\rightarrow E$)
    *   *$BC$* is not candiadte key because *$B$* can be determined from *$A$*.
    *   *$(CD)^+$* = *$C,D,E$*
    *   *$CD$* is not a candidate key.
*   **Check for Partial Dependencies:**
    *   *$AB \rightarrow C$*: No partial dependency as *$C$* is directly determined by the whole key.
    *   *$BC \rightarrow D$*: Partial dependency exists because *$B$* is part of the candidate key *$AB$*, and *$B$* alone can determine *D* (because *B* can be determined from *A*, so *AB* can determine *B*, *B* can determine *D*).

**Answer:** The relation is **not** in 2NF because there is a partial dependency: *$AB \rightarrow D$* through *$BC \rightarrow D$*.

### 5. Dependency-Preserving Decomposition of R(A, B, C, D) into R1(A, B), R2(B, C), R3(C, D) with FDs: A -> B, B -> C, C -> D

*   **Check if all FDs are Preserved:**
    *   *$A \rightarrow B$*: Preserved in *R1*.
    *   *$B \rightarrow C$*: Preserved in *R2*.
    *   *$C \rightarrow D$*: Preserved in *R3*.

**Answer:** The decomposition is **dependency-preserving**.

### 6. Highest Normal Form of R(A, B, C, D) with FDs: A -> B, B -> C, AB -> D

*   **Candidate Key:**
    *   *$\{A\}^+$* = *$\{A, B, C, D\}$*
    *   *$\{A\}$* is the only candidate key.
*   **2NF:** Satisfied (no partial dependencies).
*   **3NF:** Satisfied (no transitive dependencies).
*   **BCNF:** Not satisfied. For the non-trivial FD *$B \rightarrow C$*, *B* is not a superkey.

**Answer:** The highest normal form is **3NF**.

### 7. Candidate Key Check for R(A, B, C, D) with FDs: A -> BC, B -> D

*   **Find Closure of A:**
    *   *$A^+$* = *$\{A, B, C, D\}$* (Using *$A \rightarrow BC$*, then *$B \rightarrow D$*)
    *   No proper subset of *{A}* determines all attributes.

**Answer:** *$\{A\}$* **is** a candidate key.

### 8. Candidate Key(s) of R(A, B, C, D, E) with FDs: AB -> C, C -> D, A -> E

*   **Find Closure of AB:**
    *   *$(AB)^+$* = *$\{A, B, C, D, E\}$*
    *   *$\{AB\}$* is a superkey.
*   **Check for Minimality:**
    *   *$A^+$* = *$\{A, E\}$*
    *   *$B^+$* = *$\{B\}$*
    *   Neither *A* nor *B* alone can determine all attributes.

**Answer:** The candidate key is *$\{AB\}$*.

### 9. BCNF Check for R(A, B, C) with FDs: A -> B, B -> C, A -> C

*   **Candidate Key:**
    *   *$\{A\}^+$* = *$\{A, B, C\}$*
    *   *$\{A\}$* is the only candidate key.
*   **BCNF Check:**
    *   For *$A \rightarrow B$*, *$A$* is a superkey.
    *   For *$B \rightarrow C$*, *$B$* is not a superkey.
    *   For *$A \rightarrow C$*, *$A$* is a superkey.

**Answer:** The relation is **not** in BCNF because of the FD *$B \rightarrow C$*, where *$B$* is not a superkey.

### 10. Lossless and Dependency-Preserving Decomposition of R(A, B, C, D) into R1(A, B) and R2(A, C, D) with FDs: A -> B, A -> C, C -> D

*   **Lossless Check:**
    *   *R1* ∩ *R2* = *{A}*
    *   *$A^+$* = *$\{A, B, C, D\}$*
    *   *$\{A\}$* is a key for both *R1* and *R2*.

*   **Dependency-Preserving Check:**
    *   *$A \rightarrow B$*: Preserved in *R1*.
    *   *$A \rightarrow C$*: Preserved in *R2*.
    *   *$C \rightarrow D$*: Preserved in *R2*.

**Answer:** The decomposition is **lossless** and **dependency-preserving**.
