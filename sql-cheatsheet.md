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




