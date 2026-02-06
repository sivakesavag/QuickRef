# Chapter 27: Database Integration

**Target MCQs**: 50-60
**Current Batch**: 1-30
**Topics Covered**: `sqlite3` driver (Cursors, Connections, Transactions), DB-API 2.0 specs, PostgreSQL (`psycopg2`), SQLAlchemy (Core, ORM, Connection Pooling), NoSQL Basics (MongoDB/`pymongo`), Key-Value stores (`redis`), Context Managers for DBs, SQL Injection Prevention.

---

**Q27.1: Basic - [SQLite Standard Library]**

Which database module is included in Python's standard library?

A) `sqlite3`
B) `mysql`
C) `psycopg2`
D) `pymongo`

**Answer: A**

**Explanation:**
Lightweight, disk-based database requiring no separate server process.

---

**Q27.2: Intermediate - [Cursor Object]**

In Python's DB-API 2.0 (like `sqlite3`), a "Cursor" is used to:

A) Click buttons.
B) Execute SQL queries and traverse/fetch the results.
C) Close the database.
D) Encrypt data.

**Answer: B**

**Explanation:**
`cur = conn.cursor()`; `cur.execute(sql)`.

---

**Q27.3: Advanced - [Commit vs Rollback]**

If you execute an INSERT statement but forget to call `conn.commit()`:

A) The data is saved automatically.
B) The changes are lost (rolled back) when the connection closes, as transactions are predominantly implicit.
C) The database corrupts.
D) It throws an error.

**Answer: B**

**Explanation:**
Most Python DB drivers start a transaction automatically. You must explicitly commit.

---

**Q27.4: Basic - [Fetches]**

To retrieve all rows from a query result, use:

A) `cursor.fetchall()`
B) `cursor.get_all()`
C) `cursor.read()`
D) `cursor.rows()`

**Answer: A**

**Explanation:**
Returns a list of tuples. Be careful with large datasets (use `fetchone` or `fetchmany` or iterate the cursor).

---

**Q27.5: Intermediate - [SQL Injection Prevention]**

The correct way to safeguard against SQL Injection when inserting variables:

A) f-strings: `f"SELECT * FROM users WHERE name = '{name}'"`
B) String formatting: `"SELECT ... %s" % name`
C) Parameterized queries: `cursor.execute("SELECT * FROM users WHERE name = ?", (name,))`
D) String concatenation.

**Answer: C**

**Explanation:**
The driver handles escaping special characters safely. NEVER use string formatting for SQL values.

---

**Q27.6: Advanced - [Context Manager Connection]**

Using `with sqlite3.connect('db.db') as conn:` usually ensures:

A) The connection is automatically closed.
B) The transaction is automatically committed if no error occurs, or rolled back if an exception is raised (depending on implementation - `sqlite3` acts as a transaction manager).
C) Speed.
D) Nothing.

**Answer: B**

**Explanation:**
In `sqlite3`, the context manager typically handles the *transaction* commit/rollback, not just closing.

---

**Q27.7: Expert - [SQLAlchemy ORM vs Core]**

SQLAlchemy **Core** provides ________, while SQLAlchemy **ORM** provides ________.

A) High-level objects; Low-level strings.
B) A SQL Expression Language (schema-centric, close to SQL); A Domain Object Model (mapping classes to tables, higher level).
C) Functions; Classes.
D) Speed; Slowness.

**Answer: B**

**Explanation:**
Core is more precise/performant; ORM is more developer-friendly for business logic.

---

**Q27.8: Basic - [Connect]**

The function to open a database connection in `sqlite3` is:

A) `sqlite3.open()`
B) `sqlite3.connect()`
C) `sqlite3.init()`
D) `sqlite3.start()`

**Answer: B**

**Explanation:**
Returns a Connection object.

---

**Q27.9: Intermediate - [Executemany]**

To insert multiple rows efficiently in one go:

A) Loop over `execute()`.
B) `cursor.executemany("INSERT INTO t VALUES (?)", data_list)`
C) Write a text file.
D) Use threads.

**Answer: B**

**Explanation:**
Significantly faster than calling execute in a loop due to fewer round-trips/transaction overhead.

---

**Q27.10: Advanced - [Psycopg2]**

`psycopg2` is the most popular adapter for:

A) MySQL.
B) PostgreSQL.
C) Oracle.
D) MongoDB.

**Answer: B**

**Explanation:**
Robust, efficient, and fully implements DB-API 2.0.

---

**Q27.11: Basic - [Row Factory]**

Setting `conn.row_factory = sqlite3.Row` allows you to:

A) Access columns by name (like a dictionary) instead of just integer index.
B) Create rows.
C) Use factories.
D) Make it faster.

**Answer: A**

**Explanation:**
`row['column_name']` is much more readable than `row[3]`.

---

**Q27.12: Intermediate - [NoSQL - MongoDB]**

In `pymongo` (MongoDB driver), a "Collection" is roughly equivalent to a SQL:

A) Database.
B) Table.
C) Row.
D) Column.

**Answer: B**

**Explanation:**
And a "Document" is equivalent to a Row.

---

**Q27.13: Advanced - [Connection Pooling]**

The purpose of Connection Pooling (e.g., in SQLAlchemy) is to:

A) Share one connection with everyone.
B) Reuse active database connections from a pool instead of opening/closing a generic TCP connection for every request, which is expensive.
C) Save disk space.
D) Pool water.

**Answer: B**

**Explanation:**
Critical for high-performance web applications.

---

**Q27.14: Expert - [N+1 Problem]**

The "N+1 Select Problem" in ORMs occurs when:

A) You add 1 to N.
B) You fetch a parent object (1 query) and then iterate through its children, triggering a new separate query for *each* child (N queries), totaling N+1.
C) The DB crashes.
D) You have too many tables.

**Answer: B**

**Explanation:**
Solved by "Eager Loading" (e.g., `.joinedload()` in SQLAlchemy) to fetch everything in 1 query.

---

**Q27.15: Intermediate - [Redis]**

Redis is often used with Python as a:

A) Relational Database.
B) In-memory Key-Value store (for Caching, Message Brokering).
C) File system.
D) Compiler.

**Answer: B**

**Explanation:**
Extremely fast. Accessed via `redis-py`.

---

**Q27.16: Basic - [Primary Key]**

A Primary Key in a SQL table must be:

A) Red.
B) Unique and Not Null.
C) A string.
D) Optional.

**Answer: B**

**Explanation:**
Uniquely identifies a record.

---

**Q27.17: Advanced - [Declarative Base]**

In SQLAlchemy ORM, you typically define models by inheriting from:

A) `object`.
B) `DeclarativeBase` (or `declarative_base()`).
C) `db.Model`.
D) `sql.Class`.

**Answer: B**

**Explanation:**
Allows defining the table schema and the python class mapping in one place.

---

**Q27.18: Intermediate - [Transactions]**

The ACID property "Atomicity" means:

A) Only atoms are stored.
B) A transaction is treated as a single unit: either *all* operations succeed, or *none* do (rollback). Partial updates are impossible.
C) Data is isolated.
D) Data is durable.

**Answer: B**

**Explanation:**
Prevents data inconsistency (e.g., money deducted from A but not credited to B).

---

**Q27.19: Basic - [Where Clause]**

To filter results in SQL:

A) `FILTER BY`
B) `WHERE`
C) `IF`
D) `WHEN`

**Answer: B**

**Explanation:**
`SELECT * FROM table WHERE id = 1`.

---

**Q27.20: Expert - [Engine]**

In SQLAlchemy, the `Engine` (`create_engine`):

A) Is the starting point that manages the connection source (pool) and dialect to the database.
B) Is the car part.
C) Is a cursor.
D) Is a table.

**Answer: A**

**Explanation:**
`engine = create_engine('sqlite:///:memory:')`.

---

**Q27.21: Intermediate - [BSON]**

MongoDB (and pymongo) stores data in a format called BSON, which stands for:

A) Binary JSON.
B) Big JSON.
C) Basic JSON.
D) Bad JSON.

**Answer: A**

**Explanation:**
Supports more types than JSON (like Date, Binary) and is efficient for traversing.

---

**Q27.22: Basic - [Delete]**

To remove rows from a SQL table:

A) `REMOVE`
B) `DELETE FROM table WHERE ...`
C) `DROP`
D) `CUT`

**Answer: B**

**Explanation:**
`DROP` deletes the table structure itself.

---

**Q27.23: Advanced - [Migration]**

Tools like `Alembic` (for SQLAlchemy) or `Django Migrations` are used to:

A) Move data to the cloud.
B) Version control the database schema (create scripts to upgrade/downgrade schema structure) as code evolves.
C) Make backups.
D) Migrate birds.

**Answer: B**

**Explanation:**
Essential for team development to keep DBs in sync.

---

**Q27.24: Expert - [Cursor closing]**

Why is it important to close cursors and connections?

A) To be polite.
B) To release server-side resources (handles, memory, locks) and prevent "Too many connections" errors.
C) It isn't important.
D) Python does it instantly.

**Answer: B**

**Explanation:**
Though GC handles it eventually, explicit closure (or context managers) is safer for high load.

---

**Q27.25: Intermediate - [Foreign Key]**

A Foreign Key is:

A) A key from another country.
B) A field that links to the Primary Key of another table, establishing a relationship.
C) A password.
D) A backup.

**Answer: B**

**Explanation:**
Enforces referential integrity.

---

**Q27.26: Basic - [Null]**

In SQL, `NULL` represents:

A) Zero.
B) Empty String.
C) Missing or Undefined data.
D) False.

**Answer: C**

**Explanation:**
NULL is not equal to anything, even itself.

---

**Q27.27: Advanced - [DictCursor]**

In `psycopg2`, using `RealDictCursor`:

A) Returns results as Python dictionaries instead of tuples.
B) Returns a real dictionary.
C) Checks spelling.
D) Is slow.

**Answer: A**

**Explanation:**
Similar to `sqlite3.Row`, improves code readability at slightly higher memory cost.

---

**Q27.28: Expert - [SQL Injection - Placeholders]**

Which placeholder style does `sqlite3` use vs `psycopg2`?

A) Both use `%s`.
B) `sqlite3` uses `?` (qmark), `psycopg2` uses `%s` (format).
C) Both use `?`.
D) Both use `$1`.

**Answer: B**

**Explanation:**
This difference helps explain why ORMs are nice (they abstract this away).

---

**Q27.29: Intermediate - [Filter vs Get]**

In many ORMs, `filter()` (or `where`) returns ________, while `get()` returns ________.

A) A list/queryset; A single object (or raises error if not found/multiple).
B) One object; A list.
C) The same thing.
D) Integers.

**Answer: A**

**Explanation:**
`get` expects uniqueness.

---

**Q27.30: Basic - [Limit]**

To restrict the number of rows returned by a query:

A) `CAP 10`
B) `LIMIT 10`
C) `TOP 10`
D) `STOP 10`

**Answer: B**

**Explanation:**
Standard SQL syntax (though some dialects use TOP).

---

**Q27.31: Intermediate - [Order By]**

Result sets are unordered by default. To enforce an order:

A) `ORDER BY column ASC/DESC`
B) `SORT BY`
C) `SEQUENCE`
D) `RANK`

**Answer: A**

**Explanation:**
Without this, the DB is free to return rows in any order it finds fastest.

---

**Q27.32: Advanced - [Connection String]**

A typical SQLAlchemy connection string looks like:

A) `postgresql://user:password@localhost/dbname`
B) `http://user:password@localhost/dbname`
C) `file://dbname`
D) `dbname`

**Answer: A**

**Explanation:**
Follows the URL format: `dialect+driver://username:password@host:port/database`.

---

**Q27.33: Basic - [Join]**

A SQL JOIN is used to:

A) Combine rows from two or more tables, based on a related column between them.
B) Split a table.
C) Login.
D) Create a table.

**Answer: A**

**Explanation:**
`INNER JOIN` is the most common (returns only matching pairs).

---

**Q27.34: Expert - [Isolation Level]**

Setting the transaction isolation level to `READ UNCOMMITTED` allows:

A) Dirty Reads (seeing uncommitted changes from other transactions).
B) Better security.
C) Serial execution.
D) No reads.

**Answer: A**

**Explanation:**
Fastest but least safe. `SERIALIZABLE` is the safest but slowest.

---

**Q27.35: Intermediate - [Context Manager closing]**

If you don't use a context manager, you must ensure connections are closed in:

A) A `finally` block.
B) The `try` block.
C) The `else` block.
D) Global scope.

**Answer: A**

**Explanation:**
Guarantees execution even if errors occur.

---

**Q27.36: Advanced - [ORM Relationships]**

In SQLAlchemy, `relationship('Address', back_populates='user')`:

A) Defines a high-level navigation property, allowing you to access `user.addresses` as a list of Python objects.
B) Creates a foreign key column in the DB.
C) Deletes the table.
D) Validates the address.

**Answer: A**

**Explanation:**
The distinction between the `ForeignKey` (database schema) and `relationship` (ORM navigation) is key.

---

**Q27.37: Basic - [Create Table]**

To create a new table:

A) `MAKE TABLE`
B) `CREATE TABLE name (columns...)`
C) `NEW TABLE`
D) `INIT TABLE`

**Answer: B**

**Explanation:**
e.g., `CREATE TABLE users (id INTEGER PRIMARY KEY, name TEXT)`.

---

**Q27.38: Intermediate - [Like Operator]**

To find strings ending with "son":

A) `WHERE name LIKE '%son'`
B) `WHERE name = '*son'`
C) `WHERE name ENDS 'son'`
D) `WHERE name == 'son'`

**Answer: A**

**Explanation:**
`%` is the wildcard for any sequence of characters. `_` is for a single character.

---

**Q27.39: Advanced - [Upsert]**

An "Upsert" operation:

A) Inserts a row, or Updates it if it already exists (usually based on Primary Key conflict).
B) Deletes upper rows.
C) Sorts up.
D) Errors.

**Answer: A**

**Explanation:**
Syntaxes vary (e.g., SQLite `INSERT OR REPLACE`, Postgres `ON CONFLICT DO UPDATE`).

---

**Q27.40: Expert - [Connection vs Cursor]**

The Connection object represents ________, while the Cursor represents ________.

A) The session/socket; The state of a specific query/iteration.
B) The file; The user.
C) The query; The database.
D) The read; The write.

**Answer: A**

**Explanation:**
You can have multiple cursors per connection.

---

**Q27.41: Basic - [Count]**

To count the number of rows:

A) `COUNT(*)`
B) `SUM(*)`
C) `TOTAL(*)`
D) `NUM(*)`

**Answer: A**

**Explanation:**
Standard aggregate function.

---

**Q27.42: Intermediate - [Group By]**

`GROUP BY` is used to:

A) Group rows that have the same values in specified columns into summary rows (often used with aggregates like COUNT, MAX).
B) Sort rows.
C) Hide rows.
D) Join tables.

**Answer: A**

**Explanation:**
`SELECT department, COUNT(*) FROM employees GROUP BY department`.

---

**Q27.43: Advanced - [Session in ORM]**

In SQLAlchemy ORM, the `Session`:

A) Is a holding zone for all the objects you've loaded or associated with a database connection. It manages the "Unit of Work".
B) Is a cookie.
C) Is the database server.
D) Is a table.

**Answer: A**

**Explanation:**
You add objects to the session, and flush/commit them to persist changes.

---

**Q27.44: Expert - [Lazy Loading]**

"Lazy Loading" of relationships means:

A) Related data is not fetched from the DB until you actually access the attribute (e.g., `user.addresses`).
B) The database is slow.
C) The server sleeps.
D) Data is never fetched.

**Answer: A**

**Explanation:**
Saves initial bandwidth but can lead to the N+1 problem if iterating.

---

**Q27.45: Intermediate - [Distinct]**

`SELECT DISTINCT column ...`:

A) Returns unique values only (removes duplicates).
B) Returns all values.
C) Returns distinct errors.
D) Sorts values.

**Answer: A**

**Explanation:**
Useful for finding the set of available categories.

---

**Q27.46: Basic - [Update]**

Syntax to modify existing data:

A) `UPDATE table SET column = value WHERE ...`
B) `CHANGE table ...`
C) `MODIFY table ...`
D) `SET table ...`

**Answer: A**

**Explanation:**
Always remember the WHERE clause, or you update every row!

---

**Q27.47: Advanced - [Stored Procedures]**

Parametrized functions stored inside the database server are called:

A) Macros.
B) Stored Procedures.
C) Hooks.
D) Lambdas.

**Answer: B**

**Explanation:**
Can be called from Python (`cursor.callproc`), moving logic close to the data.

---

**Q27.48: Expert - [Index]**

Creating an INDEX on a column:

A) Speeds up retrieval (SELECT/WHERE) but slows down insertion/updates (overhead of maintaining the index structure).
B) Speeds up everything.
C) Slows down everything.
D) Saves space.

**Answer: A**

**Explanation:**
Like the index at the back of a book. Essential for performance on large tables.

---

**Q27.49: Intermediate - [Having Clause]**

`HAVING` is similar to `WHERE`, but it:

A) Filters groups *after* aggregation (e.g., `GROUP BY ... HAVING COUNT(*) > 5`).
B) Filters rows before grouping.
C) Starts the query.
D) Is faster.

**Answer: A**

**Explanation:**
`WHERE` cannot contain aggregate functions.

---

**Q27.50: Basic - [Drivers]**

Python needs a specific "Driver" (or adapter) for each Database type because:

A) It likes variety.
B) Each database uses a different wire protocol (binary format) to communicate.
C) It is slow.
D) It is old.

**Answer: B**

**Explanation:**
DB-API 2.0 provides the standard Python interface, but the driver (psycopg2, mysql-connector) implements the protocol.

---

---

## Review Notes (2026-02-06)

- No major content errors were identified in this review pass.
