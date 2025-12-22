# Comprehensive SQL Practice Curriculum

**160-200 Progressive Practice Questions | Beginner → Expert**

> **SQL Dialect**: PostgreSQL-compatible (differences noted for MySQL/SQL Server)  
> **Format**: Each question includes difficulty, skill tested, problem statement, expected output, and constraints

---

## Table of Contents

1. [Sample Schema](#sample-schema)
2. [Beginner Level (Q1-50)](#beginner-level)
3. [Intermediate Level (Q51-110)](#intermediate-level)
4. [Advanced Level (Q111-170)](#advanced-level)
5. [Expert Level (Q171-200)](#expert-level)
6. [Capstone Mini-Projects](#capstone-mini-projects)

---

## Curriculum Summary

| Level | Questions | Key Topics |
|-------|-----------|------------|
| 🟢 Beginner | Q1-50 | SELECT, filtering, sorting, aggregations, basic joins, DML |
| 🟡 Intermediate | Q51-110 | Advanced joins, subqueries, CTEs, set operations, date/time, strings, NULL |
| 🔴 Advanced | Q111-170 | Window functions, recursive CTEs, data modeling, DDL, optimization |
| 🔴 Expert | Q171-200 | Transactions, isolation, JSON/arrays, real-world case studies |

**🎓 Capstone Projects (3):**
1. E-commerce Analytics Platform
2. Banking Transaction System (OLTP)
3. Social Media Analytics Dashboard

**⏱ Estimated Completion Time:** 80-120 hours

---

# Sample Schema

## Entity Relationship Diagram

```
┌──────────────┐       ┌──────────────┐       ┌──────────────┐
│  categories  │──────<│   products   │──────<│ order_items  │
└──────────────┘       └──────────────┘       └──────────────┘
                              │                      │
                              ▼                      │
                       ┌──────────────┐              │
                       │  inventory   │              │
                       └──────────────┘              │
                                                     ▼
┌──────────────┐       ┌──────────────┐       ┌──────────────┐
│  customers   │──────<│    orders    │<──────┤  employees   │
└──────────────┘       └──────────────┘       └──────────────┘
                              │
                              ▼
                       ┌──────────────┐
                       │   payments   │
                       └──────────────┘
```

## Table Definitions

### categories
```sql
CREATE TABLE categories (
    category_id   SERIAL PRIMARY KEY,
    category_name VARCHAR(50) NOT NULL UNIQUE,
    description   TEXT,
    parent_id     INT REFERENCES categories(category_id),  -- Self-referencing for hierarchy
    created_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### products
```sql
CREATE TABLE products (
    product_id    SERIAL PRIMARY KEY,
    product_name  VARCHAR(100) NOT NULL,
    category_id   INT REFERENCES categories(category_id),
    unit_price    DECIMAL(10,2) NOT NULL CHECK (unit_price >= 0),
    cost_price    DECIMAL(10,2) CHECK (cost_price >= 0),
    sku           VARCHAR(20) UNIQUE,
    is_active     BOOLEAN DEFAULT TRUE,
    weight_kg     DECIMAL(5,2),
    description   TEXT,
    created_at    TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at    TIMESTAMP
);
```

### inventory
```sql
CREATE TABLE inventory (
    inventory_id    SERIAL PRIMARY KEY,
    product_id      INT REFERENCES products(product_id) UNIQUE,
    quantity        INT NOT NULL DEFAULT 0 CHECK (quantity >= 0),
    reorder_level   INT DEFAULT 10,
    warehouse_code  VARCHAR(10),
    last_restock    DATE,
    updated_at      TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### customers
```sql
CREATE TABLE customers (
    customer_id   SERIAL PRIMARY KEY,
    first_name    VARCHAR(50) NOT NULL,
    last_name     VARCHAR(50) NOT NULL,
    email         VARCHAR(100) UNIQUE NOT NULL,
    phone         VARCHAR(20),
    city          VARCHAR(50),
    country       VARCHAR(50) DEFAULT 'USA',
    registration_date DATE DEFAULT CURRENT_DATE,
    tier          VARCHAR(20) DEFAULT 'Bronze' CHECK (tier IN ('Bronze', 'Silver', 'Gold', 'Platinum')),
    is_active     BOOLEAN DEFAULT TRUE
);
```

### employees
```sql
CREATE TABLE employees (
    employee_id   SERIAL PRIMARY KEY,
    first_name    VARCHAR(50) NOT NULL,
    last_name     VARCHAR(50) NOT NULL,
    email         VARCHAR(100) UNIQUE,
    department    VARCHAR(50),
    hire_date     DATE NOT NULL,
    salary        DECIMAL(10,2),
    manager_id    INT REFERENCES employees(employee_id),  -- Self-referencing for hierarchy
    is_active     BOOLEAN DEFAULT TRUE
);
```

### orders
```sql
CREATE TABLE orders (
    order_id      SERIAL PRIMARY KEY,
    customer_id   INT REFERENCES customers(customer_id),
    employee_id   INT REFERENCES employees(employee_id),  -- Sales rep
    order_date    TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    shipped_date  TIMESTAMP,
    status        VARCHAR(20) DEFAULT 'Pending' 
                  CHECK (status IN ('Pending', 'Processing', 'Shipped', 'Delivered', 'Cancelled')),
    shipping_fee  DECIMAL(8,2) DEFAULT 0,
    notes         TEXT
);
```

### order_items
```sql
CREATE TABLE order_items (
    item_id       SERIAL PRIMARY KEY,
    order_id      INT REFERENCES orders(order_id) ON DELETE CASCADE,
    product_id    INT REFERENCES products(product_id),
    quantity      INT NOT NULL CHECK (quantity > 0),
    unit_price    DECIMAL(10,2) NOT NULL,  -- Price at time of order
    discount      DECIMAL(4,2) DEFAULT 0 CHECK (discount >= 0 AND discount <= 1),
    UNIQUE(order_id, product_id)
);
```

### payments
```sql
CREATE TABLE payments (
    payment_id     SERIAL PRIMARY KEY,
    order_id       INT REFERENCES orders(order_id),
    payment_date   TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    amount         DECIMAL(10,2) NOT NULL CHECK (amount > 0),
    payment_method VARCHAR(20) CHECK (payment_method IN ('Credit Card', 'Debit Card', 'PayPal', 'Bank Transfer', 'Cash')),
    status         VARCHAR(20) DEFAULT 'Completed' CHECK (status IN ('Pending', 'Completed', 'Failed', 'Refunded'))
);
```

## Sample Data Summary

| Table | Row Count | Key Characteristics |
|-------|-----------|---------------------|
| categories | 15 | 3 parent categories, 12 subcategories |
| products | 100 | Mixed active/inactive, various price ranges |
| inventory | 100 | Some at reorder level, some out of stock |
| customers | 500 | Mix of tiers, some inactive, multiple countries |
| employees | 25 | 5 departments, hierarchical structure |
| orders | 2000 | Various statuses, spans 2 years |
| order_items | 5000 | 1-5 items per order |
| payments | 1800 | Some orders unpaid, some refunded |

---

# Beginner Level

## Section 1: SELECT Basics, Filtering & Sorting (Q1-15)

---

### Q1. Basic SELECT

🟢 **Difficulty**: Beginner  
**Skill**: Basic SELECT statement

**Problem**: Write a query to retrieve all columns from the `customers` table.

**Expected Output**: All columns (customer_id, first_name, last_name, email, phone, city, country, registration_date, tier, is_active) for all customers.

**Constraints**: None

---

### Q2. Selecting Specific Columns

🟢 **Difficulty**: Beginner  
**Skill**: Column selection

**Problem**: Retrieve only the `first_name`, `last_name`, and `email` of all customers.

**Expected Output**:
| first_name | last_name | email |
|------------|-----------|-------|
| ... | ... | ... |

**Constraints**: Column order matters in output.

---

### Q3. Column Aliasing

🟢 **Difficulty**: Beginner  
**Skill**: AS keyword, aliasing

**Problem**: Select product names and their prices, renaming columns to `Product` and `Price`.

**Expected Output**:
| Product | Price |
|---------|-------|
| Widget A | 29.99 |

**Constraints**: Use meaningful aliases.

---

### Q4. DISTINCT Values

🟢 **Difficulty**: Beginner  
**Skill**: DISTINCT keyword

**Problem**: Find all unique countries where customers are located.

**Expected Output**: List of unique country names.

**Constraints**: No duplicates in result.

---

### Q5. WHERE Clause - Equality

🟢 **Difficulty**: Beginner  
**Skill**: WHERE clause, equality filter

**Problem**: Find all customers who are in the `'Gold'` tier.

**Expected Output**: All columns for Gold tier customers.

**Constraints**: Case-sensitive string matching.

---

### Q6. WHERE Clause - Comparison

🟢 **Difficulty**: Beginner  
**Skill**: Comparison operators

**Problem**: Find all products with a `unit_price` greater than 100.

**Expected Output**:
| product_id | product_name | unit_price |
|------------|--------------|------------|
| ... | ... | ... |

**Constraints**: > operator, not >=

---

### Q7. WHERE with AND

🟢 **Difficulty**: Beginner  
**Skill**: AND logical operator

**Problem**: Find all active customers (`is_active = TRUE`) located in `'New York'` city.

**Expected Output**: All columns for matching customers.

**Constraints**: Both conditions must be true.

---

### Q8. WHERE with OR

🟢 **Difficulty**: Beginner  
**Skill**: OR logical operator

**Problem**: Find all products in category_id 1 OR category_id 2.

**Expected Output**: All product details for matching categories.

**Constraints**: Either condition can be true.

---

### Q9. WHERE with IN

🟢 **Difficulty**: Beginner  
**Skill**: IN operator

**Problem**: Find all orders with status `'Pending'`, `'Processing'`, or `'Shipped'`.

**Expected Output**: order_id, customer_id, order_date, status

**Constraints**: Use IN instead of multiple ORs.

---

### Q10. WHERE with BETWEEN

🟢 **Difficulty**: Beginner  
**Skill**: BETWEEN operator

**Problem**: Find all products with `unit_price` between 50 and 150 (inclusive).

**Expected Output**: product_name, unit_price

**Constraints**: BETWEEN is inclusive on both ends.

---

### Q11. WHERE with LIKE

🟢 **Difficulty**: Beginner  
**Skill**: Pattern matching with LIKE

**Problem**: Find all customers whose email ends with `'@gmail.com'`.

**Expected Output**: first_name, last_name, email

**Constraints**: Case sensitivity depends on collation (assume case-sensitive).

---

### Q12. WHERE with NOT

🟢 **Difficulty**: Beginner  
**Skill**: NOT operator

**Problem**: Find all products that are NOT active (`is_active = FALSE`).

**Expected Output**: product_id, product_name, is_active

**Constraints**: Can also use `is_active = FALSE` directly.

---

### Q13. ORDER BY Single Column

🟢 **Difficulty**: Beginner  
**Skill**: Sorting with ORDER BY

**Problem**: List all products sorted by `unit_price` in descending order.

**Expected Output**: product_name, unit_price (highest price first)

**Constraints**: DESC keyword required.

---

### Q14. ORDER BY Multiple Columns

🟢 **Difficulty**: Beginner  
**Skill**: Multi-column sorting

**Problem**: List all customers sorted by `country` (ascending), then by `last_name` (ascending).

**Expected Output**: first_name, last_name, country

**Constraints**: Primary sort by country, secondary by last_name.

---

### Q15. LIMIT and OFFSET

🟢 **Difficulty**: Beginner  
**Skill**: Pagination with LIMIT/OFFSET

**Problem**: Get the 5 most expensive products, skipping the first 2.

**Expected Output**: product_name, unit_price (positions 3-7 by price)

**Constraints**: 
- PostgreSQL: `LIMIT 5 OFFSET 2`
- SQL Server: `OFFSET 2 ROWS FETCH NEXT 5 ROWS ONLY`

---

## Section 2: Aggregations, GROUP BY, HAVING (Q16-30)

---

### Q16. COUNT All Rows

🟢 **Difficulty**: Beginner  
**Skill**: COUNT(*) function

**Problem**: Count the total number of customers in the database.

**Expected Output**:
| total_customers |
|-----------------|
| 500 |

**Constraints**: None

---

### Q17. COUNT with Column

🟢 **Difficulty**: Beginner  
**Skill**: COUNT(column) vs COUNT(*)

**Problem**: Count how many customers have a phone number (non-NULL).

**Expected Output**: Single number representing count.

**Constraints**: COUNT(column) ignores NULLs.

---

### Q18. SUM Function

🟢 **Difficulty**: Beginner  
**Skill**: SUM aggregation

**Problem**: Calculate the total of all `unit_price` values from the `order_items` table.

**Expected Output**:
| total_sales |
|-------------|
| ... |

**Constraints**: Handle potential large numbers.

---

### Q19. AVG Function

🟢 **Difficulty**: Beginner  
**Skill**: AVG aggregation

**Problem**: Find the average `unit_price` of all products.

**Expected Output**: Rounded to 2 decimal places.

**Constraints**: AVG ignores NULL values.

---

### Q20. MIN and MAX

🟢 **Difficulty**: Beginner  
**Skill**: MIN, MAX functions

**Problem**: Find the earliest and latest `order_date` from the orders table.

**Expected Output**:
| earliest_order | latest_order |
|----------------|--------------|
| 2023-01-01 | 2024-12-22 |

**Constraints**: Works with dates.

---

### Q21. GROUP BY Single Column

🟢 **Difficulty**: Beginner  
**Skill**: GROUP BY clause

**Problem**: Count the number of customers in each `tier`.

**Expected Output**:
| tier | customer_count |
|------|----------------|
| Bronze | 200 |
| Silver | 150 |
| ... | ... |

**Constraints**: Non-aggregated columns must be in GROUP BY.

---

### Q22. GROUP BY Multiple Columns

🟢 **Difficulty**: Beginner  
**Skill**: Multi-column grouping

**Problem**: Count customers by `country` and `tier` combination.

**Expected Output**:
| country | tier | customer_count |
|---------|------|----------------|
| USA | Gold | 45 |
| ... | ... | ... |

**Constraints**: Order by country, then tier.

---

### Q23. GROUP BY with SUM

🟢 **Difficulty**: Beginner  
**Skill**: Aggregation with grouping

**Problem**: Calculate total revenue (sum of `quantity * unit_price * (1 - discount)`) per `order_id` from `order_items`.

**Expected Output**:
| order_id | order_total |
|----------|-------------|
| 1 | 523.45 |

**Constraints**: Account for discount in calculation.

---

### Q24. GROUP BY with AVG

🟢 **Difficulty**: Beginner  
**Skill**: Average per group

**Problem**: Find the average product price per `category_id`.

**Expected Output**:
| category_id | avg_price |
|-------------|-----------|
| 1 | 45.99 |

**Constraints**: Round to 2 decimal places.

---

### Q25. HAVING Clause Basics

🟢 **Difficulty**: Beginner  
**Skill**: Filtering groups with HAVING

**Problem**: Find categories that have more than 10 products.

**Expected Output**:
| category_id | product_count |
|-------------|---------------|
| ... | ... |

**Constraints**: HAVING filters after GROUP BY; WHERE filters before.

---

### Q26. HAVING with Multiple Conditions

🟢 **Difficulty**: Beginner  
**Skill**: Complex HAVING filters

**Problem**: Find customer tiers where the count is between 50 and 200.

**Expected Output**:
| tier | count |
|------|-------|
| ... | ... |

**Constraints**: Use HAVING with BETWEEN or compound conditions.

---

### Q27. Combining WHERE and HAVING

🟢 **Difficulty**: Beginner  
**Skill**: WHERE vs HAVING

**Problem**: For active products only (`is_active = TRUE`), find categories where average price exceeds 75.

**Expected Output**:
| category_id | avg_price |
|-------------|-----------|
| ... | ... |

**Constraints**: WHERE filters rows before grouping; HAVING filters groups after.

---

### Q28. COUNT DISTINCT

🟢 **Difficulty**: Beginner  
**Skill**: COUNT(DISTINCT column)

**Problem**: Count how many distinct countries have customers.

**Expected Output**: Single number.

**Constraints**: Removes duplicates before counting.

---

### Q29. Aggregate with Expression

🟢 **Difficulty**: Beginner  
**Skill**: Aggregation on calculated columns

**Problem**: Calculate the total profit margin (`SUM(unit_price - cost_price)`) for all products.

**Expected Output**:
| total_margin |
|--------------|
| ... |

**Constraints**: Handle NULL cost_price (treat as 0 or exclude).

---

### Q30. Finding Extremes per Group

🟢 **Difficulty**: Beginner  
**Skill**: MIN/MAX with GROUP BY

**Problem**: Find the cheapest and most expensive product in each category.

**Expected Output**:
| category_id | min_price | max_price |
|-------------|-----------|-----------|
| 1 | 9.99 | 299.99 |

**Constraints**: One row per category.

---

## Section 3: Basic Joins (Q31-45)

---

### Q31. INNER JOIN Basics

🟢 **Difficulty**: Beginner  
**Skill**: INNER JOIN

**Problem**: List all orders with customer names (first_name, last_name) and order_date.

**Expected Output**:
| order_id | first_name | last_name | order_date |
|----------|------------|-----------|------------|
| ... | ... | ... | ... |

**Constraints**: Only orders with valid customer_id (excludes NULLs).

---

### Q32. INNER JOIN with Filter

🟢 **Difficulty**: Beginner  
**Skill**: JOIN with WHERE

**Problem**: Find all orders placed by customers in the 'Gold' tier.

**Expected Output**: order_id, customer first/last name, tier, order_date

**Constraints**: Filter applies to joined result.

---

### Q33. Three-Table JOIN

🟢 **Difficulty**: Beginner  
**Skill**: Multiple INNER JOINs

**Problem**: List product names, their category names, and order quantities from order_items.

**Expected Output**:
| product_name | category_name | quantity |
|--------------|---------------|----------|
| ... | ... | ... |

**Constraints**: Join products → categories and products → order_items.

---

### Q34. LEFT JOIN Basics

🟢 **Difficulty**: Beginner  
**Skill**: LEFT OUTER JOIN

**Problem**: List ALL customers with their orders (if any). Include customers who have never ordered.

**Expected Output**:
| customer_id | first_name | order_id | order_date |
|-------------|------------|----------|------------|
| 1 | John | 101 | 2024-01-15 |
| 2 | Jane | NULL | NULL |

**Constraints**: Unmatched customers show NULL for order columns.

---

### Q35. LEFT JOIN to Find Missing

🟢 **Difficulty**: Beginner  
**Skill**: LEFT JOIN with IS NULL

**Problem**: Find all products that have never been ordered.

**Expected Output**: product_id, product_name

**Constraints**: Use `WHERE order_items.item_id IS NULL`.

---

### Q36. RIGHT JOIN

🟢 **Difficulty**: Beginner  
**Skill**: RIGHT OUTER JOIN

**Problem**: List all products with their inventory quantities. Include products without inventory records.

**Expected Output**:
| product_id | product_name | quantity |
|------------|--------------|----------|
| ... | ... | ... |

**Constraints**: RIGHT JOIN or reverse the LEFT JOIN logic.

---

### Q37. JOIN with Aggregation

🟢 **Difficulty**: Beginner  
**Skill**: Combining JOIN and GROUP BY

**Problem**: Count the number of orders per customer.

**Expected Output**:
| customer_id | first_name | order_count |
|-------------|------------|-------------|
| ... | ... | ... |

**Constraints**: Include customers with 0 orders (use LEFT JOIN).

---

### Q38. JOIN with Multiple Conditions

🟢 **Difficulty**: Beginner  
**Skill**: JOIN ON with AND

**Problem**: Find orders handled by employees in the 'Sales' department for 'Gold' tier customers.

**Expected Output**: order_id, customer name, employee name, department

**Constraints**: Join conditions on both customer tier and employee department.

---

### Q39. Table Aliases in JOINs

🟢 **Difficulty**: Beginner  
**Skill**: Using aliases for readability

**Problem**: Rewrite Q31 using table aliases (c for customers, o for orders).

**Expected Output**: Same as Q31.

**Constraints**: Use short, meaningful aliases.

---

### Q40. JOIN with ORDER BY

🟢 **Difficulty**: Beginner  
**Skill**: Sorting joined results

**Problem**: List all orders with customer and product details, sorted by order_date descending, then product_name ascending.

**Expected Output**: order_id, order_date, first_name, product_name

**Constraints**: Multi-column sort on joined data.

---

### Q41. FULL OUTER JOIN

🟢 **Difficulty**: Beginner  
**Skill**: FULL OUTER JOIN

**Problem**: Show all products and all inventory records, matching where possible.

**Expected Output**:
| product_id | product_name | inventory_id | quantity |
|------------|--------------|--------------|----------|
| ... | ... | ... | ... |

**Constraints**: 
- MySQL doesn't support FULL OUTER JOIN directly (use UNION of LEFT and RIGHT)
- PostgreSQL/SQL Server support it natively.

---

### Q42. JOIN vs Subquery Equivalence

🟢 **Difficulty**: Beginner  
**Skill**: Understanding JOIN alternatives

**Problem**: Find customers who have placed orders. Write using: (a) INNER JOIN, (b) EXISTS subquery.

**Expected Output**: customer_id, first_name, last_name (same for both approaches)

**Constraints**: Demonstrate equivalence.

---

### Q43. Natural JOIN (Awareness)

🟢 **Difficulty**: Beginner  
**Skill**: NATURAL JOIN caveat

**Problem**: Explain why the following query might give unexpected results, then write the correct version:
```sql
SELECT * FROM orders NATURAL JOIN customers;
```

**Expected Output**: Explanation + corrected explicit JOIN.

**Constraints**: NATURAL JOIN matches ALL same-named columns (dangerous).

---

### Q44. CROSS JOIN

🟢 **Difficulty**: Beginner  
**Skill**: Cartesian product

**Problem**: Generate all possible product-category combinations (even invalid ones) for a report matrix.

**Expected Output**: product_name, category_name (all combinations)

**Constraints**: Result size = |products| × |categories|. Use sparingly.

---

### Q45. JOIN with CASE Expression

🟢 **Difficulty**: Beginner  
**Skill**: CASE in SELECT with JOIN

**Problem**: List orders with a status label: 'Urgent' if Pending, 'In Progress' if Processing/Shipped, 'Complete' otherwise.

**Expected Output**:
| order_id | status | status_label |
|----------|--------|--------------|
| 1 | Pending | Urgent |

**Constraints**: Use CASE WHEN inside SELECT.

---

## Section 4: Basic DML Operations (Q46-50)

---

### Q46. INSERT Single Row

🟢 **Difficulty**: Beginner  
**Skill**: INSERT statement

**Problem**: Insert a new customer with the following details:
- first_name: 'Alice'
- last_name: 'Smith'  
- email: 'alice.smith@example.com'
- city: 'Boston'
- tier: 'Silver'

**Expected Output**: Statement confirmation, new row visible in SELECT.

**Constraints**: Provide all required columns (NOT NULL).

---

### Q47. INSERT Multiple Rows

🟢 **Difficulty**: Beginner  
**Skill**: Multi-row INSERT

**Problem**: Insert 3 new categories in a single statement:
- 'Outdoor', 'Sports', 'Seasonal'

**Expected Output**: 3 rows inserted.

**Constraints**: 
- PostgreSQL: `VALUES (...), (...), (...)`
- Some dialects require separate INSERTs.

---

### Q48. UPDATE with WHERE

🟢 **Difficulty**: Beginner  
**Skill**: UPDATE statement

**Problem**: Update all Bronze tier customers in 'USA' to Silver tier.

**Expected Output**: N rows updated.

**Constraints**: Always use WHERE to avoid updating all rows!

---

### Q49. DELETE with WHERE

🟢 **Difficulty**: Beginner  
**Skill**: DELETE statement

**Problem**: Delete all orders with status 'Cancelled' that are older than 1 year.

**Expected Output**: N rows deleted.

**Constraints**: 
- Use date arithmetic: `order_date < CURRENT_DATE - INTERVAL '1 year'`
- Be careful with cascading deletes (order_items).

---

### Q50. INSERT from SELECT

🟢 **Difficulty**: Beginner  
**Skill**: INSERT...SELECT

**Problem**: Create a new table `premium_customers` and populate it with all Gold and Platinum tier customers.

**Expected Output**: 
```sql
CREATE TABLE premium_customers AS SELECT ... 
-- or
INSERT INTO premium_customers SELECT ...
```

**Constraints**: Understand CREATE TABLE AS vs INSERT INTO...SELECT.

---

# Intermediate Level

## Section 5: Advanced Joins (Q51-65)

---

### Q51. Self JOIN

🟡 **Difficulty**: Intermediate  
**Skill**: Self-referencing JOIN

**Problem**: List all employees with their manager's name.

**Expected Output**:
| employee_id | employee_name | manager_name |
|-------------|---------------|--------------|
| 2 | Jane Doe | John Smith |
| 3 | Bob Wilson | John Smith |

**Constraints**: Use table aliases (e for employee, m for manager). Handle CEO (manager_id IS NULL).

---

### Q52. Self JOIN for Hierarchy

🟡 **Difficulty**: Intermediate  
**Skill**: Hierarchical data with self-join

**Problem**: Find all subcategories and their parent category names.

**Expected Output**:
| subcategory_id | subcategory_name | parent_name |
|----------------|------------------|-------------|
| 4 | Smartphones | Electronics |

**Constraints**: categories.parent_id references categories.category_id.

---

### Q53. Anti-Join Pattern

🟡 **Difficulty**: Intermediate  
**Skill**: Anti-join (finding non-matching rows)

**Problem**: Find all employees who have never processed any order.

**Expected Output**: employee_id, first_name, last_name

**Constraints**: 
- Method 1: LEFT JOIN + IS NULL
- Method 2: NOT EXISTS
- Method 3: NOT IN (beware of NULLs!)

---

### Q54. Semi-Join Pattern

🟡 **Difficulty**: Intermediate  
**Skill**: Semi-join (existence check)

**Problem**: Find all customers who have at least one order with status 'Delivered'.

**Expected Output**: customer_id, first_name, last_name (no duplicates)

**Constraints**: 
- Method 1: EXISTS subquery
- Method 2: IN subquery
- Avoid: JOIN with DISTINCT (less efficient)

---

### Q55. Multiple Anti-Joins

🟡 **Difficulty**: Intermediate  
**Skill**: Complex exclusion patterns

**Problem**: Find products that have never been ordered AND have inventory quantity = 0.

**Expected Output**: product_id, product_name

**Constraints**: Combine anti-join with regular filter.

---

### Q56. Inequality Join

🟡 **Difficulty**: Intermediate  
**Skill**: Non-equi joins

**Problem**: Find all pairs of products where one is more expensive than the other (within same category).

**Expected Output**:
| cheap_product | expensive_product | price_diff |
|---------------|-------------------|------------|
| Widget A | Widget Pro | 50.00 |

**Constraints**: Use `p1.unit_price < p2.unit_price` in JOIN condition. Avoid duplicates.

---

### Q57. Range Join

🟡 **Difficulty**: Intermediate  
**Skill**: BETWEEN in JOIN

**Problem**: Match each order to a "shipping tier" based on order total:
- Tier 1: $0-50, Tier 2: $51-200, Tier 3: $201+

Given a `shipping_tiers` table with (tier_id, min_amount, max_amount).

**Expected Output**: order_id, order_total, tier_id

**Constraints**: Use `JOIN shipping_tiers ON total BETWEEN min AND max`.

---

### Q58. Exclusive Join (XOR)

🟡 **Difficulty**: Intermediate  
**Skill**: FULL OUTER JOIN with exclusion

**Problem**: Find products that exist in products table OR inventory table, but NOT both.

**Expected Output**: Items with mismatched records.

**Constraints**: 
```sql
WHERE p.product_id IS NULL OR i.product_id IS NULL
```

---

### Q59. Lateral Join Concept

🟡 **Difficulty**: Intermediate  
**Skill**: LATERAL join (PostgreSQL) / CROSS APPLY (SQL Server)

**Problem**: For each customer, find their 3 most recent orders.

**Expected Output**:
| customer_id | first_name | order_id | order_date |
|-------------|------------|----------|------------|
| 1 | John | 500 | 2024-12-01 |
| 1 | John | 495 | 2024-11-15 |

**Constraints**: 
- PostgreSQL: `CROSS JOIN LATERAL (SELECT ... LIMIT 3)`
- SQL Server: `CROSS APPLY`
- MySQL: Correlated subquery or window function alternative

---

### Q60. Multiple JOIN Types Combined

🟡 **Difficulty**: Intermediate  
**Skill**: Mixing INNER and OUTER joins

**Problem**: List all products with their category (required) and inventory (optional).

**Expected Output**: product_name, category_name, quantity (NULL if no inventory)

**Constraints**: Be careful with join order when mixing types.

---

### Q61. Self Comparison

🟡 **Difficulty**: Intermediate  
**Skill**: Finding duplicates with self-join

**Problem**: Find customers with duplicate emails (same email, different customer_id).

**Expected Output**: c1.customer_id, c2.customer_id, email

**Constraints**: Avoid matching row to itself (`c1.customer_id < c2.customer_id`).

---

### Q62. Multi-Table Outer Join

🟡 **Difficulty**: Intermediate  
**Skill**: Chained LEFT JOINs

**Problem**: List all customers with their orders, and for each order, the payment (if any).

**Expected Output**: customer_name, order_id, order_date, payment_id, amount

**Constraints**: Preserve all customers, even those without orders or payments.

---

### Q63. Join with Aggregation Filter

🟡 **Difficulty**: Intermediate  
**Skill**: HAVING on joined aggregates

**Problem**: Find customers whose total order value exceeds $1000.

**Expected Output**:
| customer_id | first_name | total_spent |
|-------------|------------|-------------|
| ... | ... | ... |

**Constraints**: Use JOIN + GROUP BY + HAVING.

---

### Q64. Conditional Aggregation in Join

🟡 **Difficulty**: Intermediate  
**Skill**: CASE inside aggregate with JOIN

**Problem**: For each category, count active and inactive products separately.

**Expected Output**:
| category_name | active_count | inactive_count |
|---------------|--------------|----------------|
| Electronics | 25 | 5 |

**Constraints**: Use `SUM(CASE WHEN is_active THEN 1 ELSE 0 END)`.

---

### Q65. Date-Based Join

🟡 **Difficulty**: Intermediate  
**Skill**: Joining on date ranges

**Problem**: Find all orders placed within 7 days of a customer's registration.

**Expected Output**: customer_id, registration_date, order_id, order_date, days_since_registration

**Constraints**: Use date arithmetic in JOIN condition.

---

## Section 6: Subqueries and CTEs (Q66-80)

---

### Q66. Scalar Subquery

🟡 **Difficulty**: Intermediate  
**Skill**: Single-value subquery

**Problem**: Find all products priced above the average product price.

**Expected Output**: product_name, unit_price, (avg_price for reference)

**Constraints**: Subquery returns single value.

---

### Q67. Subquery in WHERE with IN

🟡 **Difficulty**: Intermediate  
**Skill**: IN with subquery

**Problem**: Find all orders placed by customers from 'USA'.

**Expected Output**: order_id, order_date, customer_id

**Constraints**: Use `WHERE customer_id IN (SELECT ... FROM customers WHERE country = 'USA')`.

---

### Q68. Correlated Subquery

🟡 **Difficulty**: Intermediate  
**Skill**: Subquery referencing outer query

**Problem**: Find products whose price is above the average price for their category.

**Expected Output**: product_name, unit_price, category_id

**Constraints**: Subquery references `p.category_id` from outer query.

---

### Q69. EXISTS vs IN

🟡 **Difficulty**: Intermediate  
**Skill**: EXISTS subquery

**Problem**: Rewrite Q67 using EXISTS instead of IN. Compare performance considerations.

**Expected Output**: Same as Q67.

**Constraints**: 
- EXISTS: Better when subquery has many rows
- IN: Better when subquery result is small

---

### Q70. NOT EXISTS

🟡 **Difficulty**: Intermediate  
**Skill**: Negated existence check

**Problem**: Find categories that have no products.

**Expected Output**: category_id, category_name

**Constraints**: Use `WHERE NOT EXISTS (SELECT 1 FROM products WHERE ...)`.

---

### Q71. Subquery in SELECT

🟡 **Difficulty**: Intermediate  
**Skill**: Scalar subquery in column list

**Problem**: For each order, show total item count alongside order details.

**Expected Output**:
| order_id | order_date | total_items |
|----------|------------|-------------|
| 1 | 2024-01-15 | 3 |

**Constraints**: Subquery in SELECT must return single value per row.

---

### Q72. Subquery in FROM (Derived Table)

🟡 **Difficulty**: Intermediate  
**Skill**: Inline view / derived table

**Problem**: Find the top 5 customers by order count, then show their tier distribution.

**Expected Output**:
| tier | top_customer_count |
|------|-------------------|
| Gold | 3 |
| Platinum | 2 |

**Constraints**: First aggregate in subquery, then aggregate again.

---

### Q73. Basic CTE

🟡 **Difficulty**: Intermediate  
**Skill**: Common Table Expression

**Problem**: Rewrite Q66 using a CTE to calculate the average price.

**Expected Output**: Same as Q66.

**Constraints**: 
```sql
WITH avg_prices AS (SELECT AVG(unit_price) as avg_price FROM products)
SELECT ... FROM products, avg_prices WHERE ...
```

---

### Q74. Multiple CTEs

🟡 **Difficulty**: Intermediate  
**Skill**: Chained CTEs

**Problem**: Find customers who have ordered more than the average order count AND spent more than the average total.

**Expected Output**: customer_id, first_name, order_count, total_spent

**Constraints**: Define separate CTEs for order counts and totals, then join.

---

### Q75. CTE for Readability

🟡 **Difficulty**: Intermediate  
**Skill**: Refactoring complex queries

**Problem**: Rewrite this nested query using CTEs for clarity:
```sql
SELECT * FROM (SELECT * FROM (SELECT customer_id, SUM(amount) as total 
FROM orders o JOIN payments p ON o.order_id = p.order_id 
GROUP BY customer_id) x WHERE total > 1000) y WHERE ...
```

**Expected Output**: Equivalent result, readable query.

**Constraints**: Each logical step becomes a named CTE.

---

### Q76. CTE with INSERT

🟡 **Difficulty**: Intermediate  
**Skill**: CTE in DML statement

**Problem**: Insert into an `archived_orders` table all orders older than 2 years, using a CTE to identify them.

**Expected Output**: N rows inserted.

**Constraints**: PostgreSQL/SQL Server support CTE with INSERT.

---

### Q77. ALL/ANY Operators

🟡 **Difficulty**: Intermediate  
**Skill**: Comparison with subquery results

**Problem**: Find products that are more expensive than ALL products in category 1.

**Expected Output**: product_id, product_name, unit_price

**Constraints**: 
- `> ALL (...)` = greater than maximum
- `> ANY (...)` = greater than minimum

---

### Q78. Multi-Level Subquery

🟡 **Difficulty**: Intermediate  
**Skill**: Nested subqueries

**Problem**: Find employees who manage employees who have processed orders.

**Expected Output**: manager_id, manager_name

**Constraints**: 3 levels: employees → employees → orders.

---

### Q79. Subquery vs JOIN Performance

🟡 **Difficulty**: Intermediate  
**Skill**: Query optimization awareness

**Problem**: Write two versions of "find all orders with product 'Widget A'":
1. Using JOIN
2. Using subquery

Explain when each is preferable.

**Expected Output**: Both queries + explanation.

**Constraints**: Consider query optimizer behavior.

---

### Q80. Correlated UPDATE

🟡 **Difficulty**: Intermediate  
**Skill**: UPDATE with subquery

**Problem**: Update each product's `updated_at` to the date of its most recent order.

**Expected Output**: N rows updated.

**Constraints**: 
```sql
UPDATE products p SET updated_at = (
  SELECT MAX(o.order_date) FROM orders o 
  JOIN order_items oi ON ... 
  WHERE oi.product_id = p.product_id
);
```

---

## Section 7: Set Operations (Q81-90)

---

### Q81. UNION Basics

🟡 **Difficulty**: Intermediate  
**Skill**: UNION operator

**Problem**: Combine a list of customer emails and employee emails into a single list.

**Expected Output**: Single column of all unique emails.

**Constraints**: UNION removes duplicates by default.

---

### Q82. UNION ALL

🟡 **Difficulty**: Intermediate  
**Skill**: UNION ALL (preserve duplicates)

**Problem**: Same as Q81, but preserve duplicates (if any email appears in both tables).

**Expected Output**: All emails, including duplicates.

**Constraints**: UNION ALL is faster (no deduplication).

---

### Q83. UNION with Different Columns

🟡 **Difficulty**: Intermediate  
**Skill**: Column alignment in UNION

**Problem**: Create a combined "contact list" showing:
- Customers as 'Customer' type with their name
- Employees as 'Employee' type with their name

**Expected Output**:
| contact_type | full_name |
|--------------|-----------|
| Customer | John Doe |
| Employee | Jane Smith |

**Constraints**: Columns must match in number and compatible types.

---

### Q84. INTERSECT

🟡 **Difficulty**: Intermediate  
**Skill**: INTERSECT operator

**Problem**: Find email domains that appear in both customers and employees tables.

**Expected Output**: List of common domains.

**Constraints**: 
- MySQL doesn't support INTERSECT (use INNER JOIN alternative)
- PostgreSQL/SQL Server support natively

---

### Q85. EXCEPT / MINUS

🟡 **Difficulty**: Intermediate  
**Skill**: EXCEPT operator

**Problem**: Find product IDs that exist in products table but NOT in order_items (never ordered).

**Expected Output**: product_id list

**Constraints**: 
- PostgreSQL: EXCEPT
- Oracle: MINUS
- MySQL: Use LEFT JOIN with NULL check

---

### Q86. Set Operations with ORDER BY

🟡 **Difficulty**: Intermediate  
**Skill**: Sorting combined results

**Problem**: Combine customer and employee names, sorted alphabetically.

**Expected Output**: Sorted combined list.

**Constraints**: ORDER BY applies to final result; place at end.

---

### Q87. UNION with Aggregates

🟡 **Difficulty**: Intermediate  
**Skill**: Aggregating before UNION

**Problem**: Show total orders per month from 2023 and 2024 as separate "year" records.

**Expected Output**:
| year | month | order_count |
|------|-------|-------------|
| 2023 | 1 | 45 |
| 2024 | 1 | 62 |

**Constraints**: Aggregate in each SELECT before UNION.

---

### Q88. Set Operations for Data Validation

🟡 **Difficulty**: Intermediate  
**Skill**: Finding data discrepancies

**Problem**: Find order_ids in payments that don't exist in orders table (orphaned payments).

**Expected Output**: List of orphaned payment order_ids.

**Constraints**: Use EXCEPT or LEFT JOIN with NULL.

---

### Q89. Complex Set Logic

🟡 **Difficulty**: Intermediate  
**Skill**: Combining multiple set operations

**Problem**: Find customers who have ordered AND made payments, but have NOT cancelled any order.

**Expected Output**: customer_id, first_name

**Constraints**: Combine INTERSECT and EXCEPT logic.

---

### Q90. UNION for Pivoting

🟡 **Difficulty**: Intermediate  
**Skill**: UNION for row transformation

**Problem**: Transform product prices into rows showing "High" (>100), "Medium" (50-100), "Low" (<50) price tiers with counts.

**Expected Output**:
| tier | count |
|------|-------|
| High | 25 |
| Medium | 45 |
| Low | 30 |

**Constraints**: Use UNION of three SELECT statements with different filters.

---

## Section 8: Date/Time, Strings, Regex, NULL Logic (Q91-110)

---

### Q91. Current Date/Time

🟡 **Difficulty**: Intermediate  
**Skill**: Date/time functions

**Problem**: Display current date, current timestamp, and current time separately.

**Expected Output**: Three columns with current values.

**Constraints**: 
- PostgreSQL: `CURRENT_DATE`, `CURRENT_TIMESTAMP`, `CURRENT_TIME`
- MySQL: `CURDATE()`, `NOW()`, `CURTIME()`
- SQL Server: `GETDATE()`

---

### Q92. Date Extraction

🟡 **Difficulty**: Intermediate  
**Skill**: EXTRACT / DATEPART

**Problem**: Extract year, month, and day from order_date for all orders.

**Expected Output**:
| order_id | order_year | order_month | order_day |
|----------|------------|-------------|-----------|
| 1 | 2024 | 3 | 15 |

**Constraints**: 
- PostgreSQL: `EXTRACT(YEAR FROM order_date)`
- MySQL: `YEAR(order_date)`
- SQL Server: `DATEPART(year, order_date)`

---

### Q93. Date Arithmetic

🟡 **Difficulty**: Intermediate  
**Skill**: Adding/subtracting dates

**Problem**: Find orders placed in the last 30 days.

**Expected Output**: All recent orders.

**Constraints**: 
- PostgreSQL: `order_date > CURRENT_DATE - INTERVAL '30 days'`
- MySQL: `order_date > DATE_SUB(CURDATE(), INTERVAL 30 DAY)`
- SQL Server: `order_date > DATEADD(day, -30, GETDATE())`

---

### Q94. Date Difference

🟡 **Difficulty**: Intermediate  
**Skill**: Calculating date intervals

**Problem**: Calculate days between order_date and shipped_date for each order.

**Expected Output**: order_id, order_date, shipped_date, days_to_ship

**Constraints**: 
- PostgreSQL: `shipped_date - order_date` (returns integer days)
- MySQL: `DATEDIFF(shipped_date, order_date)`
- SQL Server: `DATEDIFF(day, order_date, shipped_date)`

---

### Q95. Date Truncation

🟡 **Difficulty**: Intermediate  
**Skill**: DATE_TRUNC / Date truncation

**Problem**: Group orders by month (truncate to first of month).

**Expected Output**:
| order_month | order_count |
|-------------|-------------|
| 2024-01-01 | 150 |

**Constraints**: 
- PostgreSQL: `DATE_TRUNC('month', order_date)`
- MySQL: `DATE_FORMAT(order_date, '%Y-%m-01')`

---

### Q96. Date Formatting

🟡 **Difficulty**: Intermediate  
**Skill**: TO_CHAR / DATE_FORMAT

**Problem**: Display order dates in format 'Mon DD, YYYY' (e.g., 'Dec 22, 2024').

**Expected Output**: Formatted date strings.

**Constraints**: 
- PostgreSQL: `TO_CHAR(order_date, 'Mon DD, YYYY')`
- MySQL: `DATE_FORMAT(order_date, '%b %d, %Y')`

---

### Q97. String Concatenation

🟡 **Difficulty**: Intermediate  
**Skill**: String concatenation

**Problem**: Create a full name column combining first_name and last_name.

**Expected Output**: full_name

**Constraints**: 
- PostgreSQL: `first_name || ' ' || last_name`
- MySQL: `CONCAT(first_name, ' ', last_name)`
- SQL Server: `first_name + ' ' + last_name`

---

### Q98. String Functions

🟡 **Difficulty**: Intermediate  
**Skill**: UPPER, LOWER, LENGTH, TRIM

**Problem**: Show customer emails in lowercase with their character length.

**Expected Output**:
| email | email_length |
|-------|--------------|
| john@email.com | 14 |

**Constraints**: Use LOWER() and LENGTH()/LEN().

---

### Q99. Substring Operations

🟡 **Difficulty**: Intermediate  
**Skill**: SUBSTRING / SUBSTR

**Problem**: Extract the domain from customer emails (after @).

**Expected Output**:
| email | domain |
|-------|--------|
| john@gmail.com | gmail.com |

**Constraints**: 
- Use `SUBSTRING(email FROM POSITION('@' IN email) + 1)`
- Or: `SUBSTRING(email, POSITION('@' IN email) + 1)`

---

### Q100. Pattern Matching with LIKE

🟡 **Difficulty**: Intermediate  
**Skill**: LIKE patterns

**Problem**: Find all products whose name starts with 'Pro' and ends with 'Plus'.

**Expected Output**: product_name list

**Constraints**: 
- `%` = any characters
- `_` = single character
- Pattern: `'Pro%Plus'`

---

### Q101. SIMILAR TO / REGEXP

🟡 **Difficulty**: Intermediate  
**Skill**: Regex pattern matching

**Problem**: Find customers whose phone matches pattern: 3 digits - 3 digits - 4 digits.

**Expected Output**: Matching phone numbers.

**Constraints**: 
- PostgreSQL: `phone ~ '^\d{3}-\d{3}-\d{4}$'`
- MySQL: `phone REGEXP '^[0-9]{3}-[0-9]{3}-[0-9]{4}$'`

---

### Q102. String Replacement

🟡 **Difficulty**: Intermediate  
**Skill**: REPLACE function

**Problem**: Replace all occurrences of 'Inc.' with 'Incorporated' in product descriptions.

**Expected Output**: Updated descriptions (SELECT, not UPDATE).

**Constraints**: REPLACE(string, from, to)

---

### Q103. COALESCE for NULL Handling

🟡 **Difficulty**: Intermediate  
**Skill**: COALESCE function

**Problem**: Show product cost_price, using 0 if NULL.

**Expected Output**:
| product_name | cost_price |
|--------------|------------|
| Widget A | 15.00 |
| Widget B | 0 |

**Constraints**: `COALESCE(cost_price, 0)`

---

### Q104. NULLIF Function

🟡 **Difficulty**: Intermediate  
**Skill**: NULLIF for conditional NULL

**Problem**: Calculate price per unit, avoiding division by zero. If quantity is 0, return NULL.

**Expected Output**: Uses `NULLIF(quantity, 0)` in denominator.

**Constraints**: Prevents division by zero error.

---

### Q105. NULL in Comparisons

🟡 **Difficulty**: Intermediate  
**Skill**: NULL comparison gotchas

**Problem**: Find all products where cost_price is unknown (NULL).

**Expected Output**: Products with NULL cost_price.

**Constraints**: 
- ❌ `WHERE cost_price = NULL` (never true)
- ✅ `WHERE cost_price IS NULL`

---

### Q106. NULL in Aggregates

🟡 **Difficulty**: Intermediate  
**Skill**: NULL behavior in aggregations

**Problem**: Compare COUNT(*), COUNT(cost_price), and COUNT(DISTINCT cost_price).

**Expected Output**: Three different counts with explanation.

**Constraints**: 
- COUNT(*) counts all rows
- COUNT(column) ignores NULLs
- COUNT(DISTINCT column) counts unique non-NULLs

---

### Q107. NULL in Boolean Logic

🟡 **Difficulty**: Intermediate  
**Skill**: Three-valued logic

**Problem**: Explain the result of: `SELECT * FROM products WHERE NOT (is_active = FALSE)`

**Expected Output**: Explanation + correct query for "not inactive products."

**Constraints**: NULL is_active won't match! Use `WHERE is_active IS DISTINCT FROM FALSE` or explicit NULL handling.

---

### Q108. CASE with NULL

🟡 **Difficulty**: Intermediate  
**Skill**: NULL in CASE expressions

**Problem**: Categorize products by cost status: 'Free' if 0, 'Priced' if > 0, 'Unknown' if NULL.

**Expected Output**:
| product_name | cost_status |
|--------------|-------------|
| Widget A | Priced |
| Sample | Unknown |

**Constraints**: Check NULL first in CASE, as NULL comparisons return unknown.

---

### Q109. NULL-Safe Equality

🟡 **Difficulty**: Intermediate  
**Skill**: IS NOT DISTINCT FROM

**Problem**: Find products where current cost_price equals previous cost_price, including NULL = NULL.

**Expected Output**: Products with unchanged cost.

**Constraints**: 
- PostgreSQL: `IS NOT DISTINCT FROM`
- MySQL: `<=>`
- SQL Server: Use ISNULL or COALESCE

---

### Q110. Combining NULL Logic

🟡 **Difficulty**: Intermediate  
**Skill**: Complex NULL handling

**Problem**: Find orders where shipped_date is either NULL (not shipped) OR more than 7 days after order_date.

**Expected Output**: order_id, order_date, shipped_date, status

**Constraints**: Use OR with IS NULL check.

---

# Advanced Level

## Section 9: Window Functions (Q111-130)

---

### Q111. ROW_NUMBER Basics

🔴 **Difficulty**: Advanced  
**Skill**: ROW_NUMBER window function

**Problem**: Assign a unique sequential number to each order, ordered by order_date.

**Expected Output**:
| row_num | order_id | order_date |
|---------|----------|------------|
| 1 | 15 | 2023-01-01 |
| 2 | 23 | 2023-01-02 |

**Constraints**: `ROW_NUMBER() OVER (ORDER BY order_date)`

---

### Q112. ROW_NUMBER with PARTITION

🔴 **Difficulty**: Advanced  
**Skill**: Partitioned row numbering

**Problem**: For each customer, number their orders chronologically (1st order, 2nd order, etc.).

**Expected Output**:
| customer_id | order_num | order_id | order_date |
|-------------|-----------|----------|------------|
| 1 | 1 | 10 | 2023-01-15 |
| 1 | 2 | 45 | 2023-03-20 |
| 2 | 1 | 12 | 2023-01-18 |

**Constraints**: `ROW_NUMBER() OVER (PARTITION BY customer_id ORDER BY order_date)`

---

### Q113. RANK vs DENSE_RANK

🔴 **Difficulty**: Advanced  
**Skill**: Ranking functions

**Problem**: Rank products by unit_price. Show difference between RANK and DENSE_RANK when ties exist.

**Expected Output**:
| product_name | unit_price | rank | dense_rank |
|--------------|------------|------|------------|
| Product A | 100 | 1 | 1 |
| Product B | 100 | 1 | 1 |
| Product C | 90 | 3 | 2 |

**Constraints**: RANK skips numbers after ties; DENSE_RANK doesn't.

---

### Q114. NTILE for Quartiles

🔴 **Difficulty**: Advanced  
**Skill**: NTILE function

**Problem**: Divide customers into 4 equal groups (quartiles) based on their total spending.

**Expected Output**:
| customer_id | total_spent | spending_quartile |
|-------------|-------------|-------------------|
| 1 | 5000 | 1 |
| 2 | 2500 | 2 |

**Constraints**: `NTILE(4) OVER (ORDER BY total_spent DESC)`

---

### Q115. LAG Function

🔴 **Difficulty**: Advanced  
**Skill**: Accessing previous row

**Problem**: Show each order with the previous order's date and the days since last order.

**Expected Output**:
| order_id | order_date | prev_order_date | days_since_last |
|----------|------------|-----------------|-----------------|
| 1 | 2024-01-15 | NULL | NULL |
| 2 | 2024-01-20 | 2024-01-15 | 5 |

**Constraints**: `LAG(order_date, 1) OVER (ORDER BY order_date)`

---

### Q116. LEAD Function

🔴 **Difficulty**: Advanced  
**Skill**: Accessing next row

**Problem**: For each product, show the next higher priced product in the same category.

**Expected Output**: product_name, unit_price, next_product, next_price

**Constraints**: `LEAD(product_name) OVER (PARTITION BY category_id ORDER BY unit_price)`

---

### Q117. FIRST_VALUE and LAST_VALUE

🔴 **Difficulty**: Advanced  
**Skill**: First/last in partition

**Problem**: For each order, show the first and last product ordered (alphabetically).

**Expected Output**: order_id, first_product, last_product

**Constraints**: 
- FIRST_VALUE is straightforward
- LAST_VALUE needs frame: `ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING`

---

### Q118. Running Total

🔴 **Difficulty**: Advanced  
**Skill**: Cumulative SUM

**Problem**: Calculate a running total of sales by date.

**Expected Output**:
| order_date | daily_sales | running_total |
|------------|-------------|---------------|
| 2024-01-01 | 500 | 500 |
| 2024-01-02 | 300 | 800 |
| 2024-01-03 | 700 | 1500 |

**Constraints**: `SUM(daily_sales) OVER (ORDER BY order_date ROWS UNBOUNDED PRECEDING)`

---

### Q119. Moving Average

🔴 **Difficulty**: Advanced  
**Skill**: Window frames for averages

**Problem**: Calculate 7-day moving average of order counts.

**Expected Output**:
| order_date | daily_orders | moving_avg_7d |
|------------|--------------|---------------|
| 2024-01-07 | 15 | 12.5 |

**Constraints**: `AVG(daily_orders) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)`

---

### Q120. Percent of Total

🔴 **Difficulty**: Advanced  
**Skill**: Window for percentage calculations

**Problem**: Calculate each product's price as a percentage of total category price.

**Expected Output**:
| product_name | category_id | unit_price | pct_of_category |
|--------------|-------------|------------|-----------------|
| Widget A | 1 | 100 | 25.00% |

**Constraints**: `unit_price / SUM(unit_price) OVER (PARTITION BY category_id) * 100`

---

### Q121. Ranking Within Groups

🔴 **Difficulty**: Advanced  
**Skill**: Top N per group

**Problem**: Find the top 3 products by sales in each category.

**Expected Output**: category_name, product_name, total_sales, rank

**Constraints**: Use ROW_NUMBER or RANK with filter in outer query.

---

### Q122. Year-over-Year Comparison

🔴 **Difficulty**: Advanced  
**Skill**: LAG with PARTITION

**Problem**: Compare each month's sales to the same month last year.

**Expected Output**:
| year | month | sales | prev_year_sales | yoy_growth |
|------|-------|-------|-----------------|------------|
| 2024 | 1 | 10000 | 8000 | 25% |

**Constraints**: `LAG(sales, 12) OVER (ORDER BY year, month)`

---

### Q123. Cumulative Distribution

🔴 **Difficulty**: Advanced  
**Skill**: CUME_DIST function

**Problem**: Calculate what percentage of products are priced at or below each product's price.

**Expected Output**: product_name, unit_price, cumulative_pct

**Constraints**: `CUME_DIST() OVER (ORDER BY unit_price)` returns 0-1.

---

### Q124. PERCENT_RANK

🔴 **Difficulty**: Advanced  
**Skill**: Percentile ranking

**Problem**: Find products in the top 10% by price.

**Expected Output**: Products where PERCENT_RANK >= 0.9

**Constraints**: `PERCENT_RANK() OVER (ORDER BY unit_price)`

---

### Q125. Window with CASE

🔴 **Difficulty**: Advanced  
**Skill**: Conditional window aggregation

**Problem**: Calculate the running count of 'Delivered' orders vs total orders.

**Expected Output**: order_date, delivered_count, total_count, delivery_rate

**Constraints**: `SUM(CASE WHEN status = 'Delivered' THEN 1 ELSE 0 END) OVER (...)`

---

### Q126. Gap Detection

🔴 **Difficulty**: Advanced  
**Skill**: Finding gaps in sequences

**Problem**: Find gaps in order_id sequence (missing order numbers).

**Expected Output**: gap_start, gap_end

**Constraints**: Use LAG to compare consecutive IDs.

---

### Q127. Island Detection

🔴 **Difficulty**: Advanced  
**Skill**: Identifying consecutive sequences

**Problem**: Identify consecutive days when orders were placed (order "islands").

**Expected Output**: island_start, island_end, consecutive_days

**Constraints**: Use difference between ROW_NUMBER and date to group islands.

---

### Q128. Frame Clause Deep Dive

🔴 **Difficulty**: Advanced  
**Skill**: ROWS vs RANGE

**Problem**: Explain the difference between these two queries:
```sql
SUM(x) OVER (ORDER BY date ROWS BETWEEN 1 PRECEDING AND 1 FOLLOWING)
SUM(x) OVER (ORDER BY date RANGE BETWEEN 1 PRECEDING AND 1 FOLLOWING)
```

**Expected Output**: Explanation with examples showing different results.

**Constraints**: ROWS = physical rows; RANGE = logical value range.

---

### Q129. Multiple Window Functions

🔴 **Difficulty**: Advanced  
**Skill**: Combining window functions

**Problem**: For each order, show: row number, rank by amount, running total, and comparison to previous order.

**Expected Output**: All four metrics in one query.

**Constraints**: Define window once with WINDOW clause or repeat in each function.

---

### Q130. Window Function with GROUP BY

🔴 **Difficulty**: Advanced  
**Skill**: Aggregation + windowing

**Problem**: For each category, show monthly sales AND the category's YTD running total.

**Expected Output**:
| category | month | monthly_sales | ytd_sales |
|----------|-------|---------------|-----------|
| Electronics | Jan | 5000 | 5000 |
| Electronics | Feb | 6000 | 11000 |

**Constraints**: GROUP BY first, then apply window function to aggregated results (use subquery or CTE).

---

## Section 10: Recursive CTEs (Q131-140)

---

### Q131. Basic Recursive CTE

🔴 **Difficulty**: Advanced  
**Skill**: Recursive CTE structure

**Problem**: Generate numbers 1 to 10 using recursive CTE.

**Expected Output**: Single column with numbers 1-10.

**Constraints**: 
```sql
WITH RECURSIVE nums AS (
  SELECT 1 as n
  UNION ALL
  SELECT n + 1 FROM nums WHERE n < 10
)
SELECT * FROM nums;
```

---

### Q132. Date Series Generation

🔴 **Difficulty**: Advanced  
**Skill**: Generating date ranges

**Problem**: Generate all dates between '2024-01-01' and '2024-01-31'.

**Expected Output**: 31 rows with dates.

**Constraints**: Useful for filling gaps in time series reports.

---

### Q133. Employee Hierarchy

🔴 **Difficulty**: Advanced  
**Skill**: Organizational tree traversal

**Problem**: Show the complete management chain for each employee (employee → manager → ... → CEO).

**Expected Output**:
| employee_id | employee_name | level | path |
|-------------|---------------|-------|------|
| 5 | John | 3 | CEO > VP > Manager > John |

**Constraints**: Recursive CTE with path concatenation.

---

### Q134. Category Tree

🔴 **Difficulty**: Advanced  
**Skill**: Hierarchical category traversal

**Problem**: List all categories with their full path (e.g., "Electronics > Phones > Smartphones").

**Expected Output**: category_id, category_name, full_path, depth

**Constraints**: Categories have parent_id for self-referencing.

---

### Q135. Bill of Materials

🔴 **Difficulty**: Advanced  
**Skill**: Explosion of nested components

**Problem**: Given a `components` table (product_id, component_id, quantity), find all parts needed to build product 1, including nested sub-components.

**Expected Output**: All component IDs with total quantities needed.

**Constraints**: Classic BOM explosion problem.

---

### Q136. Recursive Path Finding

🔴 **Difficulty**: Advanced  
**Skill**: Graph traversal

**Problem**: Given a `routes` table (from_city, to_city), find all possible paths from 'New York' to 'Los Angeles'.

**Expected Output**: All paths with intermediate cities.

**Constraints**: Handle cycle detection to prevent infinite loops.

---

### Q137. Level-Limited Recursion

🔴 **Difficulty**: Advanced  
**Skill**: Controlling recursion depth

**Problem**: Find all employees within 2 levels of a specific manager.

**Expected Output**: Employees at level 1 and level 2 only.

**Constraints**: Add level counter and filter in WHERE.

---

### Q138. Recursive Aggregation

🔴 **Difficulty**: Advanced  
**Skill**: Aggregating hierarchical data

**Problem**: Calculate total team size for each manager (including all nested reports).

**Expected Output**: manager_id, manager_name, total_reports

**Constraints**: Combine recursive CTE with aggregation.

---

### Q139. Detecting Cycles

🔴 **Difficulty**: Advanced  
**Skill**: Cycle detection in recursion

**Problem**: Find circular references in the employee manager hierarchy (if any).

**Expected Output**: List of employee_ids involved in cycles.

**Constraints**: 
- PostgreSQL: Use `CYCLE` clause
- Others: Track visited path as array

---

### Q140. Recursive String Parsing

🔴 **Difficulty**: Advanced  
**Skill**: String splitting with recursion

**Problem**: Split a comma-separated string '1,2,3,4,5' into rows.

**Expected Output**: 5 rows with individual values.

**Constraints**: 
- MySQL 8+: Use RECURSIVE CTE with SUBSTRING
- PostgreSQL: `string_to_array` is simpler, but show CTE approach

---

## Section 11: Data Modeling (Q141-150)

---

### Q141. Primary Key Design

🔴 **Difficulty**: Advanced  
**Skill**: Primary key selection

**Problem**: Discuss trade-offs between natural keys (e.g., email) vs surrogate keys (e.g., customer_id SERIAL). When would you use each?

**Expected Output**: Analysis with pros/cons table.

**Constraints**: Consider: uniqueness, stability, performance, foreign keys.

---

### Q142. Foreign Key Constraints

🔴 **Difficulty**: Advanced  
**Skill**: Referential integrity

**Problem**: Add a foreign key to `orders` table referencing `customers`, with appropriate ON DELETE behavior.

**Expected Output**: ALTER TABLE statement with explanation of CASCADE vs RESTRICT vs SET NULL.

**Constraints**: Choose behavior based on business rules.

---

### Q143. Check Constraints

🔴 **Difficulty**: Advanced  
**Skill**: Data validation at DB level

**Problem**: Add constraints to ensure:
1. unit_price >= 0
2. quantity > 0
3. discount is between 0 and 1

**Expected Output**: ALTER TABLE statements with CHECK constraints.

**Constraints**: Database-level validation vs application-level.

---

### Q144. Unique Constraints

🔴 **Difficulty**: Advanced  
**Skill**: UNIQUE constraint

**Problem**: Ensure no duplicate (order_id, product_id) combinations in order_items.

**Expected Output**: 
```sql
ALTER TABLE order_items ADD CONSTRAINT unique_order_product UNIQUE(order_id, product_id);
```

**Constraints**: Difference between UNIQUE and PRIMARY KEY.

---

### Q145. Normalization - 1NF

🔴 **Difficulty**: Advanced  
**Skill**: First Normal Form

**Problem**: This table violates 1NF. Normalize it:
```
orders: order_id, items (comma-separated product_ids)
```

**Expected Output**: Separate order_items table.

**Constraints**: 1NF requires atomic values.

---

### Q146. Normalization - 2NF/3NF

🔴 **Difficulty**: Advanced  
**Skill**: Eliminating partial/transitive dependencies

**Problem**: Normalize this table to 3NF:
```
order_details: order_id, product_id, product_name, category_name, quantity
```

**Expected Output**: Separate products and categories tables.

**Constraints**: 2NF eliminates partial dependencies; 3NF eliminates transitive dependencies.

---

### Q147. Denormalization Trade-offs

🔴 **Difficulty**: Advanced  
**Skill**: When to denormalize

**Problem**: When would you intentionally store redundant data? Give 2 examples with justification.

**Expected Output**: Real-world scenarios (e.g., reporting tables, caching totals).

**Constraints**: Balance between storage, consistency, and query performance.

---

### Q148. Index Design Basics

🔴 **Difficulty**: Advanced  
**Skill**: Creating indexes

**Problem**: Create indexes to optimize these queries:
1. `SELECT * FROM orders WHERE customer_id = ?`
2. `SELECT * FROM products WHERE category_id = ? AND is_active = TRUE`

**Expected Output**: CREATE INDEX statements.

**Constraints**: Consider column selectivity and query patterns.

---

### Q149. Composite Index Order

🔴 **Difficulty**: Advanced  
**Skill**: Multi-column index design

**Problem**: Explain why index order matters. Which index is better for the query `WHERE a = 1 AND b > 10`?
- INDEX(a, b)
- INDEX(b, a)

**Expected Output**: Explanation with query execution analysis.

**Constraints**: Leftmost prefix rule.

---

### Q150. Partial and Functional Indexes

🔴 **Difficulty**: Advanced  
**Skill**: Advanced index types

**Problem**: Create a partial index on orders for only 'Pending' status orders (PostgreSQL).

**Expected Output**: 
```sql
CREATE INDEX idx_pending ON orders(order_id) WHERE status = 'Pending';
```

**Constraints**: Reduces index size; PostgreSQL feature.

---

## Section 12: DDL Operations (Q151-160)

---

### Q151. CREATE TABLE with Constraints

🔴 **Difficulty**: Advanced  
**Skill**: Comprehensive DDL

**Problem**: Create a `reviews` table with:
- Primary key, foreign keys to customers and products
- Rating between 1-5
- Review text (optional)
- Created timestamp default to now
- Unique constraint on (customer_id, product_id)

**Expected Output**: Complete CREATE TABLE statement.

**Constraints**: Include all appropriate constraints inline.

---

### Q152. ALTER TABLE - Add Column

🔴 **Difficulty**: Advanced  
**Skill**: Schema modification

**Problem**: Add a `loyalty_points` column to customers with default 0.

**Expected Output**: ALTER TABLE statement.

**Constraints**: Consider impact on existing data.

---

### Q153. ALTER TABLE - Modify Column

🔴 **Difficulty**: Advanced  
**Skill**: Column type changes

**Problem**: Change `phone` column from VARCHAR(20) to VARCHAR(30).

**Expected Output**: 
- PostgreSQL: `ALTER TABLE customers ALTER COLUMN phone TYPE VARCHAR(30);`
- MySQL: `ALTER TABLE customers MODIFY phone VARCHAR(30);`

**Constraints**: Be cautious with type changes that might truncate data.

---

### Q154. DROP with Dependencies

🔴 **Difficulty**: Advanced  
**Skill**: Safe object deletion

**Problem**: Drop the `categories` table. What happens to products referencing it?

**Expected Output**: Discussion of CASCADE vs RESTRICT, and proper approach.

**Constraints**: Always check dependencies first.

---

### Q155. TRUNCATE vs DELETE

🔴 **Difficulty**: Advanced  
**Skill**: Data removal strategies

**Problem**: Compare TRUNCATE and DELETE for removing all rows. When to use each?

**Expected Output**: 
| Aspect | DELETE | TRUNCATE |
|--------|--------|----------|
| Speed | Slower | Faster |
| Rollback | Yes | Limited |
| Triggers | Fired | Not fired |
| WHERE clause | Allowed | Not allowed |

**Constraints**: Understand transaction behavior.

---

### Q156. View Creation

🔴 **Difficulty**: Advanced  
**Skill**: CREATE VIEW

**Problem**: Create a view `vw_order_summary` showing order_id, customer name, total amount, and status.

**Expected Output**: CREATE VIEW statement with joins.

**Constraints**: Views simplify complex queries but may impact performance.

---

### Q157. Materialized View

🔴 **Difficulty**: Advanced  
**Skill**: Materialized views

**Problem**: Create a materialized view for daily sales summary. Include refresh strategy.

**Expected Output**: 
```sql
CREATE MATERIALIZED VIEW mv_daily_sales AS SELECT ...;
REFRESH MATERIALIZED VIEW mv_daily_sales;
```

**Constraints**: PostgreSQL/Oracle feature; trade-off between freshness and speed.

---

### Q158. Sequence and Identity

🔴 **Difficulty**: Advanced  
**Skill**: Auto-incrementing values

**Problem**: Compare SERIAL (PostgreSQL), AUTO_INCREMENT (MySQL), and IDENTITY (SQL Server).

**Expected Output**: Syntax examples and behavioral differences.

**Constraints**: Understand gap behavior after rollbacks.

---

### Q159. Temporary Tables

🔴 **Difficulty**: Advanced  
**Skill**: Temp table creation and usage

**Problem**: Create a temporary table to store intermediate calculation results, use it, then clean up.

**Expected Output**: Complete workflow with temp table.

**Constraints**: Scope: session vs transaction; naming conventions.

---

### Q160. Table Partitioning Concept

🔴 **Difficulty**: Advanced  
**Skill**: Partition design

**Problem**: Design a partitioning strategy for `orders` table with 10 million rows spanning 5 years.

**Expected Output**: Partition by range (date) strategy with monthly/yearly partitions.

**Constraints**: PostgreSQL declarative partitioning syntax.

---

## Section 13: Query Optimization (Q161-170)

---

### Q161. EXPLAIN Plan Reading

🔴 **Difficulty**: Advanced  
**Skill**: Interpreting execution plans

**Problem**: Run EXPLAIN on this query and interpret the results:
```sql
SELECT * FROM orders o 
JOIN customers c ON o.customer_id = c.customer_id 
WHERE c.country = 'USA';
```

**Expected Output**: Explanation of scan types, join methods, costs.

**Constraints**: 
- PostgreSQL: `EXPLAIN ANALYZE`
- MySQL: `EXPLAIN FORMAT=JSON`

---

### Q162. Index Scan vs Sequential Scan

🔴 **Difficulty**: Advanced  
**Skill**: Understanding scan types

**Problem**: When does the optimizer choose a sequential scan over an index scan?

**Expected Output**: Scenarios: small tables, low selectivity, missing index, etc.

**Constraints**: Sometimes seq scan IS faster.

---

### Q163. Sargability

🔴 **Difficulty**: Advanced  
**Skill**: Search argument-able predicates

**Problem**: Rewrite these non-sargable queries to be index-friendly:
1. `WHERE YEAR(order_date) = 2024`
2. `WHERE UPPER(email) = 'TEST@EMAIL.COM'`
3. `WHERE price * 1.1 > 100`

**Expected Output**: Sargable versions of each query.

**Constraints**: Avoid functions on indexed columns in WHERE.

---

### Q164. Join Order Optimization

🔴 **Difficulty**: Advanced  
**Skill**: Query structure for optimizer

**Problem**: You have tables A (1M rows), B (1K rows), C (100 rows). How should you order joins?

**Expected Output**: Discussion of join order, hints, and optimizer behavior.

**Constraints**: Modern optimizers usually handle this, but understand the logic.

---

### Q165. Avoiding N+1 Queries

🔴 **Difficulty**: Advanced  
**Skill**: Batch fetching

**Problem**: Application runs 100 separate queries to get order details. Rewrite as single query.

**Expected Output**: JOIN-based single query replacing loop.

**Constraints**: Common ORM problem; use eager loading.

---

### Q166. Index-Only Scan

🔴 **Difficulty**: Advanced  
**Skill**: Covering indexes

**Problem**: Create an index that allows this query to be answered entirely from the index:
```sql
SELECT customer_id, order_count FROM (
  SELECT customer_id, COUNT(*) as order_count FROM orders GROUP BY customer_id
) x;
```

**Expected Output**: Index on customer_id that covers the query.

**Constraints**: Include columns avoid table lookups.

---

### Q167. Query Rewriting for Performance

🔴 **Difficulty**: Advanced  
**Skill**: Equivalent but faster queries

**Problem**: Optimize this query:
```sql
SELECT * FROM products WHERE category_id IN (
  SELECT category_id FROM categories WHERE category_name LIKE 'Electronics%'
);
```

**Expected Output**: JOIN version and performance comparison.

**Constraints**: Subquery vs JOIN depends on data distribution.

---

### Q168. Statistics and ANALYZE

🔴 **Difficulty**: Advanced  
**Skill**: Table statistics

**Problem**: Query runs slow after large data load. What should you do?

**Expected Output**: 
```sql
ANALYZE orders;  -- PostgreSQL
ANALYZE TABLE orders;  -- MySQL
```

**Constraints**: Outdated statistics lead to bad plans.

---

### Q169. Connection Pooling Awareness

🔴 **Difficulty**: Advanced  
**Skill**: Resource management

**Problem**: Application uses 500 database connections. What are the problems and solutions?

**Expected Output**: Discussion of connection pooling, pgbouncer, etc.

**Constraints**: Each connection consumes memory; pool size tuning.

---

### Q170. Query Profiling

🔴 **Difficulty**: Advanced  
**Skill**: Performance diagnosis

**Problem**: Demonstrate how to identify slow queries in:
1. PostgreSQL (pg_stat_statements)
2. MySQL (slow query log)

**Expected Output**: Configuration and query examples.

**Constraints**: Enable monitoring in production with minimal overhead.

---

# Expert Level

## Section 14: Transactions and Concurrency (Q171-180)

---

### Q171. Transaction Basics

🔴 **Difficulty**: Expert  
**Skill**: BEGIN, COMMIT, ROLLBACK

**Problem**: Write a transaction that transfers $100 from customer A to customer B. Handle insufficient balance.

**Expected Output**: Complete transaction with error handling.

**Constraints**: 
```sql
BEGIN;
UPDATE accounts SET balance = balance - 100 WHERE customer_id = 'A';
UPDATE accounts SET balance = balance + 100 WHERE customer_id = 'B';
COMMIT;
```

---

### Q172. SAVEPOINT Usage

🔴 **Difficulty**: Expert  
**Skill**: Partial rollback

**Problem**: In a complex order creation, use SAVEPOINTs to rollback only failed items while preserving successful ones.

**Expected Output**: Transaction with multiple savepoints.

**Constraints**: 
```sql
SAVEPOINT sp1;
-- try item 1
ROLLBACK TO sp1;  -- if failed
```

---

### Q173. Isolation Level - Read Uncommitted

🔴 **Difficulty**: Expert  
**Skill**: Dirty reads

**Problem**: Demonstrate a dirty read scenario with READ UNCOMMITTED isolation.

**Expected Output**: Two session scripts showing dirty read.

**Constraints**: Not recommended for production; useful for understanding.

---

### Q174. Isolation Level - Read Committed

🔴 **Difficulty**: Expert  
**Skill**: Non-repeatable reads

**Problem**: Show how READ COMMITTED prevents dirty reads but allows non-repeatable reads.

**Expected Output**: Two session example with timing.

**Constraints**: Default in PostgreSQL.

---

### Q175. Isolation Level - Repeatable Read

🔴 **Difficulty**: Expert  
**Skill**: Phantom reads

**Problem**: Demonstrate phantom reads in REPEATABLE READ (MySQL) vs prevention in PostgreSQL.

**Expected Output**: Comparative behavior explanation.

**Constraints**: Implementation varies by database.

---

### Q176. Isolation Level - Serializable

🔴 **Difficulty**: Expert  
**Skill**: Strictest isolation

**Problem**: When would you use SERIALIZABLE? Demonstrate a scenario requiring it.

**Expected Output**: Example with serialization anomaly prevented.

**Constraints**: Performance impact; use sparingly.

---

### Q177. Locking Fundamentals

🔴 **Difficulty**: Expert  
**Skill**: Row-level vs table-level locks

**Problem**: Explain the locking behavior of:
1. `SELECT ... FOR UPDATE`
2. `SELECT ... FOR SHARE`

**Expected Output**: Use cases and behavior differences.

**Constraints**: FOR UPDATE locks for write; FOR SHARE for read.

---

### Q178. Deadlock Scenario

🔴 **Difficulty**: Expert  
**Skill**: Deadlock understanding

**Problem**: Create a deadlock between two transactions accessing rows in opposite order.

**Expected Output**: 
```
Session 1: Lock row A, then try row B
Session 2: Lock row B, then try row A
Result: Deadlock detected
```

**Constraints**: Database auto-detects and kills one transaction.

---

### Q179. Deadlock Prevention

🔴 **Difficulty**: Expert  
**Skill**: Lock ordering

**Problem**: How would you prevent the deadlock from Q178?

**Expected Output**: Strategies: consistent lock ordering, shorter transactions, deadlock retry logic.

**Constraints**: Application-level solution.

---

### Q180. Optimistic vs Pessimistic Locking

🔴 **Difficulty**: Expert  
**Skill**: Concurrency control strategies

**Problem**: Implement optimistic locking using a version column. Show the UPDATE pattern.

**Expected Output**: 
```sql
UPDATE products SET stock = stock - 1, version = version + 1 
WHERE product_id = ? AND version = ?;
-- Check rows affected; if 0, retry
```

**Constraints**: Optimistic better for low contention; pessimistic for high contention.

---

## Section 15: Advanced Topics (Q181-190)

---

### Q181. JSON Data - Storage

🔴 **Difficulty**: Expert  
**Skill**: JSON/JSONB columns

**Problem**: Create a table with JSON metadata column and insert sample data.

**Expected Output**: 
```sql
CREATE TABLE products_v2 (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100),
  metadata JSONB
);
INSERT INTO products_v2 VALUES (1, 'Widget', '{"color": "red", "sizes": [1,2,3]}');
```

**Constraints**: PostgreSQL JSONB; MySQL JSON.

---

### Q182. JSON Data - Querying

🔴 **Difficulty**: Expert  
**Skill**: JSON operators

**Problem**: Query products where `metadata->>'color'` is 'red' and metadata contains a size > 5.

**Expected Output**: 
- PostgreSQL: `WHERE metadata->>'color' = 'red' AND metadata->'sizes' @> '[5]'`
- MySQL: `WHERE JSON_EXTRACT(metadata, '$.color') = 'red'`

**Constraints**: Operator syntax varies significantly.

---

### Q183. JSON Data - Indexing

🔴 **Difficulty**: Expert  
**Skill**: GIN indexes on JSON

**Problem**: Create an index to optimize JSON queries on the metadata column.

**Expected Output**: 
```sql
CREATE INDEX idx_metadata ON products_v2 USING GIN (metadata);
```

**Constraints**: GIN supports containment operators (@>).

---

### Q184. Array Operations

🔴 **Difficulty**: Expert  
**Skill**: PostgreSQL arrays

**Problem**: Store tags as an array and query products with specific tags.

**Expected Output**: 
```sql
-- Create
tags TEXT[]
-- Query
WHERE tags @> ARRAY['sale', 'new']
-- Unnest
SELECT unnest(tags) FROM products
```

**Constraints**: PostgreSQL-specific.

---

### Q185. PIVOT / CROSSTAB

🔴 **Difficulty**: Expert  
**Skill**: Pivoting data

**Problem**: Transform monthly sales data from rows to columns (Jan, Feb, Mar as separate columns).

**Expected Output**: 
```sql
-- PostgreSQL with tablefunc
SELECT * FROM crosstab(...) 
-- Standard SQL with CASE
SELECT 
  product_id,
  SUM(CASE WHEN month = 1 THEN amount END) as jan,
  SUM(CASE WHEN month = 2 THEN amount END) as feb
FROM sales GROUP BY product_id;
```

**Constraints**: Standard approach works everywhere.

---

### Q186. UNPIVOT

🔴 **Difficulty**: Expert  
**Skill**: Columns to rows

**Problem**: Transform columns (metric_a, metric_b, metric_c) into rows with (metric_name, value).

**Expected Output**: 
```sql
SELECT id, 'metric_a' as metric, metric_a as value FROM data
UNION ALL
SELECT id, 'metric_b', metric_b FROM data
-- OR PostgreSQL: LATERAL with VALUES
```

**Constraints**: UNPIVOT is SQL Server specific; UNION works everywhere.

---

### Q187. Full-Text Search

🔴 **Difficulty**: Expert  
**Skill**: Text search capabilities

**Problem**: Implement full-text search on product descriptions.

**Expected Output**: 
```sql
-- PostgreSQL
CREATE INDEX idx_fts ON products USING GIN (to_tsvector('english', description));
SELECT * FROM products WHERE to_tsvector('english', description) @@ to_tsquery('widget & blue');
```

**Constraints**: More powerful than LIKE for text search.

---

### Q188. MERGE / UPSERT

🔴 **Difficulty**: Expert  
**Skill**: Insert or update in one statement

**Problem**: Insert a new product or update if SKU already exists.

**Expected Output**: 
```sql
-- PostgreSQL
INSERT INTO products (sku, name, price) VALUES (...)
ON CONFLICT (sku) DO UPDATE SET name = EXCLUDED.name, price = EXCLUDED.price;

-- SQL Server
MERGE INTO products USING (...) ...
```

**Constraints**: Syntax varies; understand atomic behavior.

---

### Q189. Lateral Subquery

🔴 **Difficulty**: Expert  
**Skill**: LATERAL for row-by-row correlation

**Problem**: For each category, get the top 2 selling products (alternative to window function).

**Expected Output**: 
```sql
SELECT c.*, p.* FROM categories c
CROSS JOIN LATERAL (
  SELECT * FROM products WHERE category_id = c.category_id 
  ORDER BY sales DESC LIMIT 2
) p;
```

**Constraints**: PostgreSQL; SQL Server uses CROSS APPLY.

---

### Q190. Common Table Expression with OUTPUT

🔴 **Difficulty**: Expert  
**Skill**: Capturing modified rows

**Problem**: Delete old orders and log them in an audit table, in a single statement.

**Expected Output**: 
```sql
-- PostgreSQL
WITH deleted AS (
  DELETE FROM orders WHERE order_date < '2020-01-01' RETURNING *
)
INSERT INTO orders_archive SELECT * FROM deleted;
```

**Constraints**: Powerful for audit trails.

---

## Section 16: Real-World Case Studies (Q191-200)

---

### Q191. E-commerce: Abandoned Cart Analysis

🔴 **Difficulty**: Expert  
**Skill**: Multi-step analytics

**Problem**: Find customers who added items to cart but didn't complete purchase in the last 7 days. Calculate potential revenue lost.

**Expected Output**: Customer list with cart value and days since activity.

**Constraints**: Requires cart_items table (assume exists).

---

### Q192. E-commerce: Cohort Retention

🔴 **Difficulty**: Expert  
**Skill**: Cohort analysis

**Problem**: Calculate monthly retention rate: what % of customers acquired in month M made a purchase in months M+1, M+2, etc.

**Expected Output**: 
| cohort_month | month_1 | month_2 | month_3 |
|--------------|---------|---------|---------|
| 2024-01 | 100% | 45% | 32% |

**Constraints**: Complex date logic with window functions.

---

### Q193. E-commerce: RFM Segmentation

🔴 **Difficulty**: Expert  
**Skill**: Customer segmentation

**Problem**: Score customers on Recency, Frequency, Monetary value (1-5 each). Identify "Champions" (5,5,5) and "At Risk" (low scores).

**Expected Output**: Customer RFM scores with segment labels.

**Constraints**: Use NTILE for scoring.

---

### Q194. Financial: Running Balance

🔴 **Difficulty**: Expert  
**Skill**: Account balance calculation

**Problem**: Given a transactions table (account_id, date, amount +/-), calculate running balance per account.

**Expected Output**: Each transaction with running balance.

**Constraints**: Use SUM window function partitioned by account.

---

### Q195. Financial: Fraud Detection

🔴 **Difficulty**: Expert  
**Skill**: Pattern detection

**Problem**: Flag transactions where the same customer makes 3+ purchases within 5 minutes from different locations.

**Expected Output**: Suspicious transaction list.

**Constraints**: Use LAG/LEAD to compare timestamps; requires location data.

---

### Q196. HR: Salary Band Analysis

🔴 **Difficulty**: Expert  
**Skill**: Comparative analytics

**Problem**: For each department, show employees earning above/below the department median, with deviation percentage.

**Expected Output**: Employee list with median comparison.

**Constraints**: Use PERCENTILE_CONT or subquery for median.

---

### Q197. Inventory: Reorder Report

🔴 **Difficulty**: Expert  
**Skill**: Business logic implementation

**Problem**: Generate a reorder report showing products below reorder_level, with suggested order quantity based on average daily sales.

**Expected Output**: Product, current stock, daily avg sales, days until stockout, suggested order qty.

**Constraints**: Multiple joins and calculations.

---

### Q198. Marketing: Attribution Analysis

🔴 **Difficulty**: Expert  
**Skill**: Customer journey analysis

**Problem**: For customers who converted, find the first and last marketing touchpoint before conversion (first-touch and last-touch attribution).

**Expected Output**: Customer, first_touch_source, last_touch_source.

**Constraints**: Requires touchpoint/event tracking table.

---

### Q199. Operations: SLA Compliance

🔴 **Difficulty**: Expert  
**Skill**: Time-based metrics

**Problem**: Calculate % of orders shipped within 48 hours of order placement, by month.

**Expected Output**: 
| month | total_orders | on_time | sla_compliance_pct |
|-------|--------------|---------|-------------------|
| 2024-01 | 500 | 450 | 90.0% |

**Constraints**: Handle timezone and business hours if needed.

---

### Q200. Analytics: Funnel Analysis

🔴 **Difficulty**: Expert  
**Skill**: Conversion funnel

**Problem**: Given event data (view → add_to_cart → checkout → purchase), calculate conversion rate at each step.

**Expected Output**: 
| step | users | conversion_from_prev | conversion_from_start |
|------|-------|---------------------|----------------------|
| view | 10000 | - | 100% |
| add_to_cart | 3000 | 30% | 30% |
| checkout | 1000 | 33% | 10% |
| purchase | 800 | 80% | 8% |

**Constraints**: Requires event tracking table with session/user IDs.

---

# Capstone Mini-Projects

## Mini-Project 1: E-Commerce Analytics Platform

### Overview
Design and implement a complete e-commerce analytics system.

### Part A: Schema Design (2-3 hours)

**Task**: Design a schema to track:
- Products and categories (with hierarchy)
- Customers with address history
- Orders, returns, and refunds
- Inventory with warehouse locations
- Product reviews and ratings

**Deliverables**:
1. ERD diagram
2. CREATE TABLE statements with all constraints
3. Sample data (50+ rows per main table)

### Part B: Operational Queries (2-3 hours)

Write queries for:
1. Daily sales dashboard: revenue, orders, avg order value by hour
2. Inventory alerts: products below reorder level by warehouse
3. Customer lifetime value calculation
4. Product performance: sales velocity, return rate, avg rating
5. Shipping SLA compliance by carrier

### Part C: Advanced Analytics (3-4 hours)

1. **Customer Segmentation**: RFM analysis with behavioral clusters
2. **Product Affinity**: "Customers who bought X also bought Y"
3. **Seasonality Analysis**: Year-over-year comparison by product category
4. **Churn Prediction Data**: Identify at-risk customers based on declining purchase frequency

### Part D: Performance Optimization (1-2 hours)

1. Add appropriate indexes for your queries
2. Create materialized views for dashboard queries
3. Document EXPLAIN plans before/after optimization
4. Implement table partitioning for orders by date

---

## Mini-Project 2: Banking Transaction System (OLTP)

### Overview
Build a robust banking transaction system with proper concurrency handling.

### Part A: Schema Design (2 hours)

**Task**: Design tables for:
- Accounts (checking, savings, credit)
- Transactions (deposits, withdrawals, transfers)
- Transaction history / audit log
- Users and access control

**Requirements**:
- Accounts must never go negative (except credit)
- All changes must be audited
- Support for multiple currencies

### Part B: Transaction Logic (3-4 hours)

Implement these transactions with proper handling:
1. **Transfer**: Move funds between accounts atomically
2. **Batch Payment**: Pay multiple bills in one transaction
3. **Currency Exchange**: Convert between currencies with rate lookup
4. **Statement Generation**: Monthly statement with running balance

### Part C: Concurrency Challenges (2-3 hours)

1. Implement optimistic locking for account updates
2. Create a scenario showing deadlock and implement prevention
3. Write tests for isolation level behavior
4. Implement idempotent transaction endpoints (prevent double-processing)

### Part D: Reporting (1-2 hours)

1. Daily transaction summary by account type
2. Suspicious activity detection (large transfers, unusual patterns)
3. Monthly fee calculation and application
4. Interest accrual calculation

---

## Mini-Project 3: Social Media Analytics Dashboard

### Overview
Analyze social media engagement patterns with complex time-series data.

### Part A: Schema Design (1-2 hours)

**Task**: Design tables for:
- Users with profile data
- Posts (text, images, videos)
- Engagement (likes, comments, shares)
- Followers/following relationships
- Hashtags and mentions

### Part B: Engagement Metrics (2-3 hours)

1. **Post Performance**: Engagement rate by post type and time of day
2. **Viral Detection**: Posts with exponential engagement growth
3. **Influencer Score**: Based on reach and engagement quality
4. **Hashtag Trending**: Rising hashtags in the last 24 hours

### Part C: Network Analysis (2-3 hours)

1. **Follower Growth**: Daily net follower change with moving average
2. **Mutual Connections**: Find users who follow each other
3. **Reach Calculation**: Potential reach based on follower chains (2 levels)
4. **Community Detection**: Users frequently interacting together

### Part D: Advanced Features (2-3 hours)

1. **Timeline Generation**: Generate personalized feed with ranking
2. **Recommendation Engine**: Suggest users to follow based on network
3. **Content Moderation Queue**: Prioritize flagged content by severity
4. **A/B Test Analysis**: Compare engagement between feature variants

---

# Answer Key Notes

> **For Instructors**: Solution approaches for selected problems are available.
> Each question is designed to have multiple valid solutions.
> Encourage exploration of different approaches and performance comparison.

---

**End of SQL Practice Curriculum**

*Total Questions: 200*  
*Capstone Projects: 3*  
*Estimated Completion Time: 80-120 hours*

