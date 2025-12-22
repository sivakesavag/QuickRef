# SQL Comprehensive Cheatsheet

> Quick reference covering all essential SQL concepts from basics to advanced topics.  
> **SQL Dialect**: PostgreSQL-focused with MySQL/SQL Server variants noted.

---

## Table of Contents

1. [SELECT Basics](#1-select-basics)
2. [Filtering & Sorting](#2-filtering--sorting)
3. [Aggregations](#3-aggregations)
4. [Joins](#4-joins)
5. [Subqueries & CTEs](#5-subqueries--ctes)
6. [Set Operations](#6-set-operations)
7. [Window Functions](#7-window-functions)
8. [Date/Time Functions](#8-datetime-functions)
9. [String Functions](#9-string-functions)
10. [NULL Handling](#10-null-handling)
11. [DDL Operations](#11-ddl-operations)
12. [DML Operations](#12-dml-operations)
13. [Constraints & Keys](#13-constraints--keys)
14. [Indexes](#14-indexes)
15. [Transactions](#15-transactions)
16. [Query Optimization](#16-query-optimization)
17. [JSON & Arrays](#17-json--arrays)
18. [Common Patterns](#18-common-patterns)

---

## 1. SELECT Basics

```sql
-- All columns
SELECT * FROM table_name;

-- Specific columns
SELECT col1, col2 FROM table_name;

-- Aliasing
SELECT col1 AS alias_name, col2 "Column Name" FROM t;

-- Distinct values
SELECT DISTINCT col FROM table_name;

-- Expressions
SELECT col1, col2, col1 * col2 AS computed FROM t;

-- LIMIT / OFFSET (pagination)
SELECT * FROM t LIMIT 10 OFFSET 20;
-- SQL Server: OFFSET 20 ROWS FETCH NEXT 10 ROWS ONLY
```

---

## 2. Filtering & Sorting

### WHERE Clause

```sql
-- Comparison operators
WHERE col = value
WHERE col != value          -- or <>
WHERE col > value
WHERE col >= value
WHERE col < value
WHERE col <= value

-- Logical operators
WHERE cond1 AND cond2
WHERE cond1 OR cond2
WHERE NOT condition

-- Range
WHERE col BETWEEN 10 AND 100    -- inclusive

-- List
WHERE col IN ('a', 'b', 'c')
WHERE col NOT IN (1, 2, 3)

-- Pattern matching
WHERE col LIKE 'prefix%'        -- starts with
WHERE col LIKE '%suffix'        -- ends with
WHERE col LIKE '%contains%'     -- contains
WHERE col LIKE 'a_b'            -- _ = single char

-- NULL check
WHERE col IS NULL
WHERE col IS NOT NULL
```

### ORDER BY

```sql
ORDER BY col ASC              -- ascending (default)
ORDER BY col DESC             -- descending
ORDER BY col1 ASC, col2 DESC  -- multi-column
ORDER BY 1, 2                 -- by position (not recommended)
ORDER BY col NULLS FIRST      -- PostgreSQL: NULL ordering
ORDER BY col NULLS LAST
```

---

## 3. Aggregations

### Aggregate Functions

| Function | Description |
|----------|-------------|
| `COUNT(*)` | Count all rows |
| `COUNT(col)` | Count non-NULL values |
| `COUNT(DISTINCT col)` | Count unique values |
| `SUM(col)` | Total of values |
| `AVG(col)` | Average (ignores NULLs) |
| `MIN(col)` | Minimum value |
| `MAX(col)` | Maximum value |
| `STRING_AGG(col, ',')` | Concatenate strings (PostgreSQL) |
| `GROUP_CONCAT(col)` | Concatenate strings (MySQL) |

### GROUP BY & HAVING

```sql
SELECT category, COUNT(*), AVG(price)
FROM products
WHERE is_active = true          -- filters BEFORE grouping
GROUP BY category
HAVING COUNT(*) > 5             -- filters AFTER grouping
ORDER BY COUNT(*) DESC;
```

**Rule**: Non-aggregated columns in SELECT must be in GROUP BY.

---

## 4. Joins

### Join Types

```sql
-- INNER JOIN: matching rows only
SELECT * FROM a INNER JOIN b ON a.id = b.a_id;

-- LEFT JOIN: all from left + matching from right
SELECT * FROM a LEFT JOIN b ON a.id = b.a_id;

-- RIGHT JOIN: all from right + matching from left
SELECT * FROM a RIGHT JOIN b ON a.id = b.a_id;

-- FULL OUTER JOIN: all from both sides
SELECT * FROM a FULL OUTER JOIN b ON a.id = b.a_id;

-- CROSS JOIN: cartesian product
SELECT * FROM a CROSS JOIN b;

-- Self JOIN
SELECT e.name, m.name AS manager
FROM employees e LEFT JOIN employees m ON e.manager_id = m.id;
```

### Special Join Patterns

```sql
-- Anti-join (rows without match)
SELECT * FROM a LEFT JOIN b ON a.id = b.a_id WHERE b.a_id IS NULL;
-- Or: WHERE NOT EXISTS (SELECT 1 FROM b WHERE b.a_id = a.id)

-- Semi-join (exists check)
SELECT * FROM a WHERE EXISTS (SELECT 1 FROM b WHERE b.a_id = a.id);
```

### Join Diagram

```
INNER:     [A ∩ B]
LEFT:      [A] + [A ∩ B]
RIGHT:     [A ∩ B] + [B]
FULL:      [A] + [A ∩ B] + [B]
CROSS:     [A × B]
```

---

## 5. Subqueries & CTEs

### Subquery Types

```sql
-- Scalar subquery (single value)
SELECT (SELECT MAX(price) FROM products) AS max_price;

-- Column subquery (IN list)
SELECT * FROM orders WHERE customer_id IN (SELECT id FROM customers WHERE tier = 'Gold');

-- Table subquery (derived table)
SELECT * FROM (SELECT id, count FROM ...) AS derived_table;

-- Correlated subquery
SELECT * FROM products p WHERE price > (SELECT AVG(price) FROM products WHERE category_id = p.category_id);
```

### Common Table Expression (CTE)

```sql
WITH cte_name AS (
  SELECT ...
),
another_cte AS (
  SELECT ... FROM cte_name  -- can reference previous CTE
)
SELECT * FROM another_cte;
```

### Recursive CTE

```sql
WITH RECURSIVE hierarchy AS (
  -- Base case
  SELECT id, name, manager_id, 1 AS level
  FROM employees WHERE manager_id IS NULL
  
  UNION ALL
  
  -- Recursive case
  SELECT e.id, e.name, e.manager_id, h.level + 1
  FROM employees e
  JOIN hierarchy h ON e.manager_id = h.id
)
SELECT * FROM hierarchy;
```

---

## 6. Set Operations

```sql
-- UNION: combine and remove duplicates
SELECT col FROM a UNION SELECT col FROM b;

-- UNION ALL: combine keeping duplicates
SELECT col FROM a UNION ALL SELECT col FROM b;

-- INTERSECT: rows in both
SELECT col FROM a INTERSECT SELECT col FROM b;

-- EXCEPT: rows in first but not second
SELECT col FROM a EXCEPT SELECT col FROM b;  -- PostgreSQL
SELECT col FROM a MINUS SELECT col FROM b;   -- Oracle
```

**Rules**:
- Same number of columns
- Compatible data types
- ORDER BY applies to final result

---

## 7. Window Functions

### Syntax

```sql
function_name() OVER (
  [PARTITION BY col1, col2]   -- Optional: groups
  [ORDER BY col3 [ASC|DESC]]  -- Optional: order within partition
  [frame_clause]              -- Optional: window frame
)
```

### Ranking Functions

| Function | Description |
|----------|-------------|
| `ROW_NUMBER()` | Unique sequential number |
| `RANK()` | Rank with gaps for ties |
| `DENSE_RANK()` | Rank without gaps |
| `NTILE(n)` | Divide into n buckets |

```sql
SELECT name, salary,
  ROW_NUMBER() OVER (ORDER BY salary DESC) as row_num,
  RANK() OVER (ORDER BY salary DESC) as rank,
  DENSE_RANK() OVER (ORDER BY salary DESC) as dense_rank
FROM employees;
```

### Value Functions

| Function | Description |
|----------|-------------|
| `LAG(col, n, default)` | Previous row value |
| `LEAD(col, n, default)` | Next row value |
| `FIRST_VALUE(col)` | First value in window |
| `LAST_VALUE(col)` | Last value in window |
| `NTH_VALUE(col, n)` | Nth value in window |

### Aggregate Windows

```sql
-- Running total
SUM(amount) OVER (ORDER BY date ROWS UNBOUNDED PRECEDING)

-- Moving average
AVG(amount) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)

-- Percent of total
amount / SUM(amount) OVER () * 100
```

### Frame Clause

```
ROWS BETWEEN <start> AND <end>
RANGE BETWEEN <start> AND <end>

<start>/<end> options:
  UNBOUNDED PRECEDING
  n PRECEDING
  CURRENT ROW
  n FOLLOWING
  UNBOUNDED FOLLOWING
```

---

## 8. Date/Time Functions

### Current Date/Time

| PostgreSQL | MySQL | SQL Server |
|------------|-------|------------|
| `CURRENT_DATE` | `CURDATE()` | `CAST(GETDATE() AS DATE)` |
| `CURRENT_TIMESTAMP` | `NOW()` | `GETDATE()` |
| `CURRENT_TIME` | `CURTIME()` | `CAST(GETDATE() AS TIME)` |

### Extraction

```sql
-- PostgreSQL
EXTRACT(YEAR FROM date_col)
EXTRACT(MONTH FROM date_col)
EXTRACT(DAY FROM date_col)
EXTRACT(HOUR FROM timestamp_col)

-- MySQL
YEAR(date_col), MONTH(date_col), DAY(date_col)

-- SQL Server
DATEPART(year, date_col)
```

### Arithmetic

```sql
-- PostgreSQL
date_col + INTERVAL '7 days'
date_col - INTERVAL '1 month'
timestamp_col + INTERVAL '2 hours'

-- Date difference (PostgreSQL)
date2 - date1  -- returns integer days

-- MySQL
DATE_ADD(date, INTERVAL 7 DAY)
DATEDIFF(date2, date1)

-- SQL Server
DATEADD(day, 7, date_col)
DATEDIFF(day, date1, date2)
```

### Truncation & Formatting

```sql
-- PostgreSQL
DATE_TRUNC('month', timestamp_col)  -- first of month
TO_CHAR(date_col, 'YYYY-MM-DD')     -- formatting

-- MySQL
DATE_FORMAT(date_col, '%Y-%m-%d')
```

---

## 9. String Functions

| Function | PostgreSQL | MySQL | SQL Server |
|----------|------------|-------|------------|
| Concatenate | `'a' \|\| 'b'` | `CONCAT('a','b')` | `'a' + 'b'` |
| Length | `LENGTH(s)` | `LENGTH(s)` | `LEN(s)` |
| Uppercase | `UPPER(s)` | `UPPER(s)` | `UPPER(s)` |
| Lowercase | `LOWER(s)` | `LOWER(s)` | `LOWER(s)` |
| Trim | `TRIM(s)` | `TRIM(s)` | `TRIM(s)` |
| Left trim | `LTRIM(s)` | `LTRIM(s)` | `LTRIM(s)` |
| Right trim | `RTRIM(s)` | `RTRIM(s)` | `RTRIM(s)` |
| Substring | `SUBSTRING(s,start,len)` | `SUBSTRING(s,start,len)` | `SUBSTRING(s,start,len)` |
| Position | `POSITION('x' IN s)` | `LOCATE('x', s)` | `CHARINDEX('x', s)` |
| Replace | `REPLACE(s,'old','new')` | `REPLACE(s,'old','new')` | `REPLACE(s,'old','new')` |
| Left | `LEFT(s, n)` | `LEFT(s, n)` | `LEFT(s, n)` |
| Right | `RIGHT(s, n)` | `RIGHT(s, n)` | `RIGHT(s, n)` |

### Pattern Matching

```sql
-- LIKE
WHERE col LIKE 'pattern%'  -- % = any chars, _ = single char

-- ILIKE (case insensitive, PostgreSQL)
WHERE col ILIKE 'pattern%'

-- SIMILAR TO (PostgreSQL, SQL standard regex-like)
WHERE col SIMILAR TO 'abc%'

-- Regex (PostgreSQL)
WHERE col ~ '^[A-Z]{3}$'     -- case sensitive match
WHERE col ~* 'pattern'       -- case insensitive match
```

---

## 10. NULL Handling

### Key Rules

- `NULL = NULL` returns NULL (not true)
- Use `IS NULL` / `IS NOT NULL` for NULL checks
- Aggregates ignore NULLs (except COUNT(*))
- NULL in expressions propagates: `5 + NULL = NULL`

### Functions

```sql
COALESCE(val1, val2, val3)    -- first non-NULL
NULLIF(val1, val2)            -- NULL if equal
IFNULL(val, default)          -- MySQL only

-- Example: avoid division by zero
amount / NULLIF(quantity, 0)
```

### NULL-safe Comparison

```sql
-- PostgreSQL
WHERE col IS NOT DISTINCT FROM value   -- treats NULL = NULL as TRUE

-- MySQL  
WHERE col <=> value

-- Standard workaround
WHERE (col = value) OR (col IS NULL AND value IS NULL)
```

---

## 11. DDL Operations

### Tables

```sql
-- Create
CREATE TABLE table_name (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- Create from query
CREATE TABLE new_table AS SELECT * FROM old_table;

-- Alter
ALTER TABLE t ADD COLUMN new_col INT;
ALTER TABLE t DROP COLUMN old_col;
ALTER TABLE t ALTER COLUMN col TYPE VARCHAR(200);
ALTER TABLE t RENAME COLUMN old_name TO new_name;
ALTER TABLE t RENAME TO new_table_name;

-- Drop
DROP TABLE IF EXISTS table_name;
DROP TABLE table_name CASCADE;  -- with dependents
```

### Views

```sql
CREATE VIEW view_name AS SELECT ... ;
CREATE OR REPLACE VIEW view_name AS SELECT ...;
DROP VIEW view_name;

-- Materialized View (PostgreSQL)
CREATE MATERIALIZED VIEW mv_name AS SELECT ...;
REFRESH MATERIALIZED VIEW mv_name;
REFRESH MATERIALIZED VIEW CONCURRENTLY mv_name;  -- no lock
```

### Temporary Tables

```sql
CREATE TEMP TABLE temp_name (id INT, name TEXT);
-- Auto-dropped at end of session
```

---

## 12. DML Operations

### INSERT

```sql
-- Single row
INSERT INTO table (col1, col2) VALUES (val1, val2);

-- Multiple rows
INSERT INTO table (col1, col2) VALUES 
  (val1, val2),
  (val3, val4);

-- From SELECT
INSERT INTO table (col1, col2) SELECT ... FROM ...;

-- Returning (PostgreSQL)
INSERT INTO table (col) VALUES (val) RETURNING id;
```

### UPDATE

```sql
UPDATE table SET col1 = val1, col2 = val2 WHERE condition;

-- Update from another table
UPDATE t1 SET col = t2.col FROM t2 WHERE t1.id = t2.t1_id;  -- PostgreSQL

-- Always use WHERE! (unless updating all)
```

### DELETE

```sql
DELETE FROM table WHERE condition;

-- Delete with join (PostgreSQL)
DELETE FROM t1 USING t2 WHERE t1.id = t2.t1_id;

-- TRUNCATE (faster for all rows)
TRUNCATE TABLE table_name;
TRUNCATE TABLE t RESTART IDENTITY;  -- reset serial
```

### UPSERT (INSERT or UPDATE)

```sql
-- PostgreSQL
INSERT INTO table (id, name) VALUES (1, 'test')
ON CONFLICT (id) DO UPDATE SET name = EXCLUDED.name;

-- MySQL
INSERT INTO table (id, name) VALUES (1, 'test')
ON DUPLICATE KEY UPDATE name = VALUES(name);
```

---

## 13. Constraints & Keys

### Types

```sql
-- Primary Key
PRIMARY KEY (col)
PRIMARY KEY (col1, col2)  -- composite

-- Foreign Key
REFERENCES other_table(col)
ON DELETE CASCADE | RESTRICT | SET NULL | SET DEFAULT
ON UPDATE CASCADE | RESTRICT | SET NULL | SET DEFAULT

-- Unique
UNIQUE (col)
UNIQUE (col1, col2)  -- composite

-- Not Null
NOT NULL

-- Check
CHECK (col >= 0)
CHECK (col IN ('a', 'b', 'c'))

-- Default
DEFAULT value
DEFAULT CURRENT_TIMESTAMP
```

### Example

```sql
CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  customer_id INT NOT NULL REFERENCES customers(id) ON DELETE CASCADE,
  total DECIMAL(10,2) CHECK (total >= 0),
  status VARCHAR(20) DEFAULT 'pending' CHECK (status IN ('pending', 'shipped', 'delivered')),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## 14. Indexes

### Basic Operations

```sql
-- Create
CREATE INDEX idx_name ON table(column);
CREATE INDEX idx_name ON table(col1, col2);  -- composite
CREATE UNIQUE INDEX idx_name ON table(column);

-- Drop
DROP INDEX idx_name;

-- Partial index (PostgreSQL)
CREATE INDEX idx_active ON orders(id) WHERE status = 'active';

-- Expression index
CREATE INDEX idx_lower ON users(LOWER(email));
```

### Index Types

| Type | Use Case |
|------|----------|
| B-tree (default) | Equality, range queries |
| Hash | Equality only |
| GIN | Arrays, JSONB, full-text |
| GiST | Geometric, full-text |
| BRIN | Large sequential tables |

### Guidelines

- Index columns in WHERE, JOIN, ORDER BY
- High selectivity columns first in composite index
- Consider covering indexes (INCLUDE columns)
- Don't over-index (slows writes)
- Rebuild/reindex periodically

---

## 15. Transactions

### Basic Syntax

```sql
BEGIN;
  -- statements
COMMIT;

-- or
BEGIN;
  -- statements
ROLLBACK;  -- undo all
```

### Savepoints

```sql
BEGIN;
  INSERT INTO ...;
  SAVEPOINT sp1;
  INSERT INTO ...;  -- might fail
  ROLLBACK TO sp1;  -- undo since savepoint
  INSERT INTO ...;  -- try again
COMMIT;
```

### Isolation Levels

| Level | Dirty Read | Non-Repeatable Read | Phantom Read |
|-------|------------|---------------------|--------------|
| READ UNCOMMITTED | Yes | Yes | Yes |
| READ COMMITTED | No | Yes | Yes |
| REPEATABLE READ | No | No | Yes* |
| SERIALIZABLE | No | No | No |

*PostgreSQL prevents phantoms in REPEATABLE READ

```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
```

### Locking

```sql
-- Row lock for update
SELECT * FROM table WHERE id = 1 FOR UPDATE;

-- Row lock for read
SELECT * FROM table WHERE id = 1 FOR SHARE;

-- Skip locked rows
SELECT * FROM table FOR UPDATE SKIP LOCKED;

-- Explicit table lock
LOCK TABLE table_name IN EXCLUSIVE MODE;
```

---

## 16. Query Optimization

### EXPLAIN

```sql
-- PostgreSQL
EXPLAIN SELECT ...;
EXPLAIN ANALYZE SELECT ...;  -- actually runs query
EXPLAIN (ANALYZE, BUFFERS, FORMAT JSON) SELECT ...;

-- MySQL
EXPLAIN SELECT ...;
EXPLAIN FORMAT=JSON SELECT ...;
```

### Common Issues & Solutions

| Issue | Solution |
|-------|----------|
| Full table scan | Add index on WHERE columns |
| Index not used | Check for functions on columns (not sargable) |
| Slow joins | Ensure join columns are indexed |
| Large result set | Add LIMIT, use cursors |
| Outdated stats | Run ANALYZE on tables |

### Sargable vs Non-Sargable

```sql
-- ❌ Non-sargable (can't use index)
WHERE YEAR(date_col) = 2024
WHERE column + 1 = 100
WHERE UPPER(name) = 'JOHN'

-- ✅ Sargable (can use index)
WHERE date_col >= '2024-01-01' AND date_col < '2025-01-01'
WHERE column = 99
WHERE name = 'John' -- if using case-insensitive collation
```

### Performance Tips

- Select only needed columns (avoid SELECT *)
- Use EXISTS instead of IN for large subqueries
- Avoid SELECT DISTINCT if not needed
- Use CTEs for readability, but check performance
- Batch large updates/deletes
- Use connection pooling
- Monitor slow query logs

---

## 17. JSON & Arrays

### JSON (PostgreSQL)

```sql
-- Types: JSON (text) vs JSONB (binary, faster)
CREATE TABLE t (data JSONB);

-- Access
data->'key'           -- returns JSON
data->>'key'          -- returns text
data->'obj'->'nested' -- nested access
data#>'{a,b}'         -- path access

-- Query
WHERE data->>'name' = 'John'
WHERE data @> '{"type": "premium"}'  -- contains

-- Update
UPDATE t SET data = data || '{"new": "value"}';
UPDATE t SET data = jsonb_set(data, '{key}', '"value"');

-- Index
CREATE INDEX idx_json ON t USING GIN (data);
```

### Arrays (PostgreSQL)

```sql
-- Type
col INTEGER[]
col TEXT[]

-- Access
arr[1]      -- 1-indexed
arr[1:3]    -- slice

-- Query
WHERE 'value' = ANY(arr)    -- contains
WHERE arr @> ARRAY['a','b'] -- contains all
WHERE arr && ARRAY['a','b'] -- overlaps

-- Unnest
SELECT unnest(arr) FROM t;

-- Aggregate to array
SELECT array_agg(col) FROM t;
```

---

## 18. Common Patterns

### Top N per Group

```sql
WITH ranked AS (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY group_col ORDER BY sort_col DESC) as rn
  FROM table
)
SELECT * FROM ranked WHERE rn <= 3;
```

### Running Total

```sql
SELECT date, amount,
  SUM(amount) OVER (ORDER BY date) as running_total
FROM transactions;
```

### Gap and Island Detection

```sql
-- Find gaps
SELECT curr.id + 1 as gap_start, next.id - 1 as gap_end
FROM table curr
JOIN table next ON next.id = (SELECT MIN(id) FROM table WHERE id > curr.id)
WHERE next.id - curr.id > 1;
```

### Pivot

```sql
SELECT 
  category,
  SUM(CASE WHEN month = 1 THEN sales END) as jan,
  SUM(CASE WHEN month = 2 THEN sales END) as feb,
  SUM(CASE WHEN month = 3 THEN sales END) as mar
FROM sales_data
GROUP BY category;
```

### De-duplication

```sql
-- Keep first occurrence
DELETE FROM table WHERE id NOT IN (
  SELECT MIN(id) FROM table GROUP BY unique_cols
);

-- Or with window function
WITH dupes AS (
  SELECT id, ROW_NUMBER() OVER (PARTITION BY unique_cols ORDER BY id) as rn
  FROM table
)
DELETE FROM table WHERE id IN (SELECT id FROM dupes WHERE rn > 1);
```

### Hierarchical Query

```sql
WITH RECURSIVE tree AS (
  SELECT id, name, parent_id, name AS path, 0 AS depth
  FROM items WHERE parent_id IS NULL
  UNION ALL
  SELECT i.id, i.name, i.parent_id, tree.path || ' > ' || i.name, tree.depth + 1
  FROM items i JOIN tree ON i.parent_id = tree.id
)
SELECT * FROM tree ORDER BY path;
```

---

## Quick Reference Card

| Task | Syntax |
|------|--------|
| Filter rows | `WHERE condition` |
| Sort results | `ORDER BY col [ASC\|DESC]` |
| Limit rows | `LIMIT n OFFSET m` |
| Remove duplicates | `SELECT DISTINCT` |
| Aggregate | `COUNT, SUM, AVG, MIN, MAX` |
| Group results | `GROUP BY col` |
| Filter groups | `HAVING condition` |
| Join tables | `JOIN ... ON condition` |
| Combine results | `UNION, INTERSECT, EXCEPT` |
| Window function | `func() OVER (PARTITION BY ... ORDER BY ...)` |
| NULL check | `IS NULL, IS NOT NULL, COALESCE` |
| Pattern match | `LIKE '%pattern%'` |
| Subquery | `WHERE col IN (SELECT ...)` |
| CTE | `WITH cte AS (...) SELECT ...` |
| Insert | `INSERT INTO t (cols) VALUES (vals)` |
| Update | `UPDATE t SET col = val WHERE ...` |
| Delete | `DELETE FROM t WHERE ...` |
| Create table | `CREATE TABLE t (cols)` |
| Add index | `CREATE INDEX idx ON t(col)` |
| Transaction | `BEGIN; ... COMMIT;` |

---

**End of SQL Cheatsheet**

*Last Updated: December 2024*  
*Compatible with: PostgreSQL 14+, MySQL 8+, SQL Server 2019+*
