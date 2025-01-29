
**Assignment 5: Decomposing Complex SQL Schema to 2NF**

**Scenario:**

```sql
CREATE TABLE Employee (
    EmpID INT PRIMARY KEY,
    EmpName VARCHAR(50),
    EmpRole VARCHAR(50)
);

CREATE TABLE Department (
    DeptID INT PRIMARY KEY,
    DeptName VARCHAR(50)
);

CREATE TABLE Assignment (
    EmpID INT,
    DeptID INT,
    AssignmentDate DATE,
    PRIMARY KEY (EmpID, DeptID),
    FOREIGN KEY (EmpID) REFERENCES Employee(EmpID),
    FOREIGN KEY (DeptID) REFERENCES Department(DeptID)
);
```

**1. Identify Partial Dependencies:**

*   There are **no partial dependencies** in this schema.
*   In the `Assignment` table, `AssignmentDate` is dependent on the entire primary key (`EmpID`, `DeptID`). It represents the date when a specific employee was assigned to a specific department.

**2. Decomposition (Not Required):**

*   Since there are no partial dependencies, no decomposition is required. The schema is already in 2NF.

**3. SQL Code to Create New Tables (Not Required):**

*   No new tables are required.

**4. SQL INSERT Statements:**

```sql
INSERT INTO Employee (EmpID, EmpName, EmpRole) VALUES
(1, 'Alice', 'Manager'),
(2, 'Bob', 'Developer');

INSERT INTO Department (DeptID, DeptName) VALUES
(101, 'Sales'),
(102, 'Engineering');

INSERT INTO Assignment (EmpID, DeptID, AssignmentDate) VALUES
(1, 101, '2023-10-26'),
(2, 102, '2023-10-27');
```

**5. SQL SELECT Queries:**

```sql
-- Get employee assignments with department names
SELECT E.EmpName, D.DeptName, A.AssignmentDate
FROM Employee E
JOIN Assignment A ON E.EmpID = A.EmpID
JOIN Department D ON A.DeptID = D.DeptID;

-- Get all employees assigned to a specific department
SELECT E.EmpName
FROM Employee E
JOIN Assignment A ON E.EmpID = A.EmpID
JOIN Department D ON A.DeptID = D.DeptID
WHERE D.DeptName = 'Engineering';
```
![[Pasted image 20250116112243.png]]
