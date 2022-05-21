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
