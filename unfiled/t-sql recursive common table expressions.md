for loop (demonstration purposes only):
```sql
WITH i(i) AS (SELECT 1 UNION ALL SELECT i + 1 from i WHERE i < 13)
SELECT i FROM i ORDER BY i
```
