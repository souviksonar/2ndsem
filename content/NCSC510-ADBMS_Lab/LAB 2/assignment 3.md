
**Assignment 3: SQL Query-Based Approach to Detect and Remove Partial Dependencies**

**Scenario:**

```sql
CREATE TABLE Student_Courses (
    StudentID INT,
    CourseID INT,
    InstructorName VARCHAR(50),
    InstructorEmail VARCHAR(50),
    StudentName VARCHAR(50),
    PRIMARY KEY (StudentID, CourseID)
);
```

**1. SQL Query to Detect Partial Dependencies and Explanation:**

*   **Concept of Partial Dependency:** A partial dependency exists when a non-prime attribute (an attribute that is not part of the primary key) is functionally dependent on only a part of the composite primary key.
*   **Partial Dependencies in the Table:**
    *   `StudentName` depends only on `StudentID`.
    *   `InstructorName` and `InstructorEmail` depend only on `CourseID`.

**SQL Query to Illustrate Partial Dependency on `StudentName`:**

```sql
SELECT StudentID, StudentName
FROM Student_Courses
GROUP BY StudentID, StudentName
HAVING COUNT(DISTINCT CourseID) > 1;
```

*   This query groups by `StudentID` and `StudentName`. If a student (identified by `StudentID`) has the same `StudentName` but is enrolled in multiple courses (indicated by `COUNT(DISTINCT CourseID) > 1`), it demonstrates that `StudentName` is only dependent on `StudentID` and not the entire primary key.

**SQL Query to Illustrate Partial Dependency on `InstructorName` and `InstructorEmail`:**

```sql
SELECT CourseID, InstructorName, InstructorEmail
FROM Student_Courses
GROUP BY CourseID, InstructorName, InstructorEmail
HAVING COUNT(DISTINCT StudentID) > 1;
```

*   Similar to the previous query, this one groups by `CourseID`, `InstructorName`, and `InstructorEmail`. If a course has the same instructor details but multiple students enrolled, it demonstrates that `InstructorName` and `InstructorEmail` are dependent on `CourseID` only.

**2. Decomposition into Two or More Tables:**

To remove partial dependencies, we decompose the table into three tables:

*   `Students` (StudentID, StudentName)
*   `Courses` (CourseID, InstructorName, InstructorEmail)
*   `StudentCourses` (StudentID, CourseID) - a junction table to link students and courses.

**3. SQL Commands to Create New Tables and Insert Data:**

```sql
-- Create Students table
CREATE TABLE Students (
    StudentID INT PRIMARY KEY,
    StudentName VARCHAR(50)
);

-- Create Courses table
CREATE TABLE Courses (
    CourseID INT PRIMARY KEY,
    InstructorName VARCHAR(50),
    InstructorEmail VARCHAR(50)
);

-- Create StudentCourses table
CREATE TABLE StudentCourses (
    StudentID INT,
    CourseID INT,
    PRIMARY KEY (StudentID, CourseID),
    FOREIGN KEY (StudentID) REFERENCES Students(StudentID),
    FOREIGN KEY (CourseID) REFERENCES Courses(CourseID)
);

-- Insert data (example)
INSERT INTO Students (StudentID, StudentName) VALUES
(1, 'Alice'),
(2, 'Bob');

INSERT INTO Courses (CourseID, InstructorName, InstructorEmail) VALUES
(101, 'Dr. Smith', 'smith@example.com'),
(102, 'Prof. Johnson', 'johnson@example.com');

INSERT INTO StudentCourses (StudentID, CourseID) VALUES
(1, 101),
(1, 102),
(2, 101);
```

**4. Demonstrate How the New Structure Eliminates Partial Dependencies:**

*   In the new structure, `StudentName` is directly and fully dependent on `StudentID` in the `Students` table.
*   `InstructorName` and `InstructorEmail` are directly and fully dependent on `CourseID` in the `Courses` table.
*   The `StudentCourses` table only contains the composite primary key (`StudentID`, `CourseID`), and there are no non-prime attributes, thus no partial dependencies.

**Queries to Retrieve Data:**

```sql
-- Get student names and the courses they are enrolled in
SELECT S.StudentName, C.CourseID
FROM Students S
JOIN StudentCourses SC ON S.StudentID = SC.StudentID
JOIN Courses C ON SC.CourseID = C.CourseID;

-- Get instructor details for a specific course
SELECT InstructorName, InstructorEmail
FROM Courses
WHERE CourseID = 101;
```
![[Pasted image 20250116111944.png]]
