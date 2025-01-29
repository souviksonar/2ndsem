
**Assignment 2: Converting a Multi-Table 3NF Schema to 2NF Using SQL**

**Scenario:**

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    OrderDate DATE
);

CREATE TABLE Products (
    ProductID INT PRIMARY KEY,
    ProductName VARCHAR(50),
    Price DECIMAL(10, 2)
);

CREATE TABLE OrderDetails (
    OrderID INT,
    ProductID INT,
    Quantity INT,
    PRIMARY KEY (OrderID, ProductID),
    FOREIGN KEY (OrderID) REFERENCES Orders(OrderID),
    FOREIGN KEY (ProductID) REFERENCES Products(ProductID)
);
```


**1. Functional Dependencies and Explanation of 3NF:**

*   **Functional Dependencies:**
    *   `OrderID` -> `CustomerID`, `OrderDate`
    *   `ProductID` -> `ProductName`, `Price`
    *   `OrderID`, `ProductID` -> `Quantity`
*   **3NF:** This schema is in 3NF because:
    *   Each table is in 1NF (all values are atomic).
    *   Each table is in 2NF (no partial dependencies).
    *   There are no transitive dependencies.

**2. Partial Dependencies in `OrderDetails`:**

*   There are **no** partial dependencies in the `OrderDetails` table. The `Quantity` is fully dependent on the entire primary key (`OrderID`, `ProductID`).

**3. Conversion to 2NF:**

*   Since there are no partial dependencies, the `OrderDetails` table is already in 2NF. No changes are needed.

**4. SQL Commands to Modify Schema (Not Needed):**

*   No modifications are required as the schema is already 2NF compliant.

**5. Sample SQL INSERT Statements:**

```sql
INSERT INTO Orders (OrderID, CustomerID, OrderDate) VALUES
(1, 101, '2023-10-26'),
(2, 102, '2023-10-27');

INSERT INTO Products (ProductID, ProductName, Price) VALUES
(201, 'Laptop', 1200.00),
(202, 'Mouse', 25.00),
(203, 'Keyboard', 75.00);

INSERT INTO OrderDetails (OrderID, ProductID, Quantity) VALUES
(1, 201, 1),
(1, 202, 2),
(2, 203, 1);
```


**6. SQL SELECT Queries:**

```sql
-- Retrieve order details with product names
SELECT O.OrderID, P.ProductName, OD.Quantity
FROM Orders O
JOIN OrderDetails OD ON O.OrderID = OD.OrderID
JOIN Products P ON OD.ProductID = P.ProductID;

-- Retrieve total price for each order
SELECT O.OrderID, SUM(P.Price * OD.Quantity) AS TotalPrice
FROM Orders O
JOIN OrderDetails OD ON O.OrderID = OD.OrderID
JOIN Products P ON OD.ProductID = P.ProductID
GROUP BY O.OrderID;
```
![[Pasted image 20250116111151.png]]