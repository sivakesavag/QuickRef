# Chapter 19: Database & Data Handling

> **Topics Covered**: sqlite3, DB-API 2.0, parameterized queries, SQL injection, ORMs, SQLAlchemy basics, transactions, pandas basics, data cleaning, numpy fundamentals

---

## Questions

---

**Q19.1: Basic - [sqlite3 Basics]**

What is sqlite3?

A) External database server
B) Built-in Python module for SQLite — file-based SQL database
C) NoSQL database
D) Memory-only database

**Answer: B**

**Explanation:**
sqlite3 is in standard library. SQLite stores database in single file (or `:memory:`). No server needed. Perfect for small apps, testing, embedded. Full SQL support.

---

**Q19.2: Basic - [Connection and Cursor]**

What is the output?
```python
import sqlite3
conn = sqlite3.connect(':memory:')
cursor = conn.cursor()
print(type(cursor))
```

A) `<class 'Connection'>`
B) `<class 'sqlite3.Cursor'>`
C) `<class 'Database'>`
D) Error

**Answer: B**

**Explanation:**
`connect()` returns Connection. `cursor()` returns Cursor for executing SQL. `:memory:` creates in-memory database. Connection manages transactions, cursor executes queries.

---

**Q19.3: Intermediate - [Basic CRUD]**

What is the output?
```python
import sqlite3
conn = sqlite3.connect(':memory:')
conn.execute('CREATE TABLE t (id INTEGER, name TEXT)')
conn.execute('INSERT INTO t VALUES (1, "Alice")')
conn.commit()
result = conn.execute('SELECT * FROM t').fetchone()
print(result)
```

A) `{'id': 1, 'name': 'Alice'}`
B) `(1, 'Alice')`
C) `['Alice']`
D) Error

**Answer: B**

**Explanation:**
`fetchone()` returns tuple by default. `fetchall()` returns list of tuples. `fetchmany(n)` returns n rows. Use `row_factory = sqlite3.Row` for dict-like access.

---

**Q19.4: Intermediate - [Parameterized Queries]**

Why is this better?
```python
# Instead of: f"SELECT * FROM users WHERE id = {user_id}"
cursor.execute("SELECT * FROM users WHERE id = ?", (user_id,))
```

A) Faster
B) Prevents SQL injection — values are escaped/handled safely
C) More readable
D) Required by SQLite

**Answer: B**

**Explanation:**
⚠️ SQL injection: `user_id = "1; DROP TABLE users"`. Parameterized queries separate SQL from data. DB driver safely handles values. NEVER use string formatting for SQL values.

---

**Q19.5: Intermediate - [SQL Injection Example]**

What's dangerous about this code?
```python
name = input("Enter name: ")  # User enters: '; DROP TABLE users; --
cursor.execute(f"SELECT * FROM users WHERE name = '{name}'")
```

A) Nothing
B) SQL injection — user input becomes SQL code, can delete data
C) Syntax error
D) Only affects name search

**Answer: B**

**Explanation:**
User input: `'; DROP TABLE users; --` makes SQL: `SELECT * FROM users WHERE name = ''; DROP TABLE users; --'`. Executes DROP. Always use parameterized queries!

---

**Q19.6: Intermediate - [Commit and Rollback]**

What does `conn.commit()` do?

A) Saves connection
B) Commits current transaction — makes changes permanent
C) Closes connection
D) Starts transaction

**Answer: B**

**Explanation:**
Changes aren't permanent until committed. `conn.rollback()` undoes uncommitted changes. Auto-commit can be enabled but explicit commits give control. Transaction ensures atomicity.

---

**Q19.7: Intermediate - [Context Manager]**

What is the output?
```python
import sqlite3
with sqlite3.connect(':memory:') as conn:
    conn.execute('CREATE TABLE t (x INTEGER)')
    conn.execute('INSERT INTO t VALUES (1)')
# After with block
print("Done")
```

A) Auto-commits on successful exit
B) Auto-closes connection
C) Error
D) Data not saved

**Answer: A**

**Explanation:**
`with` auto-commits on normal exit, rollbacks on exception. Connection is NOT closed — just commit/rollback. Use `conn.close()` explicitly or nested with for both behaviors.

---

**Q19.8: Intermediate - [DB-API 2.0]**

What is DB-API 2.0 (PEP 249)?

A) Database version
B) Standard interface for Python database modules
C) SQL standard
D) API version for web

**Answer: B**

**Explanation:**
DB-API 2.0: standard connection/cursor interface. sqlite3, psycopg2 (PostgreSQL), mysql-connector follow it. Learn once, apply to different databases. Common methods: connect, cursor, execute, fetch*.

---

**Q19.9: Intermediate - [Row Factory]**

What is the output?
```python
import sqlite3
conn = sqlite3.connect(':memory:')
conn.row_factory = sqlite3.Row
conn.execute('CREATE TABLE t (id INT, name TEXT)')
conn.execute('INSERT INTO t VALUES (1, "Alice")')
row = conn.execute('SELECT * FROM t').fetchone()
print(row['name'], row[1])
```

A) Error
B) `Alice, Alice`
C) `name, 1`
D) `Alice, 1`

**Answer: B**

**Explanation:**
`sqlite3.Row` allows column access by name AND index. `row['name']` and `row[1]` both work. More readable than tuple indices. Standard pattern for dict-like rows.

---

**Q19.10: Intermediate - [executemany]**

What is the benefit of `executemany`?
```python
data = [(1, 'a'), (2, 'b'), (3, 'c')]
cursor.executemany('INSERT INTO t VALUES (?, ?)', data)
```

A) No benefit
B) Efficient bulk insert — single SQL parse, multiple executions
C) Parallel execution
D) Required for lists

**Answer: B**

**Explanation:**
Bulk operations more efficient: parse SQL once, bind different values. Faster than looping execute(). Use for batch inserts/updates. Data is list of tuples/dicts.

---

**Q19.11: Intermediate - [executescript]**

What does `cursor.executescript()` do?

A) Runs Python script
B) Executes multiple SQL statements separated by semicolons
C) Scripting language
D) Only for DDL

**Answer: B**

**Explanation:**
```python
cursor.executescript('''
    CREATE TABLE t1 (...);
    CREATE TABLE t2 (...);
    INSERT INTO t1 VALUES (...);
''')
```
Multiple statements in one call. Commits first, then executes. Useful for schema setup, migrations.

---

**Q19.12: Intermediate - [SQLite Data Types]**

What types does SQLite actually store?

A) All Python types
B) NULL, INTEGER, REAL, TEXT, BLOB only
C) Same as PostgreSQL
D) No types

**Answer: B**

**Explanation:**
SQLite has 5 storage classes. Type affinity: declared types map to these. Python sqlite3 converts: int↔INTEGER, float↔REAL, str↔TEXT, bytes↔BLOB, None↔NULL.

---

**Q19.13: Intermediate - [Transactions]**

What is a database transaction?

A) Payment processing
B) Atomic unit of work — all operations succeed or all fail (rolled back)
C) Single query
D) Connection

**Answer: B**

**Explanation:**
ACID: Atomic (all-or-nothing), Consistent, Isolated, Durable. Transaction groups operations. Error? Rollback all. Success? Commit all. Prevents partial updates, data corruption.

---

**Q19.14: Intermediate - [SQLAlchemy Core vs ORM]**

What's the difference between SQLAlchemy Core and ORM?

A) No difference
B) Core: SQL expression language; ORM: Python classes map to tables
C) Core is faster always
D) ORM is deprecated

**Answer: B**

**Explanation:**
Core: build SQL programmatically, still explicit SQL. ORM: define Python classes, SQLAlchemy generates SQL. ORM is higher-level, Core gives more control. Both use same connection engine.

---

**Q19.15: Intermediate - [ORM Example]**

What is an ORM?

A) Object Reader Module
B) Object-Relational Mapping — maps classes to tables, objects to rows
C) Database type
D) Query language

**Answer: B**

**Explanation:**
ORM: Python class `User` maps to `users` table. `User()` instance = row. Attributes = columns. `session.add(user)` inserts. Abstract away SQL (mostly). SQLAlchemy, Django ORM popular.

---

**Q19.16: Intermediate - [SQLAlchemy Model]**

What does this define?
```python
from sqlalchemy import Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base

Base = declarative_base()

class User(Base):
    __tablename__ = 'users'
    id = Column(Integer, primary_key=True)
    name = Column(String(50))
```

A) Python class only
B) Database table mapping — User class maps to users table
C) SQL query
D) Data transfer object

**Answer: B**

**Explanation:**
Declarative model: class = table, columns = Column objects. `Base.metadata.create_all(engine)` creates tables. Query: `session.query(User).filter(User.name == 'Alice').first()`. ORM pattern.

---

**Q19.17: Intermediate - [Session Management]**

What is SQLAlchemy Session?

A) User session
B) ORM unit of work — tracks object changes, manages transactions
C) Web session
D) Authentication

**Answer: B**

**Explanation:**
Session: "holding zone" for pending changes. `session.add(obj)`, `session.delete(obj)`. `session.commit()` writes to DB. `session.rollback()` undoes. Tracks object state (new, modified, deleted).

---

**Q19.18: Basic - [pandas Basics]**

What is a pandas DataFrame?

A) Picture frame
B) 2D labeled data structure (like spreadsheet/SQL table)
C) Python list
D) Database table

**Answer: B**

**Explanation:**
DataFrame: rows and columns with labels. `df = pd.DataFrame({'A': [1,2], 'B': [3,4]})`. Access: `df['A']`, `df.loc[0]`, `df.iloc[0]`. Industry standard for data analysis in Python.

---

**Q19.19: Intermediate - [Reading CSV]**

What is the output?
```python
import pandas as pd
df = pd.read_csv('data.csv')
print(type(df))
```

A) `<class 'list'>`
B) `<class 'pandas.core.frame.DataFrame'>`
C) `<class 'csv.reader'>`
D) Error

**Answer: B**

**Explanation:**
`read_csv()` parses CSV into DataFrame. Also: `read_excel()`, `read_json()`, `read_sql()`. `df.to_csv('out.csv')` writes back. pandas handles many data formats.

---

**Q19.20: Intermediate - [DataFrame Selection]**

What is the output?
```python
import pandas as pd
df = pd.DataFrame({'A': [1, 2, 3], 'B': [4, 5, 6]})
print(df[df['A'] > 1]['B'].sum())
```

A) `15`
B) `11`
C) `[5, 6]`
D) Error

**Answer: B**

**Explanation:**
`df['A'] > 1` creates boolean mask. `df[mask]` filters rows where A > 1 (rows with A=2,3). `['B']` selects column B (values 5, 6). `.sum()` = 11. Chainable operations.

---

**Q19.21: Intermediate - [Missing Data]**

What is the output?
```python
import pandas as pd
import numpy as np
df = pd.DataFrame({'A': [1, np.nan, 3]})
print(df['A'].isna().sum())
```

A) `3`
B) `1`
C) `0`
D) `NaN`

**Answer: B**

**Explanation:**
`np.nan` represents missing data. `isna()` returns boolean Series (True where NaN). `.sum()` counts Trues = 1 missing value. `fillna(0)` replaces NaN. `dropna()` removes rows with NaN.

---

**Q19.22: Intermediate - [GroupBy]**

What is the output?
```python
import pandas as pd
df = pd.DataFrame({
    'category': ['A', 'A', 'B', 'B'],
    'value': [1, 2, 3, 4]
})
print(df.groupby('category')['value'].sum().to_dict())
```

A) `{'A': 3, 'B': 7}`
B) `[3, 7]`
C) `10`
D) Error

**Answer: A**

**Explanation:**
GroupBy: split by category, apply sum to each group. A: 1+2=3, B: 3+4=7. Like SQL `GROUP BY`. Common aggregations: sum, mean, count, min, max.

---

**Q19.23: Intermediate - [Data Cleaning]**

What is the output?
```python
import pandas as pd
df = pd.DataFrame({'name': ['  Alice  ', 'BOB', 'charlie']})
df['name'] = df['name'].str.strip().str.title()
print(df['name'].tolist())
```

A) `['Alice', 'Bob', 'Charlie']`
B) `['alice', 'bob', 'charlie']`
C) `['  Alice  ', 'BOB', 'charlie']`
D) Error

**Answer: A**

**Explanation:**
String accessor `.str`: `strip()` removes whitespace, `title()` capitalizes first letter of each word. Data cleaning common: strip, lower/upper/title, replace, remove duplicates.

---

**Q19.24: Basic - [numpy Basics]**

What is numpy array advantage over list?

A) More flexible
B) Fast vectorized operations, less memory, C-level speed
C) Easier syntax
D) No advantage

**Answer: B**

**Explanation:**
numpy: homogeneous data stored contiguously. Operations: whole-array math without loops. `arr * 2` multiplies all elements. 10-100x faster than Python loops. Foundation for pandas, scipy.

---

**Q19.25: Intermediate - [numpy Array Creation]**

What is the output?
```python
import numpy as np
arr = np.array([1, 2, 3])
print(arr * 2, arr.dtype)
```

A) `[1, 2, 3, 1, 2, 3], list`
B) `[2 4 6], int64` (or int32)
C) Error
D) `[2, 4, 6], object`

**Answer: B**

**Explanation:**
numpy `*` is element-wise multiplication, not replication. `[2, 4, 6]`. `dtype` is automatically inferred (int64 on 64-bit). Vectorized: no loop needed, C-speed.

---

**Q19.26: Intermediate - [Vectorized Operations]**

What is the output?
```python
import numpy as np
a = np.array([1, 2, 3])
b = np.array([4, 5, 6])
print(a + b)
```

A) `[1, 2, 3, 4, 5, 6]`
B) `[5 7 9]`
C) Error
D) `15`

**Answer: B**

**Explanation:**
Element-wise addition: [1+4, 2+5, 3+6]. No loop needed. Also: `a - b`, `a * b`, `a / b`, `a ** 2`, etc. Vectorization = Python loops replaced by C loops.

---

**Q19.27: Intermediate - [numpy Aggregations]**

What is the output?
```python
import numpy as np
arr = np.array([[1, 2], [3, 4]])
print(arr.sum(), arr.sum(axis=0), arr.sum(axis=1))
```

A) `10, 10, 10`
B) `10, [4 6], [3 7]`
C) `10, [3 7], [4 6]`
D) Error

**Answer: B**

**Explanation:**
`sum()` = all elements = 10. `axis=0` = sum down columns = [1+3, 2+4] = [4, 6]. `axis=1` = sum across rows = [1+2, 3+4] = [3, 7]. Axis 0 is rows (vertical), 1 is columns (horizontal).

---

**Q19.28: Intermediate - [Boolean Indexing]**

What is the output?
```python
import numpy as np
arr = np.array([1, 2, 3, 4, 5])
mask = arr > 2
print(arr[mask])
```

A) `[True, True, True]`
B) `[3 4 5]`
C) `[1 2]`
D) `3`

**Answer: B**

**Explanation:**
Boolean mask: `arr > 2` = [F, F, T, T, T]. Indexing with mask returns elements where True. Powerful filtering without loops. Works with pandas too.

---

**Q19.29: Intermediate - [Reshaping Arrays]**

What is the output?
```python
import numpy as np
arr = np.arange(6).reshape(2, 3)
print(arr.shape)
```

A) `(6,)`
B) `(2, 3)`
C) `6`
D) `[2, 3]`

**Answer: B**

**Explanation:**
`arange(6)` = [0,1,2,3,4,5]. `reshape(2,3)` = 2 rows × 3 columns matrix. `.shape` returns dimension tuple. `-1` in reshape = infer: `reshape(-1, 3)` = "whatever rows needed for 3 columns".

---

**Q19.30: Intermediate - [Broadcasting]**

What is the output?
```python
import numpy as np
a = np.array([[1, 2, 3]])  # Shape (1, 3)
b = np.array([[10], [20]])  # Shape (2, 1)
print((a + b).shape)
```

A) Error
B) `(2, 3)`
C) `(1, 3)`
D) `(3, 2)`

**Answer: B**

**Explanation:**
Broadcasting: arrays with compatible shapes can combine. (1,3) + (2,1) → each broadcasts to (2,3). Result: [[11,12,13], [21,22,23]]. No explicit loop or replication needed. Powerful for matrix ops.

---

**Q19.31: Intermediate - [Connection Pooling]**

Why use connection pooling for databases?

A) Security
B) Reuse connections — avoid overhead of creating new connections per request
C) Faster queries
D) Required by SQL

**Answer: B**

**Explanation:**
Creating database connection is expensive (network, auth). Pool maintains open connections, reuses them. Libraries: SQLAlchemy has built-in pool, `psycopg2.pool`. Essential for web apps with many requests.

---

**Q19.32: Intermediate - [Prepared Statements]**

What is a prepared statement?

A) Pre-written SQL
B) SQL template compiled once, executed multiple times with parameters
C) Draft query
D) Same as stored procedure

**Answer: B**

**Explanation:**
Database compiles query plan once. Execute with different parameters — faster. Python parameterized queries often become prepared statements. Security + performance benefit.

---

**Q19.33: Intermediate - [Migrations]**

What are database migrations?

A) Moving databases
B) Version-controlled schema changes — create/alter tables in deployable scripts
C) Data backup
D) Server moves

**Answer: B**

**Explanation:**
Migrations: incremental schema changes. Each migration has upgrade/downgrade. Tools: Alembic (SQLAlchemy), Django migrations. Track database version, apply changes consistently across environments.

---

**Q19.34: Intermediate - [N+1 Query Problem]**

What is the N+1 query problem?

A) Query limit
B) One query per parent + N queries for children — inefficient; use JOIN or eager loading
C) Maximum results
D) Connection limit

**Answer: B**

**Explanation:**
```python
users = query(User).all()  # 1 query
for u in users:
    print(u.posts)  # N queries (one per user)
```
Solution: `query(User).options(joinedload(User.posts))` — single query with JOIN. ORM anti-pattern to avoid.

---

**Q19.35: Intermediate - [pandas merge]**

What is the output?
```python
import pandas as pd
df1 = pd.DataFrame({'key': [1, 2], 'value': ['a', 'b']})
df2 = pd.DataFrame({'key': [1, 2], 'other': ['x', 'y']})
merged = pd.merge(df1, df2, on='key')
print(len(merged))
```

A) `4`
B) `2`
C) `1`
D) Error

**Answer: B**

**Explanation:**
`merge` joins DataFrames on key column. Inner join by default — matching keys only. Both have 1,2 so 2 rows result. Like SQL JOIN. `how='left'`, `'right'`, `'outer'` for other join types.

---

**Q19.36: Intermediate - [pandas to_sql]**

What does this do?
```python
import pandas as pd
import sqlite3
conn = sqlite3.connect('data.db')
df.to_sql('table_name', conn, if_exists='replace')
```

A) Reads SQL
B) Writes DataFrame to database table
C) Creates connection
D) Executes query

**Answer: B**

**Explanation:**
`to_sql` writes DataFrame to database. `if_exists`: 'fail', 'replace', 'append'. Reverse: `pd.read_sql('SELECT * FROM t', conn)`. Easy pandas ↔ database interchange.

---

**Q19.37: Intermediate - [Data Validation]**

How to validate data types in pandas?

A) No validation
B) Use dtype checks, assertions, or libraries like pandera
C) Only during read
D) SQL handles it

**Answer: B**

**Explanation:**
`df.dtypes` shows column types. `df['col'].astype(int)` converts/validates. `pandera` library: define schemas, validate DataFrames. Important for data pipelines.

---

**Q19.38: Intermediate - [Memory Optimization]**

How to reduce pandas DataFrame memory usage?

A) Not possible
B) Use appropriate dtypes (category, int8 vs int64), chunked reading
C) More RAM only
D) Use lists instead

**Answer: B**

**Explanation:**
`df['status'] = df['status'].astype('category')` — small string sets use less memory. int8 vs int64 for small numbers. `pd.read_csv(..., chunksize=1000)` for large files. `df.memory_usage()` to check.

---

**Q19.39: Intermediate - [NoSQL vs SQL]**

When prefer NoSQL over SQL databases?

A) Always
B) Flexible schema, horizontal scaling, document/key-value data; SQL for structured, relational data
C) Never
D) Performance only

**Answer: B**

**Explanation:**
SQL: structured data, relationships, ACID, complex queries. NoSQL (MongoDB, Redis, Cassandra): flexible schema, scale horizontally, specific data models. Choose based on data structure and requirements.

---

**Q19.40: Intermediate - [sqlite3 Adapters]**

What are sqlite3 adapters?

A) Hardware
B) Functions to convert Python types to SQLite types for storage
C) GUI tools
D) Query builders

**Answer: B**

**Explanation:**
`sqlite3.register_adapter(type, func)` — convert Python object to SQLite value. `register_converter(typename, func)` — convert back. Handle custom types like datetime, decimal, UUID.

---

**Q19.41: Intermediate - [Index Usage]**

Why create database indexes?

A) Required
B) Speed up queries on indexed columns (slower writes as trade-off)
C) Documentation
D) Security

**Answer: B**

**Explanation:**
Index: data structure for fast lookup. `CREATE INDEX idx ON table(column)`. Query on indexed column: O(log n) vs O(n). Trade-off: slower inserts/updates (maintain index). Primary keys auto-indexed.

---

**Q19.42: Intermediate - [ACID Properties]**

What does ACID stand for?

A) Database version
B) Atomicity, Consistency, Isolation, Durability — transaction guarantees
C) Access Control ID
D) Query language

**Answer: B**

**Explanation:**
Atomicity: all or nothing. Consistency: valid state to valid state. Isolation: concurrent transactions don't interfere. Durability: committed data survives crashes. Fundamental database reliability properties.

---

**Q19.43: Intermediate - [pandas Pivot]**

What does `pivot_table` do?

A) Rotates data
B) Creates spreadsheet-style summary table with aggregations
C) Sorts data
D) Filters data

**Answer: B**

**Explanation:**
`df.pivot_table(values='sales', index='region', columns='year', aggfunc='sum')` — like Excel pivot. Rows: regions, columns: years, cells: sum of sales. Powerful for data analysis.

---

**Q19.44: Intermediate - [numpy nan handling]**

What is the output?
```python
import numpy as np
arr = np.array([1, 2, np.nan, 4])
print(np.nansum(arr), np.sum(arr))
```

A) `7.0, 7.0`
B) `7.0, nan`
C) `nan, nan`
D) Error

**Answer: B**

**Explanation:**
`np.nansum` ignores NaN: 1+2+4=7. Regular `sum` with NaN = NaN (propagates). Also: `nanmean`, `nanstd`, etc. Use nan-functions when data may have missing values.

---

**Q19.45: Intermediate - [DataFrame apply]**

What is the output?
```python
import pandas as pd
df = pd.DataFrame({'A': [1, 2, 3]})
df['B'] = df['A'].apply(lambda x: x ** 2)
print(df['B'].tolist())
```

A) `[1, 2, 3]`
B) `[1, 4, 9]`
C) `[2, 4, 6]`
D) Error

**Answer: B**

**Explanation:**
`apply()` applies function to each element (Series) or row/column (DataFrame). Lambda squares each value: 1→1, 2→4, 3→9. Flexible but slower than vectorized operations when those are available.

---

**Q19.46: Intermediate - [Database Backup]**

How to backup SQLite database?

A) Copy file only
B) Copy file (while no writes), or use sqlite3 backup API
C) Export SQL
D) Can't backup

**Answer: B**

**Explanation:**
SQLite: single file, can copy if no concurrent writes. `conn.backup(backup_conn)` — safe backup API. For production databases, use dump or built-in backup tools (pg_dump, mysqldump).

---

**Q19.47: Intermediate - [Query Optimization]**

How to optimize slow database queries?

A) Faster hardware only
B) Add indexes, EXPLAIN analysis, avoid SELECT *, batch operations
C) Use more connections
D) Switch database

**Answer: B**

**Explanation:**
EXPLAIN shows query plan — identify full table scans. Add indexes on WHERE/JOIN columns. SELECT only needed columns. Batch inserts/updates. Consider query restructuring. Profile before optimizing.

---

**Q19.48: Intermediate - [pandas loc vs iloc]**

What's the difference between `loc` and `iloc`?

A) No difference
B) loc uses labels; iloc uses integer positions
C) loc is faster
D) iloc is deprecated

**Answer: B**

**Explanation:**
`df.loc['row_label', 'col_label']` — label-based. `df.iloc[0, 1]` — integer position (0-indexed). `df.loc[0]` ≠ `df.iloc[0]` if index isn't 0,1,2... Important distinction.

---

**Q19.49: Intermediate - [Time Series]**

What makes pandas good for time series?

A) Nothing special
B) DatetimeIndex, resampling, rolling windows, shift operations
C) Only for dates
D) Required library

**Answer: B**

**Explanation:**
`pd.to_datetime()` parses dates. DatetimeIndex enables: `df.resample('M').sum()` (monthly aggregation), `df.rolling(7).mean()` (7-period moving average), `df.shift(1)` (lag). Powerful time series tools.

---

**Q19.50: Intermediate - [Data Pipelines]**

What is a data pipeline?

A) Database connection
B) Sequence of data processing steps: extract, transform, load (ETL)
C) Network pipe
D) Visualization

**Answer: B**

**Explanation:**
Pipeline: read data (extract), clean/transform, save (load). pandas: chain operations `df.pipe(func1).pipe(func2)`. ETL tools: Apache Airflow, Luigi, Prefect. Reproducible data processing.

---

## Chapter Summary

**Total MCQs: 50**

| Difficulty | Count | Percentage |
|------------|-------|------------|
| Basic | 5 | 10% |
| Intermediate | 45 | 90% |
| Advanced | 0 | 0% |
| Expert | 0 | 0% |

**Key Topics Covered:**
- sqlite3 and DB-API 2.0
- SQL injection prevention
- Transactions and ACID
- SQLAlchemy ORM basics
- pandas DataFrame operations
- Data cleaning and manipulation
- numpy fundamentals
- Database optimization
- Data pipelines
