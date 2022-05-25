
# Preface

For most of the examples below, the Northwind dataset from [github.com/Microsoft](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs) is used.

# Table of Contents

* [1. Basics](#basics)
* [2. Filtering using the WHERE clause](#2-filtering-using-the-where-clause)

# [1. Basics](#basics)

### Standard Select Query

```sql
SELECT (columns)
FROM (schema.table)
WHERE (filter)
GROUP BY (columns)
HAVING (filter after grouping)
ORDER BY (columns)
```

### Limiting number of results

```sql
SELECT TOP 10 *
FROM Northwind.dbo.Customers
```

### Basic calculations with rounding

```sql
SELECT TOP 10
	CustomerID,
	OrderID,
	ROUND(Freight, 2) AS Freight
FROM Northwind.dbo.Orders
```

### CONCAT

```sql
SELECT TOP 10
	ContactName,
	ContactTitle,
	Address,
	CONCAT(PostalCode, ' ', City) AS City
FROM Northwind.dbo.Customers
```

# [2. Filtering using the WHERE clause](#2-filtering-using-the-where-clause)

### Filtering by multiple conditions

```sql
SELECT TOP 100
	ContactName,
	ContactTitle,
	Address,
	City,
	PostalCode
FROM Northwind.dbo.Customers
WHERE City = 'London' AND ContactTitle = 'Sales Representative'
```
### Finding missing data

```sql
SELECT TOP 10 *
FROM Northwind.dbo.Orders
WHERE ShipRegion IS NULL
```

### Filtering based on results from a subquery

```sql
SELECT TOP 10
	ProductID,
	ProductName,
	CategoryID,
	QuantityPerUnit,
	UnitPrice
FROM [Northwind].[dbo].[Products]
WHERE CategoryID IN
  (
  SELECT 
	  CategoryID
  FROM Northwind.dbo.Categories
  WHERE CategoryName = 'Beverages'
  )
```

# [3. CASE WHEN Statements](#3-case-when-statements)

### Structure of a CASE WHEN statement

```sql
SELECT TOP 10
	LastName,
	FirstName,
	HireDate,
	CASE
		WHEN HireDate < '1993-01-01'
			THEN 'Long-term Employee'
		ELSE 'No long-term Employee'
	END AS EmployeeType
FROM Northwind.dbo.Employees
```

### Multiple WHEN conditions

```sql
SELECT TOP 10
	CompanyName
	City,
	Country,
	CASE 
		WHEN Country IN ('USA', 'UK')
			THEN 'Region A'
		WHEN Country IN ('Germany', 'Austria', 'Switzerland')
			THEN 'Region B'
		ELSE 'Other Region'
	END AS CustomRegion
FROM Northwind.dbo.Customers
```

# [4. Joining tables](#4-joining-tables)

### Basic structure of a (left) join

```sql
SELECT TOP 100 
	o.OrderID,
	o.CustomerID,
	o.OrderDate,
	c.CompanyName,
	c.Country
FROM Northwind.dbo.Orders AS o
	LEFT JOIN Northwind.dbo.Customers AS c
		ON o.CustomerID = c.CustomerID
```

Other types that can be used are INNER JOIN and RIGHT JOIN. 

# [5. Aggregation](#5-aggregation)

### Basic structure

```sql
SELECT (columns)
FROM (schema.table)
WHERE (filter)
GROUP BY (columns)
ORDER BY (columns)
```

### Using COUNT

```sql
SELECT COUNT(*)
FROM Northwind.dbo.Customers
WHERE Country = 'Austria'
```


### Using COUNT DISTINCT

```sql
SELECT COUNT(DISTINCT(Country))
FROM Northwind.dbo.Suppliers
```

### Using SUM (with an inside calculation)

```sql
SELECT TOP 10
	o.CustomerID,
	SUM(d.UnitPrice * d.Quantity) AS total
FROM Northwind.dbo.Orders AS o
	LEFT JOIN Northwind.dbo."Order Details" AS d
	ON o.OrderID = d.OrderID
GROUP BY o.CustomerID
ORDER BY total DESC
```

### Using MIN/MAX

```sql
SELECT 
	c.CategoryName,
	MAX(p.UnitPrice) AS MaxUnitPrice
FROM Northwind.dbo.Products AS p
	LEFT JOIN Northwind.dbo.Categories AS c
		ON c.CategoryID = p.CategoryID
GROUP BY c.CategoryName
```

### Perform filtering after grouping using HAVING

```sql
SELECT 
	c.CategoryID,
	c.CategoryName,
	MAX(p.UnitPrice) AS MaxUnitPrice
FROM Northwind.dbo.Products AS p
	LEFT JOIN Northwind.dbo.Categories AS c
		ON c.CategoryID = p.CategoryID
GROUP BY c.CategoryID, c.CategoryName 
HAVING MAX(p.UnitPrice) > 100
```

[6. Window Functions](#6-window-functions)

