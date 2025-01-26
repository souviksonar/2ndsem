### Index Evaluation Metrics

> [!PDF|yellow] [[Database System Concepts 7.pdf#page=653&selection=39,0,65,42&color=yellow|Database System Concepts 7, p.624]]
> > - **Access types:** The types of access that are supported efficiently. Access types can include finding records with a specified attribute value and finding records whose attribute values fall in a specified range.
> > - **Access time:** The time it takes to find a particular data item, or set of items, using the technique in question.
> > - **Insertion time:** The time it takes to insert a new data item. This value includes the time it takes to find the correct place to insert the new data item, as well as the time it takes to update the index structure.
> > - **Deletion time:** The time it takes to delete a data item. This value includes the time it takes to find the item to be deleted, as well as the time it takes to update the index structure.
> > - **Space overhead:** The additional space occupied by an index structure. Provided that the amount of additional space is moderate, it is usually worthwhile to sacrifice the space to achieve improved performance.

****
### Why we need Multi-level indexing
![[CSC502-ADBMS/media/media/2.1 Indexing.webp]]
[[2.1 Indexing.pdf#page=11&rect=60,241,676,470&color=yellow|2.1 Indexing, p.11]]

---
### B Tree

![[CSC502-ADBMS/media/media/5 Database Management System - File Organization & Indexing.webp]]
[[5 Database Management System - File Organization & Indexing.pdf#page=14&rect=119,104,515,494|5 Database Management System - File Organization & Indexing, p.14]]
![[CSC502-ADBMS/media/media/5 Database Management System - File Organization & Indexing 1.webp]]
[[5 Database Management System - File Organization & Indexing.pdf#page=15&rect=70,104,475,680|5 Database Management System - File Organization & Indexing, p.15]]


---
### B+ Tree

![[CSC502-ADBMS/media/media/5 Database Management System - File Organization & Indexing 2.webp]]

[[5 Database Management System - File Organization & Indexing.pdf#page=27&rect=76,154,491,681|5 Database Management System - File Organization & Indexing, p.27]]

