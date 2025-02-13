Okay, here are the first 20 questions based on the provided PDF document, formatted as requested:

#flashcards/Relational_Databases
QUESTION: What are the fundamental characteristics of a relation in the context of relational databases?
OPTIONS:
A) Named, two-dimensional table; Unique relation name; Named columns (attributes); Atomic attribute values.
B) Unnamed, multi-dimensional table; Unique rows; Unnamed columns; Complex attribute values.
C) Named, one-dimensional table; Duplicate relation name; Unnamed columns; Atomic attribute values.
D) Named, two-dimensional table; Unique relation name; Unnamed columns; Non-atomic attribute values.
??
SOLUTION:
A) A relation is a named, two-dimensional table with a unique name, named columns (attributes), and atomic attribute values. The order of rows and columns is irrelevant.

#flashcards/Relational_Keys
QUESTION:  In the relation `EMPLOYEE1(Emp_ID, Name, Dept, Salary)`, which attribute is most likely the primary key?
OPTIONS:
A) Name
B) Dept
C) Salary
D) Emp_ID
??
SOLUTION:
D) `Emp_ID` is underlined in the example, indicating it's the primary key, designed to uniquely identify each row (employee).

#flashcards/Composite_Foreign_Keys
QUESTION:  A primary key consisting of more than one attribute is called a:
OPTIONS:
A) Foreign Key
B) Composite Key
C) Secondary Key
D) Super Key
??
SOLUTION:
B) A composite key is, by definition, a primary key made up of multiple attributes.

#flashcards/Composite_Foreign_Keys
QUESTION: Which of the following statements best describes a foreign key?
OPTIONS:
A) An attribute that uniquely identifies a row in a relation.
B) An attribute in a relation that serves as the primary key of another relation in the same database.
C) A primary key that consists of more than one attribute.
D) A key that is used for encryption.
??
SOLUTION:
B) A foreign key links two tables together by referencing the primary key of another table.

#flashcards/Integrity_Constraints
QUESTION: What are the four components typically included in a domain definition?
OPTIONS:
A) Domain name, Meaning, Data type, Size
B) Primary key, Foreign key, Data type, Size
C) Relation name, Attribute name, Data type, Size
D) Domain name, Meaning, Data type, Size, Allowable values/range
??
SOLUTION:
D) Domain definition usually consists of 4 components: domain name, meaning, data type, size (or length), allowable values/allowable range (if applicable)

#flashcards/Integrity_Constraints
QUESTION: The integrity constraint that ensures every relation has a primary key and that the data values for that primary key are valid is called:
OPTIONS:
A) Domain Integrity
B) Referential Integrity
C) Entity Integrity
D) Key Integrity
??
SOLUTION:
C) Entity Integrity ensures the primary key exists and is valid (and not null).

#flashcards/Integrity_Constraints
QUESTION: The referential integrity constraint is a rule that maintains consistency among rows between how many relations?:
OPTIONS:
A) Only One
B) Two
C) Three
D) Unlimited
??
SOLUTION:
B) Referential integrity specifically concerns the relationship *between* two relations (one with a primary key, one with a foreign key).

#flashcards/Integrity_Constraints
QUESTION:  If deleting a customer would also require deleting all associated orders to maintain referential integrity, which referential integrity action is being described?
OPTIONS:
A) Restrict
B) Cascade
C) Set-to-Null
D) Default
??
SOLUTION:
B) Cascade automatically deletes dependent rows when the corresponding parent row is deleted.

#flashcards/Integrity_Constraints
QUESTION: If setting the foreign key to NULL is permitted when deleting related primary key, this refers to:
OPTIONS:
	A) Restrict
	B) Set-to-Null
	C) Cascade
	D) No Action
??
SOLUTION:
	B) Set-to-Null

#flashcards/Relational_Database_Design
QUESTION:  Which of the following is NOT listed as a design goal for relational databases?
OPTIONS:
A) Avoid redundant data.
B) Ensure relationships among attributes are represented.
C) Facilitate checking of updates for integrity constraint violations.
D) Maximize data redundancy for faster queries.
??
SOLUTION:
D) Relational database design aims to *minimize*, not maximize, redundancy.

#flashcards/Decomposition
QUESTION: The process of breaking down a relation schema into smaller, more manageable relation schemas is referred to as ______.
??
SOLUTION:
Decomposition

#flashcards/Decomposition
QUESTION:  For a decomposition to be lossless-join, if R is the original schema and R1 and R2 are the decomposed schemas, the following must hold true:  $R = \_\_\_\_$.
OPTIONS:
A)  $R_1 - R_2$
B)  $R_1 \cup R_2$
C) $R_1 \cap R_2$
D) $R_1$ x $R_2$
??
SOLUTION:
B) $R_1 \cup R_2$. The union of the decomposed schemas must contain all attributes of the original schema. The join condition will be explained in next card.

#flashcards/Decomposition
QUESTION: Given a relation schema R and its decomposition into R1 and R2, for all possible relations r on schema R the equation is:  $r$ = \_\_\_.
OPTIONS:
A) $\Pi_{R1}(r) \cup \Pi_{R2}(r)$
B) $\Pi_{R1}(r) \cap \Pi_{R2}(r)$
C) $\Pi_{R1}(r) \bowtie \Pi_{R2}(r)$
D) $\Pi_{R1}(r) - \Pi_{R2}(r)$
??
SOLUTION:
C) $\Pi_{R1}(r) \bowtie \Pi_{R2}(r)$. This represents the natural join of the projections of r onto R1 and R2.

#flashcards/Functional_Dependencies
QUESTION:  If $\alpha \rightarrow \beta$ holds, and for two tuples $t_1$ and $t_2$, $t_1[\alpha] = t_2[\alpha]$, then what can be said about $t_1[\beta]$ and $t_2[\beta]$?
OPTIONS:
A)  $t_1[\beta] > t_2[\beta]$
B)  $t_1[\beta] < t_2[\beta]$
C) $t_1[\beta] = t_2[\beta]$
D) No relationship can be determined.
??
SOLUTION:
C) $t_1[\beta] = t_2[\beta]$. This is the definition of a functional dependency.

#flashcards/Functional_Dependencies
QUESTION:  A functional dependency $\alpha \rightarrow \beta$ is considered trivial if:
OPTIONS:
A) $\alpha \subseteq \beta$
B) $\beta \subseteq \alpha$
C) $\alpha \cap \beta = \emptyset$
D) $\alpha \cup \beta = R$
??
SOLUTION:
B) $\beta \subseteq \alpha$. A trivial functional dependency is one that is always satisfied.

#flashcards/Functional_Dependencies
QUESTION: Given the functional dependencies A -> B and B -> C, which of the following can be inferred using Armstrong's Axiom of Transitivity?
OPTIONS:
A) B -> A
B) C -> B
C) A -> C
D) C -> A
??
SOLUTION:
 C) A -> C

#flashcards/Armstrongs_Axioms
QUESTION: Name the three Armstrong's Axioms.
??
SOLUTION:
Reflexivity, Augmentation, Transitivity

#flashcards/Attribute_Closure
QUESTION: Computing the ______ of an attribute set involves finding all attributes that are functionally determined by that set.
??
SOLUTION:
Closure

#flashcards/Multivalued_Dependencies
QUESTION: In the relation `classes(course, teacher, book)`, if knowing the `course` implies a set of possible `teacher` values and a *separate* set of possible `book` values, independent of each other, this suggests the presence of a _____.
??
SOLUTION:
Multivalued dependency

#flashcards/Normal_Forms
QUESTION: A relation schema R is in 4NF if, for all multivalued dependencies in D+ of the form $\alpha \twoheadrightarrow \beta$, where $\alpha \subseteq R$ and $\beta \subseteq R$, at least one of the following holds true: $\alpha \twoheadrightarrow \beta$ is trivial, or $\alpha$ is a _____ for schema R.
??
SOLUTION:
Superkey
