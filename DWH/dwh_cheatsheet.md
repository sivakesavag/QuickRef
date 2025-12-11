# Data Warehousing & Data Modelling Cheatsheet

> **Comprehensive reference guide for solving DWH assignments from Beginner to Expert level**

---

## Table of Contents

1. [Foundational Concepts](#1-foundational-concepts)
2. [Data Modeling Fundamentals](#2-data-modeling-fundamentals)
3. [Dimensional Modeling](#3-dimensional-modeling)
4. [Slowly Changing Dimensions](#4-slowly-changing-dimensions)
5. [Advanced Dimension Patterns](#5-advanced-dimension-patterns)
6. [Fact Table Patterns](#6-fact-table-patterns)
7. [ETL/ELT Patterns](#7-etlelt-patterns)
8. [Data Vault Modeling](#8-data-vault-modeling)
9. [Architecture Patterns](#9-architecture-patterns)
10. [Performance Optimization](#10-performance-optimization)
11. [Data Quality & Governance](#11-data-quality--governance)
12. [SQL Reference](#12-sql-reference)
13. [Industry Data Models](#13-industry-data-models)
14. [Quick Reference Tables](#14-quick-reference-tables)

---

## Cheatsheet Overview

| Section | Topics Covered |
|---------|----------------|
| **1. Foundational Concepts** | OLTP vs OLAP comparison, DWH characteristics (Inmon), Data warehouse layer architecture |
| **2. Data Modeling Fundamentals** | Conceptual/Logical/Physical models, ER diagram notations (Chen, Crow's Foot), Normalization (1NF, 2NF, 3NF, BCNF), Key types (Natural vs Surrogate) |
| **3. Dimensional Modeling** | Star/Snowflake/Galaxy schemas, Dimension table design, Date dimension templates, Fact table design, Measure types (Additive/Semi-Additive/Non-Additive), Grain determination |
| **4. Slowly Changing Dimensions** | SCD comparison table (Types 0-6), Type 1 (Overwrite), Type 2 (Add row with dates/flags), Type 3 (Add column), Type 6 (Hybrid 1+2+3) with complete SQL examples |
| **5. Advanced Dimension Patterns** | Junk dimensions (combining low-cardinality flags), Degenerate dimensions (IDs without dimension tables), Role-playing dimensions (single dimension, multiple roles), Bridge tables (M:M relationships with weight factors) |
| **6. Fact Table Patterns** | Factless fact tables (Coverage & Event tracking), Accumulating snapshot (process lifecycle), Periodic snapshot (state at intervals) |
| **7. ETL/ELT Patterns** | ETL vs ELT comparison, Staging layer patterns (Raw → Clean), Incremental load strategies (Watermark-based, Hash-based), MERGE (Upsert) pattern, Late-arriving data handling |
| **8. Data Vault Modeling** | Hub design (business entities), Link design (relationships), Satellite design (descriptive attributes), Hash key generation, Data Vault loading patterns |
| **9. Architecture Patterns** | Inmon (top-down, 3NF), Kimball (bottom-up, dimensional), Data Vault (hybrid), Lambda (batch + real-time), Kappa (stream-only) |
| **10. Performance Optimization** | Indexing strategies (Columnstore for facts, B-Tree for dimensions), Partitioning (range, benefits), Query optimization tips (Do's & Don'ts), Aggregation strategies |
| **11. Data Quality & Governance** | Data quality dimensions (Completeness, Accuracy, Consistency, Timeliness, Uniqueness, Validity), Quality check SQL patterns, Audit dimension design, Data lineage queries |
| **12. SQL Reference** | Window functions (Ranking, Running totals, YoY comparison), Common aggregations, Pivoting, Date calculations |
| **13. Industry Data Models** | Retail (Customer, Product, Store, Sales), Healthcare (Patient, Provider, Encounter), Finance (Account, Transaction, Credit exposure), E-Commerce (Order, Clickstream, Session) |
| **14. Quick Reference Tables** | SCD type summary, Fact table type summary, Architecture pattern comparison, Key formulas, Common SQL patterns, Abbreviations & Glossary |

---

# 1. Foundational Concepts

## OLTP vs OLAP

| Characteristic | OLTP | OLAP |
|----------------|------|------|
| **Purpose** | Transaction processing | Analytical processing |
| **Data** | Current, operational | Historical, integrated |
| **Design** | Normalized (3NF) | Denormalized (Star/Snowflake) |
| **Queries** | Simple, predefined | Complex, ad-hoc |
| **Users** | Clerks, customers | Analysts, managers |
| **Volume** | Many small transactions | Few complex queries |
| **Updates** | Frequent updates | Periodic batch loads |
| **Response Time** | Milliseconds | Seconds to minutes |
| **Data Size** | Gigabytes | Terabytes to Petabytes |
| **Optimization** | Write-optimized | Read-optimized |

## Data Warehouse Characteristics (Bill Inmon)

1. **Subject-Oriented**: Organized around major subjects (customers, products, sales)
2. **Integrated**: Data from multiple sources, consistent naming/formats
3. **Time-Variant**: Historical data with time dimension
4. **Non-Volatile**: Data is loaded and accessed, not updated frequently

## Data Warehouse Layers

```
┌─────────────────────────────────────────────────────┐
│                 Presentation Layer                   │
│          (Data Marts, Reports, Dashboards)          │
├─────────────────────────────────────────────────────┤
│                 Integration Layer                    │
│        (Conformed Dimensions, Enterprise DWH)       │
├─────────────────────────────────────────────────────┤
│                   Staging Layer                      │
│          (Cleansing, Transformation, CDC)           │
├─────────────────────────────────────────────────────┤
│                     Raw Layer                        │
│              (Source Data Landing Zone)             │
├─────────────────────────────────────────────────────┤
│                   Source Systems                     │
│            (ERP, CRM, Files, APIs, IoT)             │
└─────────────────────────────────────────────────────┘
```

---

# 2. Data Modeling Fundamentals

## Conceptual vs Logical vs Physical Models

| Aspect | Conceptual | Logical | Physical |
|--------|------------|---------|----------|
| **Purpose** | Business view | Detailed design | Implementation |
| **Audience** | Business users | Data architects | DBAs, developers |
| **Details** | Entities, relationships | Attributes, keys, constraints | Tables, columns, indexes |
| **Technology** | Independent | Independent | Database-specific |
| **Notation** | ER diagrams | ER with attributes | DDL scripts |

## Entity-Relationship (ER) Diagram Notation

### Chen Notation
```
┌─────────┐          ┌─────────┐
│ ENTITY  │──────────│ ENTITY  │
└─────────┘    │     └─────────┘
               │
         ◇ Relationship
               │
          (cardinality)
```

### Crow's Foot Notation
```
Cardinality Symbols:
○──────  Zero or one (optional)
│──────  Exactly one (mandatory)
○──<──  Zero or many
│──<──  One or many
```

### Cardinality Examples
```
One-to-One (1:1):     Customer ──│──│── Address
One-to-Many (1:M):    Customer ──│──<── Orders
Many-to-Many (M:M):   Students ──>──<── Courses
```

## Normalization Forms

### First Normal Form (1NF)
**Rule**: Eliminate repeating groups; ensure atomic values

❌ **Before (Violation)**:
| OrderID | Products |
|---------|----------|
| 1 | Laptop, Mouse, Keyboard |

✅ **After (1NF)**:
| OrderID | Product |
|---------|---------|
| 1 | Laptop |
| 1 | Mouse |
| 1 | Keyboard |

### Second Normal Form (2NF)
**Rule**: Must be in 1NF + No partial dependencies (all non-key attributes depend on entire primary key)

❌ **Before (Violation)** - Composite key (OrderID, ProductID):
| OrderID | ProductID | ProductName | Quantity |
|---------|-----------|-------------|----------|
ProductName depends only on ProductID (partial dependency)

✅ **After (2NF)**: Split into two tables
- Orders (OrderID, ProductID, Quantity)
- Products (ProductID, ProductName)

### Third Normal Form (3NF)
**Rule**: Must be in 2NF + No transitive dependencies

❌ **Before (Violation)**:
| EmployeeID | DeptID | DeptName |
|------------|--------|----------|
DeptName depends on DeptID (transitive dependency)

✅ **After (3NF)**: Split into two tables
- Employees (EmployeeID, DeptID)
- Departments (DeptID, DeptName)

### Boyce-Codd Normal Form (BCNF)
**Rule**: For every functional dependency X → Y, X must be a superkey

**Key difference from 3NF**: In BCNF, determinants must be candidate keys

### Quick Normalization Memory Aid
```
1NF: "No repeating groups"
2NF: "Whole key" (no partial dependencies)
3NF: "Nothing but the key" (no transitive dependencies)
BCNF: "Every determinant is a candidate key"
```

## Keys

| Key Type | Definition | Example |
|----------|------------|---------|
| **Primary Key** | Unique identifier for each row | CustomerID |
| **Candidate Key** | Column(s) that could be primary key | SSN, Email |
| **Foreign Key** | References primary key in another table | Orders.CustomerID → Customers.CustomerID |
| **Composite Key** | Multiple columns forming primary key | (OrderID, ProductID) |
| **Natural Key** | Business-meaningful identifier | ISBN, SSN, Email |
| **Surrogate Key** | System-generated artificial key | Auto-increment ID |

### Natural vs Surrogate Keys

| Aspect | Natural Key | Surrogate Key |
|--------|-------------|---------------|
| **Meaning** | Business value | No business meaning |
| **Stability** | May change | Never changes |
| **Size** | Variable (often larger) | Fixed (INT/BIGINT) |
| **Performance** | Can be slower for joins | Faster joins |
| **ETL Complexity** | Easier matching | Requires lookup |
| **Exposure** | Safe to expose | Should not expose |

**Best Practice**: Use surrogate keys for dimension tables, keep natural keys as attributes for business lookups.

---

# 3. Dimensional Modeling

## Star Schema

```
         ┌─────────────────┐
         │   dim_date      │
         │─────────────────│
         │ date_key (PK)   │
         │ full_date       │
         │ day_name        │
         │ month_name      │
         │ year            │
         └────────┬────────┘
                  │
┌─────────────────┼─────────────────┐
│                 │                 │
│    ┌────────────┴────────────┐    │
│    │      fact_sales         │    │
│    │─────────────────────────│    │
│    │ date_key (FK)           │    │
│    │ product_key (FK)        │    │
│    │ store_key (FK)          │    │
│    │ customer_key (FK)       │    │
│    │ quantity                │    │
│    │ unit_price              │    │
│    │ sales_amount            │    │
│    └─────────────────────────┘    │
│                 │                 │
└─────────────────┼─────────────────┘
                  │
┌────────────┬────┴───┬────────────┐
│            │        │            │
▼            ▼        ▼            ▼
dim_product  dim_store  dim_customer
```

### Star Schema Characteristics
- **Fact table** at center with foreign keys to dimensions
- **Dimension tables** surrounding fact table
- Denormalized dimensions for query simplicity
- Optimized for read-heavy analytical workloads

## Snowflake Schema

```
dim_category ◄── dim_subcategory ◄── dim_product ──► fact_sales
                                                         │
dim_country ◄── dim_state ◄── dim_city ◄── dim_store ◄──┘
```

### Snowflake Characteristics
- Normalized dimension tables
- Reduces data redundancy
- More complex queries (more joins)
- Better for very large dimensions

## Galaxy Schema (Fact Constellation)

```
                    dim_date
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
   fact_sales    fact_inventory   fact_orders
        │              │              │
        └──────────────┼──────────────┘
                       │
                   dim_product
                   dim_store
```

### Galaxy Characteristics
- Multiple fact tables
- Shared (conformed) dimensions
- Enables cross-functional analysis

## Dimension Table Design

### Standard Dimension Structure
```sql
CREATE TABLE dim_customer (
    -- Surrogate Key
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    
    -- Natural Key(s)
    customer_id VARCHAR(20) NOT NULL,
    
    -- Descriptive Attributes
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    
    -- Hierarchy Attributes
    city VARCHAR(50),
    state VARCHAR(50),
    country VARCHAR(50),
    region VARCHAR(50),
    
    -- Segmentation Attributes
    customer_segment VARCHAR(30),
    loyalty_tier VARCHAR(20),
    
    -- SCD Control Columns (if Type 2)
    effective_start_date DATE,
    effective_end_date DATE,
    is_current BIT DEFAULT 1,
    
    -- Audit Columns
    created_date DATETIME DEFAULT GETDATE(),
    modified_date DATETIME
);
```

### Date Dimension (Must-Have)
```sql
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,           -- YYYYMMDD format
    full_date DATE NOT NULL UNIQUE,
    
    -- Day Attributes
    day_of_week INT,                     -- 1-7
    day_name VARCHAR(10),                -- Monday, Tuesday...
    day_of_month INT,                    -- 1-31
    day_of_year INT,                     -- 1-366
    
    -- Week Attributes
    week_of_year INT,
    week_of_month INT,
    
    -- Month Attributes
    month_number INT,                    -- 1-12
    month_name VARCHAR(15),              -- January, February...
    month_short VARCHAR(3),              -- Jan, Feb...
    
    -- Quarter Attributes
    quarter_number INT,                  -- 1-4
    quarter_name VARCHAR(6),             -- Q1, Q2...
    
    -- Year Attributes
    year_number INT,
    
    -- Fiscal Calendar (if needed)
    fiscal_year INT,
    fiscal_quarter INT,
    fiscal_month INT,
    
    -- Flags
    is_weekday BIT,
    is_weekend BIT,
    is_holiday BIT,
    holiday_name VARCHAR(50),
    is_last_day_of_month BIT
);
```

### Date Dimension Population Script
```sql
DECLARE @StartDate DATE = '2020-01-01';
DECLARE @EndDate DATE = '2030-12-31';
DECLARE @Date DATE = @StartDate;

WHILE @Date <= @EndDate
BEGIN
    INSERT INTO dim_date (
        date_key, full_date, day_of_week, day_name,
        day_of_month, month_number, month_name,
        quarter_number, year_number, is_weekend
    )
    VALUES (
        CONVERT(INT, FORMAT(@Date, 'yyyyMMdd')),
        @Date,
        DATEPART(WEEKDAY, @Date),
        DATENAME(WEEKDAY, @Date),
        DAY(@Date),
        MONTH(@Date),
        DATENAME(MONTH, @Date),
        DATEPART(QUARTER, @Date),
        YEAR(@Date),
        CASE WHEN DATEPART(WEEKDAY, @Date) IN (1, 7) THEN 1 ELSE 0 END
    );
    SET @Date = DATEADD(DAY, 1, @Date);
END;
```

## Fact Table Design

### Fact Table Types

| Type | Description | Example | Grain |
|------|-------------|---------|-------|
| **Transaction** | Individual events | Sales, Orders | One row per event |
| **Periodic Snapshot** | State at regular intervals | Daily Balance | One row per period |
| **Accumulating Snapshot** | Lifetime of a process | Order Lifecycle | One row per entity |
| **Factless** | Events without measures | Attendance | One row per event |

### Standard Fact Table Structure
```sql
CREATE TABLE fact_sales (
    -- Surrogate Key (optional)
    sales_key BIGINT IDENTITY(1,1) PRIMARY KEY,
    
    -- Foreign Keys (dimensional context)
    date_key INT NOT NULL,
    product_key INT NOT NULL,
    store_key INT NOT NULL,
    customer_key INT NOT NULL,
    
    -- Degenerate Dimensions
    order_number VARCHAR(30),
    invoice_number VARCHAR(30),
    
    -- Measures (Additive)
    quantity INT,
    unit_price DECIMAL(10,2),
    gross_amount DECIMAL(12,2),
    discount_amount DECIMAL(10,2),
    net_amount DECIMAL(12,2),
    cost_amount DECIMAL(12,2),
    profit_amount DECIMAL(12,2),
    
    -- Semi-Additive Measures
    -- (e.g., inventory balance - additive across some dimensions)
    
    -- Non-Additive Measures
    -- (e.g., ratios, percentages - cannot sum directly)
    unit_margin_pct DECIMAL(5,2),
    
    -- Audit
    load_date DATETIME DEFAULT GETDATE(),
    audit_key INT
);
```

### Measure Types

| Type | Can Sum Across | Example |
|------|----------------|---------|
| **Additive** | All dimensions | Sales Amount, Quantity |
| **Semi-Additive** | Some dimensions | Account Balance (not time) |
| **Non-Additive** | No dimensions | Ratios, Percentages |

**Handling Non-Additive**: Store components separately, calculate ratios at query time
```sql
-- Store margin_amount and sales_amount
-- Calculate: margin_pct = SUM(margin_amount) / SUM(sales_amount) * 100
```

## Grain

**Definition**: The level of detail stored in a fact table

### Determining Grain
1. Identify the business process
2. Define the level of detail needed
3. Express as a declarative statement

**Examples**:
- "One row per sales transaction line item"
- "One row per customer per day"
- "One row per employee per pay period"

**Rule**: Grain must be consistent throughout the fact table

---

# 4. Slowly Changing Dimensions

## SCD Type Comparison

| Type | Strategy | History | Use Case |
|------|----------|---------|----------|
| **Type 0** | Retain Original | None | Fixed attributes (birth date) |
| **Type 1** | Overwrite | None | Error corrections |
| **Type 2** | Add New Row | Full | Audit requirements |
| **Type 3** | Add Column | Limited (1 prior) | Track specific changes |
| **Type 4** | Mini-Dimension | Full (separate table) | Rapidly changing attributes |
| **Type 6** | Hybrid (1+2+3) | Full + Current | Complex requirements |

## SCD Type 1 (Overwrite)

**Characteristics**: Simply update the existing record

```sql
-- Update procedure
UPDATE dim_customer
SET 
    customer_name = @new_name,
    email = @new_email,
    modified_date = GETDATE()
WHERE customer_id = @customer_id;
```

**Pros**: Simple, no storage overhead
**Cons**: No history tracking

## SCD Type 2 (Add New Row)

**Characteristics**: Create new row for each change, track with dates/flags

### Table Structure
```sql
CREATE TABLE dim_customer_scd2 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20) NOT NULL,
    customer_name VARCHAR(100),
    address VARCHAR(200),
    -- Type 2 control columns
    effective_start_date DATE NOT NULL,
    effective_end_date DATE,          -- NULL = current
    is_current BIT DEFAULT 1,
    version_number INT DEFAULT 1
);
```

### Update Logic
```sql
DECLARE @today DATE = CAST(GETDATE() AS DATE);

-- Step 1: Expire current record
UPDATE dim_customer_scd2
SET 
    effective_end_date = DATEADD(DAY, -1, @today),
    is_current = 0
WHERE customer_id = @customer_id 
  AND is_current = 1
  AND (address <> @new_address);  -- Only if changed

-- Step 2: Insert new version
INSERT INTO dim_customer_scd2 (
    customer_id, customer_name, address,
    effective_start_date, is_current, version_number
)
SELECT 
    @customer_id, @customer_name, @new_address,
    @today, 1, MAX(version_number) + 1
FROM dim_customer_scd2
WHERE customer_id = @customer_id;
```

### Point-in-Time Query
```sql
-- Get customer state as of specific date
SELECT *
FROM dim_customer_scd2
WHERE customer_id = 'C001'
  AND '2024-06-15' BETWEEN effective_start_date 
      AND ISNULL(effective_end_date, '9999-12-31');
```

## SCD Type 3 (Add Column)

### Table Structure
```sql
CREATE TABLE dim_customer_scd3 (
    customer_key INT PRIMARY KEY,
    customer_id VARCHAR(20),
    customer_name VARCHAR(100),
    -- Current value
    current_segment VARCHAR(30),
    -- Previous value
    previous_segment VARCHAR(30),
    segment_change_date DATE
);
```

### Update Logic
```sql
UPDATE dim_customer_scd3
SET 
    previous_segment = current_segment,
    current_segment = @new_segment,
    segment_change_date = GETDATE()
WHERE customer_id = @customer_id
  AND current_segment <> @new_segment;
```

**Pros**: Simple, tracks one prior value
**Cons**: Limited history (only one previous value)

## SCD Type 6 (Hybrid 1+2+3)

### Table Structure
```sql
CREATE TABLE dim_customer_scd6 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20),
    -- Type 1 attributes (always current across all rows)
    customer_name VARCHAR(100),
    -- Type 2 attributes (tracked via rows)
    address VARCHAR(200),
    city VARCHAR(50),
    -- Type 3 attributes (current + previous in columns)
    current_segment VARCHAR(30),
    previous_segment VARCHAR(30),
    -- Type 2 control columns
    effective_start_date DATE,
    effective_end_date DATE,
    is_current BIT
);
```

**Use Case**: When you need:
- Current name across all history (Type 1)
- Full address history (Type 2)
- Quick access to previous segment (Type 3)

---

# 5. Advanced Dimension Patterns

## Junk Dimension

**Purpose**: Combine low-cardinality flags into single dimension

### Before (Flags in Fact Table)
```sql
CREATE TABLE fact_orders (
    ...
    is_gift BIT,
    is_expedited BIT,
    payment_type VARCHAR(20),
    shipping_type VARCHAR(20)
);
```

### After (Junk Dimension)
```sql
CREATE TABLE dim_order_flags (
    order_flag_key INT PRIMARY KEY,
    is_gift BIT,
    is_expedited BIT,
    payment_type VARCHAR(20),
    shipping_type VARCHAR(20)
);

CREATE TABLE fact_orders (
    ...
    order_flag_key INT  -- Single FK instead of multiple columns
);
```

### Population (All Combinations)
```sql
INSERT INTO dim_order_flags
SELECT ROW_NUMBER() OVER (ORDER BY g.v, e.v, p.v, s.v),
       g.v, e.v, p.v, s.v
FROM (VALUES (0),(1)) g(v)
CROSS JOIN (VALUES (0),(1)) e(v)
CROSS JOIN (VALUES ('Credit'),('Debit'),('PayPal')) p(v)
CROSS JOIN (VALUES ('Standard'),('Express'),('Overnight')) s(v);
```

## Degenerate Dimension

**Definition**: Dimension key in fact table with no separate dimension table

**Examples**: Order Number, Invoice Number, Transaction ID

```sql
CREATE TABLE fact_sales (
    ...
    order_number VARCHAR(30),      -- Degenerate dimension
    invoice_number VARCHAR(30),    -- Degenerate dimension
    line_item_number INT,          -- Degenerate dimension
    ...
);

-- Index for lookups
CREATE INDEX ix_fact_sales_order ON fact_sales (order_number);
```

**When to Use**:
- No additional attributes for the ID
- Used primarily for drill-through to source system
- One-to-one relationship with fact rows

## Role-Playing Dimension

**Definition**: Single dimension used multiple times with different meanings

### Example: Date Dimension in Multiple Roles
```sql
-- Single physical table
CREATE TABLE dim_date (date_key INT PRIMARY KEY, ...);

-- Views for each role
CREATE VIEW dim_order_date AS
SELECT date_key AS order_date_key, full_date AS order_date, ...
FROM dim_date;

CREATE VIEW dim_ship_date AS
SELECT date_key AS ship_date_key, full_date AS ship_date, ...
FROM dim_date;

CREATE VIEW dim_delivery_date AS
SELECT date_key AS delivery_date_key, full_date AS delivery_date, ...
FROM dim_date;

-- Fact table with multiple date roles
CREATE TABLE fact_orders (
    order_date_key INT,
    ship_date_key INT,
    delivery_date_key INT,
    ...
);
```

## Bridge Table (Many-to-Many)

**Purpose**: Handle M:M relationships in dimensional model

### Example: Patient-Diagnosis (M:M)
```sql
-- Diagnosis dimension
CREATE TABLE dim_diagnosis (
    diagnosis_key INT PRIMARY KEY,
    diagnosis_code VARCHAR(10),
    diagnosis_name VARCHAR(200)
);

-- Bridge table
CREATE TABLE bridge_patient_diagnosis (
    patient_diagnosis_group_key INT,
    diagnosis_key INT,
    weight_factor DECIMAL(5,4) DEFAULT 1.0,
    is_primary BIT DEFAULT 0,
    PRIMARY KEY (patient_diagnosis_group_key, diagnosis_key)
);

-- Fact references bridge group
CREATE TABLE fact_patient_visits (
    visit_key INT PRIMARY KEY,
    patient_diagnosis_group_key INT,
    ...
);
```

### Query with Weight Factor
```sql
-- Distribute charges across diagnoses
SELECT 
    d.diagnosis_name,
    SUM(f.total_charges * b.weight_factor) AS allocated_charges
FROM fact_patient_visits f
JOIN bridge_patient_diagnosis b 
    ON f.patient_diagnosis_group_key = b.patient_diagnosis_group_key
JOIN dim_diagnosis d ON b.diagnosis_key = d.diagnosis_key
GROUP BY d.diagnosis_name;
```

---

# 6. Fact Table Patterns

## Factless Fact Table

### Type 1: Coverage/Eligibility
**Purpose**: Track what CAN happen (not what DID happen)

```sql
-- Which products are authorized at which stores?
CREATE TABLE fact_product_store_coverage (
    product_key INT,
    store_key INT,
    effective_date_key INT,
    expiration_date_key INT,
    PRIMARY KEY (product_key, store_key, effective_date_key)
);

-- Find products authorized but never sold
SELECT p.product_name, s.store_name
FROM fact_product_store_coverage c
JOIN dim_product p ON c.product_key = p.product_key
JOIN dim_store s ON c.store_key = s.store_key
WHERE NOT EXISTS (
    SELECT 1 FROM fact_sales f 
    WHERE f.product_key = c.product_key 
      AND f.store_key = c.store_key
);
```

### Type 2: Event Tracking
**Purpose**: Track events without measures

```sql
-- Student attendance
CREATE TABLE fact_attendance (
    date_key INT,
    student_key INT,
    class_key INT,
    period_key INT,
    PRIMARY KEY (date_key, student_key, class_key, period_key)
);

-- Find students who missed class
SELECT s.student_name, d.full_date, c.class_name
FROM dim_student s
CROSS JOIN dim_date d
CROSS JOIN dim_class c
LEFT JOIN fact_attendance a 
    ON s.student_key = a.student_key 
   AND d.date_key = a.date_key
   AND c.class_key = a.class_key
WHERE a.date_key IS NULL
  AND d.is_weekday = 1;
```

## Accumulating Snapshot Fact

**Purpose**: Track lifecycle of a process with multiple milestone dates

```sql
CREATE TABLE fact_order_lifecycle (
    order_key INT PRIMARY KEY,
    customer_key INT,
    product_key INT,
    
    -- Milestone dates (role-playing)
    order_date_key INT,
    payment_date_key INT,
    ship_date_key INT,
    delivery_date_key INT,
    
    -- Lag measures (calculated)
    days_to_payment INT,
    days_to_ship INT,
    days_to_deliver INT,
    total_days INT,
    
    -- Current status
    current_status VARCHAR(20),
    
    -- Measures
    order_amount DECIMAL(12,2)
);
```

**Update Pattern**: Row is updated as milestones are reached

## Periodic Snapshot Fact

**Purpose**: Capture state at regular intervals

```sql
CREATE TABLE fact_account_monthly (
    snapshot_date_key INT,
    account_key INT,
    customer_key INT,
    balance DECIMAL(18,2),
    deposits_mtd DECIMAL(18,2),
    withdrawals_mtd DECIMAL(18,2),
    interest_mtd DECIMAL(18,2),
    PRIMARY KEY (snapshot_date_key, account_key)
);
```

**Note**: Semi-additive measures (balance) - don't sum across time!

---

# 7. ETL/ELT Patterns

## ETL vs ELT

| Aspect | ETL | ELT |
|--------|-----|-----|
| **Transform Location** | ETL Server | Target Database |
| **Best For** | On-premises, complex transforms | Cloud, big data |
| **Scalability** | Limited by ETL server | Scales with target |
| **Latency** | Higher | Lower |
| **Tools** | SSIS, Informatica, Talend | dbt, Spark, cloud-native |

## Staging Layer Pattern

```sql
-- Raw staging (preserve source exactly)
CREATE TABLE stg_raw_customers (
    raw_id INT IDENTITY(1,1),
    load_timestamp DATETIME DEFAULT GETDATE(),
    source_file VARCHAR(200),
    -- All columns as VARCHAR
    customer_id VARCHAR(MAX),
    customer_name VARCHAR(MAX),
    email VARCHAR(MAX),
    balance VARCHAR(MAX)
);

-- Cleaned staging (typed, validated)
CREATE TABLE stg_clean_customers (
    staging_id INT IDENTITY(1,1),
    source_raw_id INT,
    customer_id VARCHAR(20) NOT NULL,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    balance DECIMAL(15,2),
    is_valid BIT DEFAULT 1,
    validation_errors VARCHAR(500)
);
```

## Incremental Load Pattern

### Watermark-Based
```sql
CREATE TABLE etl_watermarks (
    table_name VARCHAR(100) PRIMARY KEY,
    last_load_timestamp DATETIME,
    last_load_id BIGINT
);

-- Incremental extract
SELECT *
FROM source_orders
WHERE modified_timestamp > @last_watermark
  AND modified_timestamp <= @current_timestamp;

-- Update watermark after successful load
UPDATE etl_watermarks 
SET last_load_timestamp = @current_timestamp
WHERE table_name = 'orders';
```

### Hash-Based Change Detection
```sql
-- Add hash column to dimension
ALTER TABLE dim_customer ADD row_hash VARBINARY(32);

-- Calculate hash
UPDATE dim_customer
SET row_hash = HASHBYTES('SHA2_256', 
    CONCAT(customer_name, '|', email, '|', address));

-- Detect changes
SELECT s.*,
    CASE 
        WHEN d.customer_key IS NULL THEN 'INSERT'
        WHEN d.row_hash <> HASHBYTES('SHA2_256', 
            CONCAT(s.customer_name, '|', s.email, '|', s.address))
        THEN 'UPDATE'
        ELSE 'NO_CHANGE'
    END AS change_type
FROM stg_customers s
LEFT JOIN dim_customer d 
    ON s.customer_id = d.customer_id 
   AND d.is_current = 1;
```

## MERGE Pattern (Upsert)

```sql
MERGE dim_customer AS target
USING stg_customers AS source
ON target.customer_id = source.customer_id AND target.is_current = 1
WHEN MATCHED AND (
    target.customer_name <> source.customer_name OR
    target.email <> source.email
) THEN 
    UPDATE SET 
        customer_name = source.customer_name,
        email = source.email,
        modified_date = GETDATE()
WHEN NOT MATCHED BY TARGET THEN
    INSERT (customer_id, customer_name, email, created_date)
    VALUES (source.customer_id, source.customer_name, source.email, GETDATE());
```

## Late-Arriving Data Handling

### Late-Arriving Dimension
```sql
-- 1. Create inferred/placeholder record
INSERT INTO dim_customer (customer_key, customer_id, customer_name, is_inferred)
VALUES (-1, 'UNKNOWN', 'Unknown Customer', 1);

-- 2. Load fact with placeholder
INSERT INTO fact_sales (customer_key, ...)
SELECT ISNULL(d.customer_key, -1), ...  -- Use -1 if not found
FROM stg_sales s
LEFT JOIN dim_customer d ON s.customer_id = d.customer_id;

-- 3. Later: Update inferred records when dimension arrives
UPDATE d
SET customer_name = s.customer_name,
    email = s.email,
    is_inferred = 0
FROM dim_customer d
JOIN stg_customers s ON d.customer_id = s.customer_id
WHERE d.is_inferred = 1;
```

---

# 8. Data Vault Modeling

## Data Vault Components

```
┌─────────────────────────────────────────────────────┐
│                   DATA VAULT 2.0                     │
├─────────────────────────────────────────────────────┤
│  ┌─────────┐    ┌─────────┐    ┌─────────────────┐ │
│  │   HUB   │────│  LINK   │────│   SATELLITE     │ │
│  │ (Entity)│    │(Relation)    │ (Attributes)    │ │
│  └─────────┘    └─────────┘    └─────────────────┘ │
└─────────────────────────────────────────────────────┘
```

## Hub (Business Entity)

**Purpose**: Store unique business keys

```sql
CREATE TABLE hub_customer (
    hub_customer_hk BINARY(32) PRIMARY KEY,  -- Hash key
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL,
    customer_id VARCHAR(20) NOT NULL         -- Business key
);

-- Hash key calculation
INSERT INTO hub_customer (hub_customer_hk, load_date, record_source, customer_id)
SELECT 
    HASHBYTES('SHA2_256', UPPER(TRIM(customer_id))),
    GETDATE(),
    'CRM_SYSTEM',
    customer_id
FROM source_customers
WHERE NOT EXISTS (
    SELECT 1 FROM hub_customer h 
    WHERE h.customer_id = source_customers.customer_id
);
```

## Link (Relationship)

**Purpose**: Store relationships between hubs

```sql
CREATE TABLE link_customer_order (
    link_customer_order_hk BINARY(32) PRIMARY KEY,
    hub_customer_hk BINARY(32) NOT NULL,
    hub_order_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL
);
```

## Satellite (Descriptive Attributes)

**Purpose**: Store descriptive attributes with history

```sql
CREATE TABLE sat_customer_details (
    hub_customer_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    load_end_date DATETIME,                  -- For current record: NULL
    record_source VARCHAR(100) NOT NULL,
    hash_diff BINARY(32) NOT NULL,           -- Detect changes
    -- Descriptive attributes
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    address VARCHAR(200),
    PRIMARY KEY (hub_customer_hk, load_date)
);

-- Hash diff for change detection
HASHBYTES('SHA2_256', CONCAT(
    ISNULL(customer_name,''), '|',
    ISNULL(email,''), '|',
    ISNULL(phone,''), '|',
    ISNULL(address,'')
))
```

## Data Vault Loading Pattern

```sql
-- 1. Load Hub (insert new business keys only)
INSERT INTO hub_customer (hub_customer_hk, load_date, record_source, customer_id)
SELECT HASHBYTES('SHA2_256', customer_id), GETDATE(), 'SOURCE', customer_id
FROM staging.customers s
WHERE NOT EXISTS (
    SELECT 1 FROM hub_customer h WHERE h.customer_id = s.customer_id
);

-- 2. Load Satellite (insert if changed)
INSERT INTO sat_customer_details (hub_customer_hk, load_date, hash_diff, ...)
SELECT h.hub_customer_hk, GETDATE(), 
       HASHBYTES('SHA2_256', CONCAT(...)), ...
FROM staging.customers s
JOIN hub_customer h ON s.customer_id = h.customer_id
LEFT JOIN sat_customer_details sat 
    ON h.hub_customer_hk = sat.hub_customer_hk 
   AND sat.load_end_date IS NULL
WHERE sat.hub_customer_hk IS NULL  -- New
   OR sat.hash_diff <> HASHBYTES('SHA2_256', CONCAT(...));  -- Changed
```

---

# 9. Architecture Patterns

## Inmon (Corporate Information Factory)

```
Source → ETL → Enterprise DWH (3NF) → Data Marts → Reporting
```

**Characteristics**:
- Top-down approach
- Normalized enterprise DWH
- Dimensional data marts
- Single source of truth

## Kimball (Dimensional Bus)

```
Source → ETL → Staging → Dimensional Data Marts → Reporting
                              ↑
                    Conformed Dimensions (Bus)
```

**Characteristics**:
- Bottom-up approach
- Dimensional modeling throughout
- Conformed dimensions across subjects
- Faster time to value

## Data Vault

```
Source → RAW Vault → Business Vault → Information Marts → Reporting
         (Hubs)       (Derived)         (Dimensional)
         (Links)
         (Sats)
```

**Characteristics**:
- Hybrid approach
- Auditable, historized raw layer
- Flexible for changing requirements
- Parallel loading

## Lambda Architecture

```
┌─────────────────────────────────────────────┐
│              BATCH LAYER                     │
│  (Master Dataset - Complete, Accurate)      │
└─────────────────────┬───────────────────────┘
                      │
                      ▼
              ┌───────────────┐
              │ SERVING LAYER │
              │   (Queries)   │
              └───────────────┘
                      ▲
                      │
┌─────────────────────┴───────────────────────┐
│              SPEED LAYER                     │
│    (Real-time, Approximate, Recent)         │
└─────────────────────────────────────────────┘
```

**Use Case**: Combine batch accuracy with real-time speed

## Kappa Architecture

```
Source → Stream Processing → Serving Layer → Queries
              ↓
         Reprocessing (replay streams)
```

**Difference from Lambda**: Single stream processing path, no separate batch layer

---

# 10. Performance Optimization

## Indexing Strategies

### Columnstore Indexes (Fact Tables)
```sql
-- Best for analytical queries on large fact tables
CREATE CLUSTERED COLUMNSTORE INDEX cci_fact_sales
ON fact_sales;
```

### B-Tree Indexes (Dimension Tables)
```sql
-- Covering index for common queries
CREATE NONCLUSTERED INDEX ix_dim_product_category
ON dim_product (category, subcategory)
INCLUDE (product_name, brand, unit_price);

-- Filtered index for current records
CREATE NONCLUSTERED INDEX ix_dim_customer_current
ON dim_customer (customer_id)
WHERE is_current = 1;
```

## Partitioning

```sql
-- Partition by date (monthly)
CREATE PARTITION FUNCTION pf_monthly (INT)
AS RANGE RIGHT FOR VALUES (20240101, 20240201, 20240301, ...);

CREATE PARTITION SCHEME ps_monthly
AS PARTITION pf_monthly ALL TO ([PRIMARY]);

CREATE TABLE fact_sales (
    ...
    date_key INT NOT NULL
) ON ps_monthly(date_key);
```

**Benefits**:
- Partition elimination (query only relevant partitions)
- Faster data loads (partition switching)
- Easier archival (drop old partitions)

## Query Optimization Tips

### Do's
```sql
-- Specify columns (not SELECT *)
SELECT date_key, product_key, SUM(amount)
FROM fact_sales
GROUP BY date_key, product_key;

-- Use sargable predicates
WHERE date_key >= 20240101 AND date_key < 20240201

-- Use EXISTS for existence checks
WHERE EXISTS (SELECT 1 FROM dim_product p WHERE p.product_key = f.product_key)
```

### Don'ts
```sql
-- Avoid functions on indexed columns
WHERE YEAR(order_date) = 2024  -- Bad
WHERE order_date >= '2024-01-01' AND order_date < '2025-01-01'  -- Good

-- Avoid SELECT *
SELECT * FROM fact_sales  -- Bad

-- Avoid IN with large lists
WHERE product_key IN (SELECT ... FROM large_table)  -- Bad
```

## Aggregation Strategies

```sql
-- Pre-aggregated summary table
CREATE TABLE agg_daily_sales (
    date_key INT,
    product_key INT,
    store_key INT,
    total_quantity INT,
    total_sales DECIMAL(15,2),
    transaction_count INT,
    PRIMARY KEY (date_key, product_key, store_key)
);

-- Refresh procedure
CREATE PROCEDURE refresh_daily_agg
    @date_key INT
AS
BEGIN
    DELETE FROM agg_daily_sales WHERE date_key = @date_key;
    
    INSERT INTO agg_daily_sales
    SELECT date_key, product_key, store_key,
           SUM(quantity), SUM(sales_amount), COUNT(*)
    FROM fact_sales
    WHERE date_key = @date_key
    GROUP BY date_key, product_key, store_key;
END;
```

---

# 11. Data Quality & Governance

## Data Quality Dimensions

| Dimension | Definition | Check |
|-----------|------------|-------|
| **Completeness** | No missing values | NULL count |
| **Accuracy** | Values correct | Validation rules |
| **Consistency** | Same across systems | Cross-system comparison |
| **Timeliness** | Data is current | Freshness check |
| **Uniqueness** | No duplicates | Duplicate count |
| **Validity** | Values in expected range | Range/pattern checks |

## Data Quality Checks

```sql
-- Completeness
SELECT 
    'customer_name' AS column_name,
    COUNT(*) AS total,
    SUM(CASE WHEN customer_name IS NULL THEN 1 ELSE 0 END) AS nulls,
    SUM(CASE WHEN customer_name IS NULL THEN 1 ELSE 0 END) * 100.0 / COUNT(*) AS null_pct
FROM dim_customer;

-- Uniqueness
SELECT customer_id, COUNT(*) AS cnt
FROM dim_customer
WHERE is_current = 1
GROUP BY customer_id
HAVING COUNT(*) > 1;

-- Referential Integrity
SELECT f.*
FROM fact_sales f
LEFT JOIN dim_customer c ON f.customer_key = c.customer_key
WHERE c.customer_key IS NULL;

-- Range Check
SELECT *
FROM fact_sales
WHERE quantity < 0 OR sales_amount < 0;
```

## Audit Dimension

```sql
CREATE TABLE dim_audit (
    audit_key INT PRIMARY KEY,
    batch_id INT,
    load_start_time DATETIME,
    load_end_time DATETIME,
    source_system VARCHAR(100),
    source_file VARCHAR(500),
    record_count INT,
    etl_version VARCHAR(20),
    status VARCHAR(20)
);

-- Every fact row references audit
CREATE TABLE fact_sales (
    ...
    audit_key INT REFERENCES dim_audit(audit_key)
);
```

## Data Lineage Query

```sql
-- Track where data came from
SELECT 
    f.sales_key,
    a.source_system,
    a.source_file,
    a.load_start_time
FROM fact_sales f
JOIN dim_audit a ON f.audit_key = a.audit_key
WHERE f.sales_key = 12345;
```

---

# 12. SQL Reference

## Window Functions

```sql
-- Ranking
ROW_NUMBER() OVER (ORDER BY sales DESC)
RANK() OVER (PARTITION BY category ORDER BY sales DESC)
DENSE_RANK() OVER (ORDER BY sales DESC)
NTILE(4) OVER (ORDER BY sales)  -- Quartiles

-- Running Totals
SUM(amount) OVER (ORDER BY date ROWS UNBOUNDED PRECEDING)
SUM(amount) OVER (PARTITION BY customer ORDER BY date ROWS UNBOUNDED PRECEDING)

-- Moving Average
AVG(amount) OVER (ORDER BY date ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)

-- Year-over-Year
LAG(sales, 12) OVER (ORDER BY month_key)
sales - LAG(sales, 12) OVER (ORDER BY month_key) AS yoy_change

-- Percent of Total
amount / SUM(amount) OVER () * 100 AS pct_of_total
amount / SUM(amount) OVER (PARTITION BY category) * 100 AS pct_of_category
```

## Common Aggregations

```sql
-- Basic aggregations
SELECT 
    category,
    COUNT(*) AS count,
    SUM(amount) AS total,
    AVG(amount) AS average,
    MIN(amount) AS minimum,
    MAX(amount) AS maximum,
    STDEV(amount) AS std_dev
FROM fact_sales
GROUP BY category;

-- Conditional aggregation
SELECT 
    store_key,
    COUNT(CASE WHEN channel = 'Online' THEN 1 END) AS online_orders,
    COUNT(CASE WHEN channel = 'Store' THEN 1 END) AS store_orders,
    SUM(CASE WHEN is_returned = 1 THEN amount END) AS returns_amount
FROM fact_sales
GROUP BY store_key;
```

## Pivoting

```sql
-- Manual pivot
SELECT 
    product_category,
    SUM(CASE WHEN year = 2023 THEN sales END) AS sales_2023,
    SUM(CASE WHEN year = 2024 THEN sales END) AS sales_2024
FROM sales_by_year
GROUP BY product_category;

-- SQL Server PIVOT
SELECT *
FROM (SELECT category, year, sales FROM sales_data) src
PIVOT (SUM(sales) FOR year IN ([2023], [2024])) pvt;
```

## Date Calculations

```sql
-- Date parts
YEAR(order_date), MONTH(order_date), DAY(order_date)
DATEPART(QUARTER, order_date)
DATENAME(WEEKDAY, order_date)

-- Date arithmetic
DATEADD(DAY, 7, order_date)      -- Add 7 days
DATEADD(MONTH, -1, order_date)   -- Subtract 1 month
DATEDIFF(DAY, order_date, ship_date)  -- Days between

-- First/last of period
DATEADD(MONTH, DATEDIFF(MONTH, 0, order_date), 0)  -- First of month
EOMONTH(order_date)  -- Last of month
```

---

# 13. Industry Data Models

## Retail

### Key Entities
- Customer, Product, Store, Promotion, Transaction, Inventory

### Common Facts
- fact_sales (transactions)
- fact_inventory (daily snapshot)
- fact_returns
- fact_promotions

### Key Metrics
- Sales revenue, Units sold, Basket size
- Inventory turnover, Stock-outs
- Return rate, Customer lifetime value

## Healthcare

### Key Entities
- Patient, Provider, Encounter, Diagnosis, Procedure, Payer

### Common Facts
- fact_encounter (accumulating snapshot)
- fact_claims
- fact_quality_metrics (periodic snapshot)

### Key Metrics
- Length of stay, Readmission rate
- Case mix index, Cost per case
- Patient satisfaction

## Finance

### Key Entities
- Customer, Account, Transaction, Product, Branch

### Common Facts
- fact_transactions
- fact_account_balance (periodic snapshot)
- fact_credit_exposure (daily snapshot)

### Key Metrics
- Account balance, Transaction volume
- Risk-weighted assets, Expected loss
- Net interest margin

## E-Commerce

### Key Entities
- Customer, Product, Order, Session, Campaign

### Common Facts
- fact_orders
- fact_clickstream
- fact_cart_abandonment

### Key Metrics
- Conversion rate, Average order value
- Cart abandonment rate
- Customer acquisition cost

---

# 14. Quick Reference Tables

## SCD Type Summary

| Type | Action | History | Columns Added | When to Use |
|------|--------|---------|---------------|-------------|
| 0 | None | N/A | None | Fixed values |
| 1 | Overwrite | None | None | Corrections |
| 2 | New Row | Full | effective_from, effective_to, is_current | Audit |
| 3 | New Column | One prior | previous_value, change_date | Limited tracking |
| 4 | Mini-dim | Full (separate) | None (new table) | Rapid changes |
| 6 | Hybrid | Full + current | All of above | Complex needs |

## Fact Table Type Summary

| Type | Grain | Updates | Example |
|------|-------|---------|---------|
| Transaction | Event | Insert-only | Sales |
| Periodic Snapshot | Time period | Insert-only | Daily balance |
| Accumulating Snapshot | Process | Updates until complete | Order lifecycle |
| Factless | Event | Insert-only | Attendance |

## Architecture Pattern Summary

| Pattern | Approach | DWH Design | Speed | Flexibility |
|---------|----------|------------|-------|-------------|
| Inmon | Top-down | 3NF → Marts | Slower | Less flexible |
| Kimball | Bottom-up | Dimensional | Faster | Less flexible |
| Data Vault | Hybrid | Hub/Link/Sat | Medium | High |
| Lambda | Batch + Real-time | Both | Real-time available | Complex |
| Kappa | Stream-only | Stream | Real-time | Simpler than Lambda |

## Key Formulas

```sql
-- Inventory Turnover
Cost of Goods Sold / Average Inventory

-- Gross Margin
(Revenue - Cost) / Revenue * 100

-- Customer Lifetime Value
Average Purchase Value × Purchase Frequency × Customer Lifespan

-- Year-over-Year Growth
(Current Year - Prior Year) / Prior Year * 100

-- Moving Average (7-day)
AVG(value) OVER (ORDER BY date ROWS 6 PRECEDING)
```

## Common SQL Patterns

```sql
-- Duplicate detection
SELECT key_columns, COUNT(*)
FROM table
GROUP BY key_columns
HAVING COUNT(*) > 1;

-- Gap detection
SELECT a.id + 1 AS gap_start, MIN(b.id) - 1 AS gap_end
FROM table a, table b
WHERE a.id < b.id
GROUP BY a.id
HAVING a.id + 1 < MIN(b.id);

-- Running total
SUM(amount) OVER (ORDER BY date ROWS UNBOUNDED PRECEDING)

-- Percent of total
amount * 100.0 / SUM(amount) OVER ()

-- First/Last value per group
FIRST_VALUE(amount) OVER (PARTITION BY category ORDER BY date)
LAST_VALUE(amount) OVER (PARTITION BY category ORDER BY date 
    ROWS BETWEEN UNBOUNDED PRECEDING AND UNBOUNDED FOLLOWING)
```

---

## Abbreviations & Glossary

| Term | Full Form | Definition |
|------|-----------|------------|
| CDC | Change Data Capture | Track and capture data changes |
| DDL | Data Definition Language | CREATE, ALTER, DROP |
| DML | Data Manipulation Language | INSERT, UPDATE, DELETE |
| DWH | Data Warehouse | Analytical data repository |
| ELT | Extract, Load, Transform | Load first, transform in target |
| ETL | Extract, Transform, Load | Transform before loading |
| FK | Foreign Key | References primary key |
| MDM | Master Data Management | Single source of truth for entities |
| OLAP | Online Analytical Processing | Read-heavy analytics |
| OLTP | Online Transaction Processing | Write-heavy transactions |
| PK | Primary Key | Unique row identifier |
| SCD | Slowly Changing Dimension | Track dimension changes |
| SK | Surrogate Key | Artificial generated key |
| NK | Natural Key | Business meaningful key |

---

*Use this cheatsheet as a quick reference while working through the DWH assignments. For detailed implementations, refer to the assignment file.*
