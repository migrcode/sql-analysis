
# Preface

For most of the examples below, the Airbnb dataset from [insideairbnb.com](http://insideairbnb.com/get-the-data) is used.

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
SELECT TOP 10 
	movieId,
	title,
	genres
FROM master.dbo.movies
```

### Basic calculations with rounding

```sql
SELECT TOP 10
	userId,
	movieId,
	ROUND(rating, 0) AS rating,
	timestamp
FROM master.dbo.ratings
```

### CONCAT

```sql
SELECT TOP 10
	movieId,
	CONCAT('Title: ', title, ' Genres: ', genres)
FROM master.dbo.movies
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

# 3. CASE WHEN Statements

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





