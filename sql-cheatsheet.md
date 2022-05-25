
# Preface

For most of the examples below, the Northwind dataset from [github.com/Microsoft](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/northwind-pubs) is used.

# 1. Basics

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

# 2. Filtering using the WHERE clause

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

# 3. CASE WHEN Statements

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

# 4. Joining tables

### Basic structure of a (left) join

```sql
SELECT 
  x.column1,
  x.column2,
  y.column1,
  y.column2
FROM schema.left_table AS x
  LEFT JOIN schema.right_table AS y
    ON x.column1 = y.column1
```

Other types that can be used are INNER JOIN and RIGHT JOIN. 


# 5. Aggregation

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
SELECT
  column1,
  column2
  COUNT(*) AS counted_column
FROM schema.table
GROUP BY column1, column2
ORDER BY column1, column2
```


### Using COUNT DISTINCT

```sql
SELECT
  column1,
  COUNT(DISTINCT column2) AS counted_column
FROM schema.table
WHERE column1 LIKE 'X%'
GROUP BY column1
ORDER BY column1
```

### Using SUM

```sql
SELECT
  column1,
  column2
  SUM(column3) AS sum_column
FROM schema.table
GROUP BY column1, column2
ORDER BY column1, column2
```

### Using SUM with an inside calculation

```sql
SELECT
  column1,
  column2
  SUM(column3 * column4) AS sum_column
FROM schema.table
GROUP BY column1, column2
ORDER BY column1, column2
```

### Using MIN/MAX

```sql
SELECT
  MIN(column1) AS min_val,
  MAX(column2) AS max_val,
  column3,
  column4
FROM schema.table
GROUP BY column3, column4
```

### Perform filtering after grouping using HAVING

```sql
SELECT
  SUM(column1) AS sum_col,
  column2,
  column3
FROM schema.table
WHERE column4 LIKE 'X'
GROUP BY column2, column3
HAVING sum_col > 2
ORDER BY column2
```





