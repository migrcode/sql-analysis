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
SELECT * 
FROM schema.table
LIMIT 10
```

```sql
SELECT TOP 10 * 
FROM schema.table
```

### Basic calculations with rounding

```sql
SELECT 
column1,
column2,
ROUND(column1 * column2, 2) AS column3
FROM schema.table
```

### CONCAT

```sql
SELECT 
column1,
CONCAT(column2,  " ", column3)
FROM schema.table
```

# 2. Filtering using the WHERE clause

### Filtering by multiple conditions

```sql
SELECT 
column1,
column2
FROM schema.table
WHERE column1 LIKE 'May%'
AND column2 <= 5
AND column3 = '2022'
AND column4 BETWEEN '2022-01-01' AND '2022-02-01'
AND column5 IN ('High', 'Medium', 'Low')
```
### Finding missing data

```sql
SELECT 
column1,
FROM schema.table
WHERE column2 IS NULL
```

### Filtering based on results from a subquery

```sql
SELECT 
column1,
column2
FROM schema.table
WHERE 
column3 IN
(SELECT column_x
FROM schema.table2
WHERE column_y LIKE 'May%'
)
```

3. CASE WHEN Statements

### Structure of a CASE WHEN statement

```sql
SELECT 
  column1,
  column2,
  CASE
    WHEN column3 IN ('Saturday', 'Sunday')
      THEN 'Weekend'
    ELSE 'No Weekend'
  END AS is_weekend
FROM schema.table
WHERE column2 = 3
```

### Multiple WHEN conditions

```sql
SELECT 
  column1,
  column2,
  CASE
    WHEN column3 IN ('Saturday')
      THEN 'Weekend'
    WHEN column3 IN ('Sunday')
      THEN 'Weekend'
    ELSE 'No Weekend'
  END AS is_weekend
FROM schema.table
WHERE column2 = 3
```

