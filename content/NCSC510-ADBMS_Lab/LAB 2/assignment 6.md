

**Assignment 6: Advanced SQL Normalization: Identifying and Correcting Partial Dependencies**

**Scenario:**

```sql
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    SaleDate DATE,
    SalePrice DECIMAL(10, 2),
    CustomerName VARCHAR(50),
    CustomerEmail VARCHAR(50),
    PRIMARY KEY (SaleID)
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(50),
    Category VARCHAR(50)
);
```

**1. Functional Dependencies:**

*   `SaleID` -> `ProductID`, `SaleDate`, `SalePrice`, `CustomerName`, `CustomerEmail`
*   `ProductID` -> `ProductName`, `Category`
*   `CustomerEmail` -> `CustomerName` (Assuming a customer has a unique email)

**2. Partial Dependencies and 2NF Violation:**

*   **Partial Dependency:** `ProductID` -> `ProductName`, `Category`

    *   `ProductName` and `Category` are dependent on `ProductID`, which is not a candidate key in the `Sales` table. This violates 2NF because a non-prime attribute depends on a part of a potential superkey but not the primary key of the `Sales` table.
*   **Another Potential Partial Dependency:** `CustomerEmail` -> `CustomerName`
    *   If we assume that `CustomerEmail` uniquely identifies a customer, then `CustomerName` is partially dependent on `CustomerEmail` which is a potential candidate key but not the primary key of the `Sales` table.

**3. SQL Code to Decompose the `Sales` Table:**

```sql
-- Create Customers table (if we consider customer details to be a partial dependency)
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerName VARCHAR(50),
    CustomerEmail VARCHAR(50) UNIQUE
);
-- Create Sales table
CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    CustomerID INT,
    SaleDate DATE,
    SalePrice DECIMAL(10, 2),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**4. Updated SQL Schema and INSERT/SELECT Examples:**

**Updated SQL Schema:**

(The `Products` table remains the same)

```sql
CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(50),
    Category VARCHAR(50)
);

CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY AUTO_INCREMENT,
    CustomerName VARCHAR(50),
    CustomerEmail VARCHAR(50) UNIQUE
);

CREATE TABLE Sales (
    SaleID INT PRIMARY KEY,
    ProductID INT,
    CustomerID INT,
    SaleDate DATE,
    SalePrice DECIMAL(10, 2),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID),
    FOREIGN KEY (CustomerID) REFERENCES Customers(CustomerID)
);
```

**INSERT Statements:**

```sql
INSERT INTO Products (ProductID, ProductName, Category) VALUES
(1, 'Laptop', 'Electronics'),
(2, 'T-Shirt', 'Apparel');

INSERT INTO Customers (CustomerName, CustomerEmail) VALUES
('John Doe', 'john.doe@example.com'),
('Jane Smith', 'jane.smith@example.com');

INSERT INTO Sales (SaleID, ProductID, CustomerID, SaleDate, SalePrice) VALUES
(101, 1, 1, '2023-10-26', 1200.00),
(102, 2, 2, '2023-10-27', 25.00);
```

**SELECT Statements:**

```sql
-- Get sales details with product and customer information
SELECT S.SaleID, P.ProductName, C.CustomerName, S.SaleDate, S.SalePrice
FROM Sales S
JOIN Products P ON S.ProductID = P.ProductID
JOIN Customers C ON S.CustomerID = C.CustomerID;

-- Get all sales for a specific product
SELECT S.SaleID, S.SaleDate, S.SalePrice
FROM Sales S
JOIN Products P ON S.ProductID = P.ProductID
WHERE P.ProductName = 'Laptop';
```
![[Pasted image 20250116112639.png]]