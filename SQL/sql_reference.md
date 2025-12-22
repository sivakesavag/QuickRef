# SQL Curriculum Quick Reference

> Quick guide to navigate the SQL curriculum files and understand what's covered where.

---

## Files in This Folder

| File | Lines | Description |
|------|-------|-------------|
| `sql_assign.md` | ~3,400 | Main curriculum with 200 questions + 3 capstone projects |
| `sql_cheatsheet.md` | ~700 | Comprehensive SQL reference covering all topics |
| `sql_reference.md` | - | This file - navigation guide |

---

## Question Distribution

| Level | Questions | Topics Covered |
|-------|-----------|----------------|
| 🟢 Beginner | Q1-50 | SELECT, WHERE, ORDER BY, GROUP BY, HAVING, basic JOINs, INSERT/UPDATE/DELETE |
| 🟡 Intermediate | Q51-110 | Advanced joins, subqueries, CTEs, UNION/INTERSECT/EXCEPT, date/string functions, NULL handling |
| 🔴 Advanced | Q111-170 | Window functions (20), recursive CTEs (10), data modeling (10), DDL (10), query optimization (10) |
| 🔴 Expert | Q171-200 | Transactions (10), JSON/arrays/pivots (10), real-world case studies (10) |

**Total: 200 questions**

---

## Topic → Question Mapping

| # | Topic | Questions |
|---|-------|-----------|
| 1 | SELECT basics, filtering, sorting, LIMIT/OFFSET | Q1-15 |
| 2 | Aggregations, GROUP BY, HAVING | Q16-30 |
| 3 | Joins (inner/left/right/full/self/anti/semi) | Q31-45, Q51-65 |
| 4 | Subqueries, CTEs (recursive + non-recursive) | Q46-50, Q66-80, Q131-140 |
| 5 | Set operations (UNION/INTERSECT/EXCEPT) | Q81-90 |
| 6 | Window functions (ranking, frames, analytics) | Q111-130 |
| 7 | Date/time, strings, regex, NULL logic | Q91-110 |
| 8 | Data modeling: keys, constraints, normalization | Q141-150 |
| 9 | DDL + DML operations | Q46-50, Q151-160 |
| 10 | Transactions, isolation levels, locks | Q171-180 |
| 11 | Query tuning: EXPLAIN, indexing, sargability | Q161-170 |
| 12 | Advanced: JSON, arrays, pivots, full-text | Q181-190 |
| 13 | Real-world case studies | Q191-200 |

---

## Capstone Mini-Projects

| # | Project | Focus Areas |
|---|---------|-------------|
| 1 | E-Commerce Analytics Platform | Schema design, dashboards, RFM analysis, optimization |
| 2 | Banking Transaction System | OLTP design, transactions, concurrency, fraud detection |
| 3 | Social Media Analytics | Engagement metrics, network analysis, recommendations |

---

## Cheatsheet Sections

| Section | Content |
|---------|---------|
| SELECT Basics | Basic queries, aliasing, DISTINCT |
| Filtering & Sorting | WHERE, ORDER BY, LIKE, IN, BETWEEN |
| Aggregations | COUNT, SUM, AVG, MIN, MAX, GROUP BY, HAVING |
| Joins | All join types with visual diagrams |
| Subqueries & CTEs | Scalar, correlated, recursive CTEs |
| Set Operations | UNION, INTERSECT, EXCEPT |
| Window Functions | ROW_NUMBER, RANK, LAG, LEAD, frames |
| Date/Time | Extraction, arithmetic, formatting (multi-dialect) |
| String Functions | Concatenation, substring, pattern matching |
| NULL Handling | COALESCE, NULLIF, three-valued logic |
| DDL & DML | CREATE, ALTER, DROP, INSERT, UPDATE, DELETE |
| Indexes | Types, creation, optimization tips |
| Transactions | BEGIN, COMMIT, ROLLBACK, isolation levels |
| Query Optimization | EXPLAIN, sargability, performance tips |
| JSON & Arrays | PostgreSQL JSONB/arrays |
| Common Patterns | Top N, running totals, pivots, deduplication |

---

## Estimated Completion Time

- Questions: 60-80 hours
- Capstone Projects: 20-30 hours
- **Total: 80-120 hours**

---

**Status: ✅ Complete**
