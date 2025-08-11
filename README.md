# task-4-.Use-INNER-LEFT-RIGHT-FULL-JOIN

---

# **Combination Joins in SQL 

## 🛠 Step 1 – Create the Database

We first create a new database to store our tables.

```sql
CREATE DATABASE combine_data;
USE combine_data;
```

This ensures all the tables and data we create are kept in one place.

---

## 🛠 Step 2 – Create the `Customers` Table

The **Customers** table stores customer details like ID, name, and country.

```sql
CREATE TABLE Customers (
    CustomerID INT PRIMARY KEY,
    CustomerName VARCHAR(50),
    Country VARCHAR(50)
);
```

We then insert some sample data, including customers from different countries:

```sql
INSERT INTO Customers (CustomerID, CustomerName, Country) VALUES
(1, 'John Smith', 'USA'),
(2, 'Priya Sharma', 'India'),
(3, 'Ahmed Khan', 'UAE'),
...
(10, 'Sai', 'USA');
```

---

## 🛠 Step 3 – Create the `Orders` Table

The **Orders** table stores order details, including which customer placed the order.

```sql
CREATE TABLE Orders (
    OrderID INT PRIMARY KEY,
    CustomerID INT,
    Product VARCHAR(50),
    Amount DECIMAL(10,2)
);
```

Sample order data is inserted, including some orders with customers who are not in the Customers table.

```sql
INSERT INTO Orders (OrderID, CustomerID, Product, Amount) VALUES
(101, 1, 'Laptop', 800),
(102, 3, 'Phone', 500),
...
(109, 6, 'Earbuds', 700);
```

This setup allows us to test joins where:

* Some customers **have no orders**.
* Some orders **don’t have a matching customer**.

---

## 🔍 Step 4 – Running Join Queries

### **1. INNER JOIN**

Returns only matching records between Customers and Orders.

```sql
SELECT Customers.CustomerID, CustomerName, Product, Amount
FROM Customers
INNER JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Use case:** Find customers who have placed at least one order.

---

### **2. LEFT JOIN**

Returns all customers, even those without orders. Missing order details appear as `NULL`.

```sql
SELECT Customers.CustomerID, CustomerName, Product, Amount
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Use case:** View a complete customer list with their orders (if any).

---

### **3. RIGHT JOIN**

Returns all orders, even if the customer does not exist in the Customers table.

```sql
SELECT Customers.CustomerID, CustomerName, Product, Amount
FROM Customers
RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Use case:** Identify orders that may not have proper customer records.

---

### **4. FULL OUTER JOIN (MySQL Alternative)**

MySQL does not support FULL OUTER JOIN directly, so we combine `LEFT JOIN` and `RIGHT JOIN` with `UNION`.

```sql
SELECT Customers.CustomerID, CustomerName, Product, Amount
FROM Customers
LEFT JOIN Orders ON Customers.CustomerID = Orders.CustomerID
UNION
SELECT Customers.CustomerID, CustomerName, Product, Amount
FROM Customers
RIGHT JOIN Orders ON Customers.CustomerID = Orders.CustomerID;
```

**Use case:** Get a complete picture of all customers and all orders.

---

## 🎯 Key Learnings

* **INNER JOIN** → Matching rows only.
* **LEFT JOIN** → All from left table, matched where possible.
* **RIGHT JOIN** → All from right table, matched where possible.
* **FULL JOIN** → All rows from both tables, matched where possible.

<img width="701" height="726" alt="Image" src="https://github.com/user-attachments/assets/5d65ce74-cbad-462a-885e-ceb188521141" />
<img width="593" height="516" alt="Image" src="https://github.com/user-attachments/assets/51725920-4a75-4252-ac6f-d996e67c9f8e" />
<img width="827" height="542" alt="Image" src="https://github.com/user-attachments/assets/fad91f61-163f-436b-af5a-cb7a34b66fdf" />
<img width="745" height="565" alt="Image" src="https://github.com/user-attachments/assets/04f8c22d-2398-4624-b044-fd3ced7df2b6" />


---
