Okay, here are digital short notes from the provided PDF, formatted for easy readability and with variables and mathematical equations rendered using MathJax:

## Relational Databases

### Integrity Constraints

*   **Relation:** A named, two-dimensional table of data.
    *   Unique name, named columns (attributes), unique rows (records).
    *   Order of columns and rows is irrelevant.
    *   Attribute values are atomic.
*   **Relational Structure:** Expressed by a tuple: `RelationName(Attribute1, Attribute2, ...)`
    *   Example: `EMPLOYEE1(Emp_ID, Name, Dept, Salary)`
*   **Relational Keys:**
    *   **Primary Key:** Uniquely identifies each row.
        *   Example: `EMPLOYEE1(Emp_ID, Name, Dept, Salary)` (Emp\_ID is underlined)
    *   **Composite Key:** Primary key with multiple attributes.
        *   Example: `DEPENDENT(EmpID, Dependent_Name)`
    *   **Foreign Key:** Represents a relationship between two tables. An attribute in one relation that is the primary key of another relation.
        *   Example: `EMPLOYEE1(Emp_ID, Name, Dept_Name,Salary)`, `DEPARTMENT(Dept_Name, Location, Fax)` (Dept\_Name in EMPLOYEE1 is a foreign key)

### Integrity Constraints Types

*   **Domain Constraints:** Define allowable values for an attribute.
    *   Components: domain name, meaning, data type, size, allowable values/range.
*   **Entity Integrity:** Every relation has a primary key; no primary key attribute can be null.
*   **Referential Integrity:** Foreign key value must match a primary key value in the related table (or be null).
    *   **Restrict:** Don't allow delete of "parent" if related rows exist in "dependent".
    *   **Cascade:** Delete "dependent" rows corresponding with the "parent" row to be deleted
    *   **Set-to-Null:** Set foreign key in dependent to null if deleting from parent.

## Relational Database Design

### Pitfalls

*   **Bad Design Leads To:**
    *   Repetition of Information.
    *   Inability to represent certain information.
*   **Design Goals:**
    *   Avoid redundant data.
    *   Represent relationships among attributes.
    *   Facilitate checking of integrity constraints.

### Example of Bad Design

*   `Lending-schema = (branch-name, branch-city, assets, customer-name, loan-number, amount)`
*   **Redundancy:** `branch-name`, `branch-city`, `assets` repeated.
*   **Null Values:** Cannot store branch information without loans.

### Decomposition

*   Break down `Lending-schema` into:
    *   `Branch-schema = (branch-name, branch-city, assets)`
    *   `Loan-info-schema = (customer-name, loan-number, branch-name, amount)`
*   **Rule:** All attributes of original schema (R) must appear in the decomposition (R1, R2):

    $R = R_1 \cup R_2$
*   **Lossless-join decomposition:** For all possible relations r on schema R

    $r = \Pi_{R1}(r) \bowtie \Pi_{R2}(r)$

### Functional Dependencies (FDs)

*   Constraints on legal relations.
*   Value for a set of attributes uniquely determines the value for another set.
*   Generalization of the notion of a key.
*   **Notation:** $\alpha \rightarrow \beta$ ( $\alpha$ functionally determines $\beta$ )
*   **Formal Definition:**
    Let R be a relation schema, $\alpha \subseteq R$ and $\beta \subseteq R$. The functional dependency $\alpha \rightarrow \beta$ holds on R if and only if for any legal relations r(R), whenever any two tuples $t_1$ and $t_2$ of r agree on the attributes $\alpha$, they also agree on the attributes $\beta$. That is,
    $t_1[\alpha] = t_2[\alpha] \Rightarrow t_1[\beta] = t_2[\beta]$

*   **Example:** In `r(A, B)`,  `B → A` holds, but `A → B` does not.

| A   | B   |
| --- | --- |
| 1   | 4   |
| 1   | 5   |
| 3   | 7   |

*   **Superkey:** K is a superkey for relation schema R if and only if $K \rightarrow R$
*   **Candidate Key:** K is a candidate key for R if and only if
    $K \rightarrow R$, and for no $\alpha \subset K, \alpha \rightarrow R$
*   **Trivial FD:** Satisfied by all instances of a relation (e.g., $\alpha \rightarrow \beta$ if $\beta \subseteq \alpha$).

### Closure of a Set of FDs ($F^+$)

*   Set of all FDs logically implied by F.
*   **Armstrong's Axioms:**
    *   **Reflexivity:** If $\beta \subseteq \alpha$, then $\alpha \rightarrow \beta$
    *   **Augmentation:** If $\alpha \rightarrow \beta$, then $\gamma\alpha \rightarrow \gamma\beta$
    *   **Transitivity:** If $\alpha \rightarrow \beta$ and $\beta \rightarrow \gamma$, then $\alpha \rightarrow \gamma$

### Closure of Attribute Sets ($\alpha^+$)

*   Set of attributes functionally determined by $\alpha$ under F.
*   **Algorithm to compute** $\alpha^+$:
    ```
    result := α;
    while (changes to result) do
        for each β → γ in F do
            begin
                if β ⊆ result then result := result ∪ γ
            end
    ```

### Canonical Cover

*   A "minimal" set of FDs equivalent to F, with no redundancies.

### Design Goals Summary

*   BCNF (Boyce-Codd Normal Form)
*   Lossless join
*   Dependency preservation
*   SQL does not provide a direct way of specifying functional dependencies other than superkeys.

### Multivalued Dependencies (MVDs)

*   **Notation:** $\alpha \rightarrow \rightarrow \beta$
*   **Definition:** Let R be a relation schema and let $\alpha \subseteq R$ and $\beta \subseteq R$. The multivalued dependency $\alpha \rightarrow \rightarrow \beta$ holds on R if in any legal relation r(R), for all pairs for tuples $t_1$ and $t_2$ in r such that $t_1[\alpha] = t_2[\alpha]$, there exist tuples $t_3$ and $t_4$ in r such that:
    $t_1[\alpha] = t_2[\alpha] = t_3[\alpha] = t_4[\alpha]$
    $t_3[\beta] = t_1[\beta]$
    $t_3[R - \beta] = t_2[R - \beta]$
    $t_4[\beta] = t_2[\beta]$
    $t_4[R - \beta] = t_1[R - \beta]$
*   **Simplified Definition:** Let $Y, Z, W$ be nonempty subsets of attributes in R. $Y \rightarrow \rightarrow Z$ (Y multidetermines Z) if and only if for all possible relations r(R), if $<y_1, z_1, w_1> \in r$ and $<y_2, z_2, w_2> \in r$, then $<y_1, z_1, w_2> \in r$ and $<y_2, z_2, w_1> \in r$

*   **Example:** `classes(course, teacher, book)`
    *   `course →→ teacher`
    *   `course →→ book`
*   **Use of MVDs:**
    1. To test relations to determine whether they are legal under a given set of functional and multivalued dependencies.
    2. To specify constraints on the set of legal relations.

### Fourth Normal Form (4NF)

*   A relation schema R is in 4NF with respect to a set D of functional and multivalued dependencies if for all multivalued dependencies in $D^+$ of the form $\alpha \rightarrow \rightarrow \beta$, where $\alpha \subseteq R$ and $\beta \subseteq R$, at least one of the following hold:
    *   $\alpha \rightarrow \rightarrow \beta$ is trivial (i.e., $\beta \subseteq \alpha$ or $\alpha \cup \beta = R$)
    *   $\alpha$ is a superkey for schema R
*   If a relation is in 4NF, it is in BCNF.
