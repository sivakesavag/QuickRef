# Data Warehousing & Data Modelling Mastery Curriculum

> **A comprehensive progression from Beginner to Expert level with hands-on assignments**

---

## Table of Contents

1. [Curriculum Overview](#curriculum-overview)
2. [Level 1: Beginner](#level-1-beginner-foundations)
3. [Level 2: Intermediate](#level-2-intermediate-dimensional-modeling)
4. [Level 3: Advanced](#level-3-advanced-architectures)
5. [Level 4: Expert](#level-4-expert-enterprise-solutions)
6. [Appendices](#appendices)

---

## Curriculum Overview

### Learning Objectives
- Master conceptual, logical, and physical data modeling
- Design star, snowflake, and galaxy schemas
- Implement ETL/ELT pipelines with best practices
- Build enterprise-grade data warehouse solutions
- Apply data governance and quality frameworks

### Skill Progression

| Level | Focus | Assignments | Duration |
|-------|-------|-------------|----------|
| Beginner | Foundations, ER diagrams, Normalization | 15 | 4-6 weeks |
| Intermediate | Dimensional modeling, ETL basics | 15 | 6-8 weeks |
| Advanced | Complex architectures, Optimization | 15 | 8-10 weeks |
| Expert | Enterprise solutions, Real-world scenarios | 15 | 10-12 weeks |

### Detailed Topics by Level

| Level | Assignments | Key Topics Covered |
|-------|-------------|-------------------|
| **Beginner** | B1-B15 | ER diagrams, Normalization (1NF-BCNF), Natural vs Surrogate keys, Basic Star Schema, Fact/Dimension tables, Data profiling, Basic ETL, Data quality rules, OLAP queries |
| **Intermediate** | I1-I15 | SCD Types 1, 2, 3, 6, Snowflake/Galaxy schemas, Junk/Degenerate dimensions, Bridge tables, Role-playing dimensions, Factless facts, ETL staging layers, Incremental loads, Conformed dimensions, Audit dimensions |
| **Advanced** | A1-A15 | Data Vault 2.0 (Hubs, Links, Satellites), Architecture patterns (Inmon/Kimball/Lambda/Kappa), Late-arriving data, Aggregates, Partitioning, Indexing, CDC, Performance optimization, Temporal tables, Metadata management |
| **Expert** | E1-E15 | Industry scenarios (Retail, Healthcare, Finance, E-commerce), Cloud DWH architecture, Data governance, MDM integration, Self-service analytics, Data Mesh, Reverse engineering, DR/HA, Security, DataOps/CI-CD |

### Each Assignment Includes
- ✅ Business context and requirements
- ✅ DDL scripts with SQL examples
- ✅ Sample queries and data patterns
- ✅ Deliverables checklist
- ✅ Common pitfalls and design considerations

### Prerequisites
- Basic SQL knowledge (SELECT, INSERT, UPDATE, DELETE)
- Understanding of relational database concepts
- Familiarity with database design principles

---


# Level 1: Beginner (Foundations)

## Learning Goals
- Understand OLTP vs OLAP systems
- Create Entity-Relationship diagrams
- Apply normalization rules (1NF to BCNF)
- Design basic database schemas
- Write foundational SQL DDL/DML

---

## Assignment B1: Introduction to Data Warehousing Concepts

### Business Context
A startup wants to understand why they need a separate analytical system from their transactional database.

### Objectives
1. Define data warehousing and its purpose
2. Compare OLTP vs OLAP characteristics
3. Identify when a data warehouse is needed
4. Explain the key components of a DWH

### Deliverables
- [ ] Written report (2-3 pages) covering:
  - Definition and purpose of data warehousing
  - OLTP vs OLAP comparison table (10+ characteristics)
  - Business scenarios requiring DWH
  - Component diagram of typical DWH architecture

### Success Criteria
- Correctly identifies 10+ differences between OLTP/OLAP
- Provides 5+ valid business use cases
- Accurately describes all major DWH components

### Key Concepts
```
OLTP Characteristics:
- Transaction-focused
- Current data
- Normalized design
- Many concurrent users
- Simple queries
- High write frequency

OLAP Characteristics:
- Analysis-focused
- Historical data
- Denormalized design
- Few analytical users
- Complex queries
- Read-heavy
```

---

## Assignment B2: Entity-Relationship Diagram Fundamentals

### Business Context
A local bookstore needs to track books, authors, customers, and sales.

### Objectives
1. Identify entities and relationships
2. Define cardinality (1:1, 1:M, M:M)
3. Create an ER diagram with proper notation
4. Identify primary and foreign keys

### Requirements
**Entities to model:**
- Books (ISBN, title, price, publication_date)
- Authors (author_id, name, nationality)
- Customers (customer_id, name, email, phone)
- Orders (order_id, order_date, total_amount)
- Publishers (publisher_id, name, country)

**Relationships:**
- A book can have multiple authors
- An author can write multiple books
- A customer can place multiple orders
- An order can contain multiple books
- A book belongs to one publisher

### Deliverables
- [ ] ER diagram using Chen or Crow's Foot notation
- [ ] Entity definitions with attributes
- [ ] Relationship descriptions with cardinality
- [ ] DDL scripts to create tables

### Sample DDL
```sql
CREATE TABLE publishers (
    publisher_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    country VARCHAR(50)
);

CREATE TABLE books (
    isbn VARCHAR(13) PRIMARY KEY,
    title VARCHAR(200) NOT NULL,
    price DECIMAL(10,2),
    publication_date DATE,
    publisher_id INT REFERENCES publishers(publisher_id)
);

CREATE TABLE authors (
    author_id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    nationality VARCHAR(50)
);

CREATE TABLE book_authors (
    isbn VARCHAR(13) REFERENCES books(isbn),
    author_id INT REFERENCES authors(author_id),
    PRIMARY KEY (isbn, author_id)
);
```

### Common Pitfalls
- Missing junction tables for M:M relationships
- Incorrect cardinality notation
- Not identifying all foreign keys
- Missing NOT NULL constraints on required fields

---

## Assignment B3: First Normal Form (1NF)

### Business Context
A music streaming service stores playlist data in a denormalized format causing data anomalies.

### Objectives
1. Identify 1NF violations
2. Apply 1NF rules to eliminate repeating groups
3. Ensure atomic values in all columns

### Problem Data
```
| playlist_id | playlist_name | songs                          | artists              |
|-------------|---------------|--------------------------------|----------------------|
| 1           | Road Trip     | Song1, Song2, Song3            | Artist1, Artist2     |
| 2           | Workout       | Song4, Song5                   | Artist3              |
| 3           | Chill         | Song1, Song6, Song7, Song8     | Artist1, Artist4     |
```

### Deliverables
- [ ] Identify all 1NF violations in the sample data
- [ ] Redesigned schema in 1NF
- [ ] DDL scripts for normalized tables
- [ ] Sample INSERT statements

### Success Criteria
- No repeating groups
- All values are atomic
- Primary key defined for each table
- Sample data correctly migrated

### Solution Approach
```sql
-- Normalized tables
CREATE TABLE playlists (
    playlist_id INT PRIMARY KEY,
    playlist_name VARCHAR(100) NOT NULL
);

CREATE TABLE songs (
    song_id INT PRIMARY KEY,
    song_name VARCHAR(200) NOT NULL
);

CREATE TABLE artists (
    artist_id INT PRIMARY KEY,
    artist_name VARCHAR(100) NOT NULL
);

CREATE TABLE playlist_songs (
    playlist_id INT REFERENCES playlists(playlist_id),
    song_id INT REFERENCES songs(song_id),
    track_order INT,
    PRIMARY KEY (playlist_id, song_id)
);

CREATE TABLE song_artists (
    song_id INT REFERENCES songs(song_id),
    artist_id INT REFERENCES artists(artist_id),
    PRIMARY KEY (song_id, artist_id)
);
```

---

## Assignment B4: Second Normal Form (2NF)

### Business Context
An e-commerce company has order data with partial dependencies causing update anomalies.

### Objectives
1. Identify partial dependencies
2. Eliminate partial dependencies
3. Ensure full functional dependency on primary key

### Problem Data
```
Table: order_items (composite key: order_id, product_id)

| order_id | product_id | product_name | product_category | quantity | unit_price |
|----------|------------|--------------|------------------|----------|------------|
| 1001     | P101       | Laptop       | Electronics      | 2        | 999.99     |
| 1001     | P102       | Mouse        | Electronics      | 3        | 29.99      |
| 1002     | P101       | Laptop       | Electronics      | 1        | 999.99     |
```

### Issues to Identify
- `product_name` depends only on `product_id` (partial dependency)
- `product_category` depends only on `product_id` (partial dependency)
- `unit_price` could depend only on `product_id`

### Deliverables
- [ ] Document all partial dependencies
- [ ] Redesigned schema in 2NF
- [ ] DDL scripts with proper constraints
- [ ] Data migration strategy

### Normalized Solution
```sql
CREATE TABLE products (
    product_id VARCHAR(10) PRIMARY KEY,
    product_name VARCHAR(100) NOT NULL,
    product_category VARCHAR(50),
    unit_price DECIMAL(10,2)
);

CREATE TABLE order_items (
    order_id INT,
    product_id VARCHAR(10) REFERENCES products(product_id),
    quantity INT NOT NULL,
    line_price DECIMAL(10,2),  -- quantity * unit_price at time of order
    PRIMARY KEY (order_id, product_id)
);
```

---

## Assignment B5: Third Normal Form (3NF)

### Business Context
A hospital management system has transitive dependencies in patient records.

### Objectives
1. Identify transitive dependencies
2. Eliminate transitive dependencies
3. Ensure all non-key attributes depend only on the primary key

### Problem Data
```
Table: patient_records

| patient_id | patient_name | doctor_id | doctor_name | department_id | department_name |
|------------|--------------|-----------|-------------|---------------|-----------------|
| P001       | John Smith   | D101      | Dr. Jones   | DEPT01        | Cardiology      |
| P002       | Jane Doe     | D101      | Dr. Jones   | DEPT01        | Cardiology      |
| P003       | Bob Wilson   | D102      | Dr. Smith   | DEPT02        | Neurology       |
```

### Transitive Dependencies to Identify
- `doctor_name` → depends on `doctor_id` (not on `patient_id`)
- `department_name` → depends on `department_id`
- `department_id` → depends on `doctor_id`

### Deliverables
- [ ] Document all transitive dependencies
- [ ] Normalized schema in 3NF
- [ ] ER diagram showing new structure
- [ ] DDL scripts with referential integrity

### Solution
```sql
CREATE TABLE departments (
    department_id VARCHAR(10) PRIMARY KEY,
    department_name VARCHAR(100) NOT NULL
);

CREATE TABLE doctors (
    doctor_id VARCHAR(10) PRIMARY KEY,
    doctor_name VARCHAR(100) NOT NULL,
    department_id VARCHAR(10) REFERENCES departments(department_id)
);

CREATE TABLE patients (
    patient_id VARCHAR(10) PRIMARY KEY,
    patient_name VARCHAR(100) NOT NULL,
    primary_doctor_id VARCHAR(10) REFERENCES doctors(doctor_id)
);
```

---

## Assignment B6: Boyce-Codd Normal Form (BCNF)

### Business Context
A university course scheduling system has overlapping candidate keys causing anomalies.

### Objectives
1. Understand difference between 3NF and BCNF
2. Identify BCNF violations
3. Decompose tables to achieve BCNF

### Problem Data
```
Table: course_assignments
Candidate Keys: (student_id, course_id) and (student_id, professor_id)

| student_id | course_id | professor_id | room_number |
|------------|-----------|--------------|-------------|
| S001       | CS101     | P001         | R101        |
| S002       | CS101     | P001         | R101        |
| S001       | CS102     | P002         | R102        |
| S003       | CS101     | P001         | R101        |
```

**Functional Dependencies:**
- professor_id → course_id (A professor teaches only one course)
- course_id → room_number (Each course has a dedicated room)

### BCNF Violation
- `professor_id → course_id` violates BCNF because professor_id is not a superkey

### Deliverables
- [ ] Identify all functional dependencies
- [ ] Document BCNF violations
- [ ] Decomposed schema in BCNF
- [ ] Proof that decomposition is lossless

### Solution
```sql
-- Decomposed tables in BCNF
CREATE TABLE professor_courses (
    professor_id VARCHAR(10) PRIMARY KEY,
    course_id VARCHAR(10) NOT NULL
);

CREATE TABLE course_rooms (
    course_id VARCHAR(10) PRIMARY KEY,
    room_number VARCHAR(10) NOT NULL
);

CREATE TABLE student_professors (
    student_id VARCHAR(10),
    professor_id VARCHAR(10) REFERENCES professor_courses(professor_id),
    PRIMARY KEY (student_id, professor_id)
);
```

---

## Assignment B7: Natural Keys vs Surrogate Keys

### Business Context
A retail company is designing a new inventory system and must decide on key strategies.

### Objectives
1. Understand pros and cons of each key type
2. Identify when to use natural vs surrogate keys
3. Implement both approaches

### Scenarios to Analyze

**Scenario A: Product Table**
```sql
-- Natural Key Approach
CREATE TABLE products_natural (
    sku VARCHAR(20) PRIMARY KEY,  -- SKU as natural key
    product_name VARCHAR(200),
    unit_price DECIMAL(10,2)
);

-- Surrogate Key Approach
CREATE TABLE products_surrogate (
    product_id INT IDENTITY(1,1) PRIMARY KEY,  -- Auto-generated surrogate
    sku VARCHAR(20) UNIQUE NOT NULL,
    product_name VARCHAR(200),
    unit_price DECIMAL(10,2)
);
```

### Deliverables
- [ ] Comparison table: Natural vs Surrogate keys (10+ criteria)
- [ ] 5 scenarios where natural keys are preferred
- [ ] 5 scenarios where surrogate keys are preferred
- [ ] DDL examples for both approaches

### Comparison Criteria
| Criteria | Natural Key | Surrogate Key |
|----------|-------------|---------------|
| Meaningfulness | Business meaning | No meaning |
| Stability | May change | Never changes |
| Size | Variable | Fixed (usually INT) |
| Performance | Potentially slower | Faster joins |
| ETL Complexity | Simpler matching | Requires lookup |
| Storage | Variable | Consistent |

### Common Pitfalls
- Using SSN or email as natural keys (they can change)
- Not adding unique constraints when using surrogate keys
- Exposing surrogate keys to end users
- Not considering composite natural keys

---

## Assignment B8: Basic Star Schema Design

### Business Context
A small retail store wants to analyze daily sales by product, store, and time.

### Objectives
1. Understand star schema fundamentals
2. Identify facts and dimensions
3. Design a basic star schema
4. Write DDL for implementation

### Requirements
**Business Questions to Answer:**
- What are total sales by product category?
- Which store has the highest revenue?
- What are sales trends by month/quarter/year?
- Which products are top sellers?

### Deliverables
- [ ] Star schema diagram
- [ ] Fact table design with measures
- [ ] Dimension table designs
- [ ] DDL scripts
- [ ] Sample queries

### Schema Design
```sql
-- Dimension: Date
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,
    full_date DATE NOT NULL,
    day_of_week VARCHAR(10),
    day_of_month INT,
    month_number INT,
    month_name VARCHAR(20),
    quarter INT,
    year INT,
    is_weekend BIT,
    is_holiday BIT
);

-- Dimension: Product
CREATE TABLE dim_product (
    product_key INT PRIMARY KEY,
    product_id VARCHAR(20),
    product_name VARCHAR(200),
    category VARCHAR(100),
    subcategory VARCHAR(100),
    brand VARCHAR(100),
    unit_cost DECIMAL(10,2),
    unit_price DECIMAL(10,2)
);

-- Dimension: Store
CREATE TABLE dim_store (
    store_key INT PRIMARY KEY,
    store_id VARCHAR(10),
    store_name VARCHAR(100),
    city VARCHAR(50),
    state VARCHAR(50),
    country VARCHAR(50),
    region VARCHAR(50)
);

-- Fact: Sales
CREATE TABLE fact_sales (
    sales_key INT IDENTITY(1,1) PRIMARY KEY,
    date_key INT REFERENCES dim_date(date_key),
    product_key INT REFERENCES dim_product(product_key),
    store_key INT REFERENCES dim_store(store_key),
    quantity_sold INT,
    unit_price DECIMAL(10,2),
    total_amount DECIMAL(12,2),
    discount_amount DECIMAL(10,2),
    net_amount DECIMAL(12,2)
);
```

### Sample Analytical Queries
```sql
-- Sales by category
SELECT 
    p.category,
    SUM(f.net_amount) as total_sales,
    SUM(f.quantity_sold) as units_sold
FROM fact_sales f
JOIN dim_product p ON f.product_key = p.product_key
GROUP BY p.category
ORDER BY total_sales DESC;

-- Monthly sales trend
SELECT 
    d.year,
    d.month_name,
    SUM(f.net_amount) as monthly_sales
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
GROUP BY d.year, d.month_number, d.month_name
ORDER BY d.year, d.month_number;
```

---

## Assignment B9: Fact Table Types

### Business Context
An airline needs to track different types of business events including bookings, flights, and customer interactions.

### Objectives
1. Understand different fact table types
2. Design transaction, periodic, and accumulating snapshots
3. Choose appropriate fact type for scenarios

### Fact Table Types

**1. Transaction Fact Table**
```sql
-- Records individual transactions as they occur
CREATE TABLE fact_flight_bookings (
    booking_key INT PRIMARY KEY,
    date_key INT,
    customer_key INT,
    flight_key INT,
    booking_amount DECIMAL(10,2),
    seats_booked INT,
    booking_timestamp DATETIME
);
```

**2. Periodic Snapshot Fact Table**
```sql
-- Records state at regular intervals
CREATE TABLE fact_daily_flight_snapshot (
    snapshot_date_key INT,
    flight_key INT,
    total_seats INT,
    seats_booked INT,
    seats_available INT,
    booking_percentage DECIMAL(5,2),
    PRIMARY KEY (snapshot_date_key, flight_key)
);
```

**3. Accumulating Snapshot Fact Table**
```sql
-- Tracks lifecycle of a process
CREATE TABLE fact_booking_lifecycle (
    booking_key INT PRIMARY KEY,
    customer_key INT,
    flight_key INT,
    booking_date_key INT,
    payment_date_key INT,
    checkin_date_key INT,
    boarding_date_key INT,
    booking_amount DECIMAL(10,2),
    days_to_payment INT,
    days_to_checkin INT
);
```

### Deliverables
- [ ] Design all three fact types for airline scenario
- [ ] Document when to use each type
- [ ] DDL scripts for each
- [ ] Sample data and queries

### Decision Matrix
| Scenario | Recommended Fact Type |
|----------|----------------------|
| Individual sales transactions | Transaction |
| Daily inventory levels | Periodic Snapshot |
| Order fulfillment process | Accumulating Snapshot |
| Website clicks | Transaction |
| Monthly account balances | Periodic Snapshot |
| Loan application process | Accumulating Snapshot |

---

## Assignment B10: Dimension Table Design

### Business Context
Design comprehensive dimension tables for a retail analytics system.

### Objectives
1. Create rich dimension tables with hierarchies
2. Implement dimension attributes correctly
3. Understand role-playing dimensions

### Requirements

**Customer Dimension:**
```sql
CREATE TABLE dim_customer (
    customer_key INT PRIMARY KEY,
    customer_id VARCHAR(20) NOT NULL,
    -- Personal info
    first_name VARCHAR(50),
    last_name VARCHAR(50),
    full_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    -- Demographics
    birth_date DATE,
    age_group VARCHAR(20),
    gender VARCHAR(10),
    marital_status VARCHAR(20),
    -- Geographic hierarchy
    address_line1 VARCHAR(200),
    city VARCHAR(50),
    state VARCHAR(50),
    postal_code VARCHAR(20),
    country VARCHAR(50),
    region VARCHAR(50),
    -- Customer attributes
    customer_type VARCHAR(20),
    loyalty_tier VARCHAR(20),
    acquisition_date DATE,
    acquisition_channel VARCHAR(50),
    -- Metadata
    effective_date DATE,
    expiration_date DATE,
    is_current BIT
);
```

**Date Dimension:**
```sql
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,              -- YYYYMMDD format
    full_date DATE NOT NULL,
    -- Day attributes
    day_of_week INT,
    day_name VARCHAR(10),
    day_of_month INT,
    day_of_year INT,
    is_weekday BIT,
    is_weekend BIT,
    -- Week attributes
    week_of_year INT,
    week_of_month INT,
    -- Month attributes
    month_number INT,
    month_name VARCHAR(15),
    month_short_name VARCHAR(3),
    -- Quarter attributes
    quarter_number INT,
    quarter_name VARCHAR(10),
    -- Year attributes
    year_number INT,
    fiscal_year INT,
    fiscal_quarter INT,
    -- Special flags
    is_holiday BIT,
    holiday_name VARCHAR(50),
    is_last_day_of_month BIT,
    is_last_day_of_quarter BIT
);
```

### Deliverables
- [ ] Customer dimension with 20+ attributes
- [ ] Date dimension covering 10 years
- [ ] Product dimension with hierarchy
- [ ] Script to populate date dimension

### Date Dimension Population Script
```sql
-- Generate date dimension for 10 years
DECLARE @StartDate DATE = '2020-01-01';
DECLARE @EndDate DATE = '2030-12-31';
DECLARE @CurrentDate DATE = @StartDate;

WHILE @CurrentDate <= @EndDate
BEGIN
    INSERT INTO dim_date (
        date_key,
        full_date,
        day_of_week,
        day_name,
        day_of_month,
        month_number,
        month_name,
        quarter_number,
        year_number,
        is_weekend
    )
    VALUES (
        CONVERT(INT, FORMAT(@CurrentDate, 'yyyyMMdd')),
        @CurrentDate,
        DATEPART(WEEKDAY, @CurrentDate),
        DATENAME(WEEKDAY, @CurrentDate),
        DAY(@CurrentDate),
        MONTH(@CurrentDate),
        DATENAME(MONTH, @CurrentDate),
        DATEPART(QUARTER, @CurrentDate),
        YEAR(@CurrentDate),
        CASE WHEN DATEPART(WEEKDAY, @CurrentDate) IN (1, 7) THEN 1 ELSE 0 END
    );
    SET @CurrentDate = DATEADD(DAY, 1, @CurrentDate);
END;
```

---

## Assignment B11: Data Profiling Basics

### Business Context
A company is migrating data from a legacy system and needs to understand data quality before designing the warehouse.

### Objectives
1. Perform column-level profiling
2. Identify data quality issues
3. Document data patterns and anomalies

### Sample Source Data
```sql
CREATE TABLE source_customers (
    cust_id VARCHAR(20),
    cust_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(30),
    reg_date VARCHAR(20),
    status VARCHAR(10),
    balance DECIMAL(15,2)
);

-- Sample profiling queries
-- Null analysis
SELECT 
    'cust_id' as column_name,
    COUNT(*) as total_rows,
    SUM(CASE WHEN cust_id IS NULL THEN 1 ELSE 0 END) as null_count,
    SUM(CASE WHEN cust_id IS NULL THEN 1 ELSE 0 END) * 100.0 / COUNT(*) as null_pct
FROM source_customers
UNION ALL
SELECT 
    'email',
    COUNT(*),
    SUM(CASE WHEN email IS NULL THEN 1 ELSE 0 END),
    SUM(CASE WHEN email IS NULL THEN 1 ELSE 0 END) * 100.0 / COUNT(*)
FROM source_customers;

-- Distinct value analysis
SELECT 
    COUNT(DISTINCT status) as distinct_values,
    COUNT(*) as total_rows
FROM source_customers;

-- Value distribution
SELECT 
    status,
    COUNT(*) as frequency,
    COUNT(*) * 100.0 / SUM(COUNT(*)) OVER() as percentage
FROM source_customers
GROUP BY status
ORDER BY frequency DESC;

-- Pattern analysis for phone numbers
SELECT 
    LEN(phone) as phone_length,
    COUNT(*) as frequency
FROM source_customers
GROUP BY LEN(phone)
ORDER BY frequency DESC;
```

### Deliverables
- [ ] Data profiling report for each column
- [ ] Null/empty value analysis
- [ ] Distinct value counts
- [ ] Min/max/average for numeric columns
- [ ] Pattern analysis for text fields
- [ ] Data quality issue documentation

---

## Assignment B12: Simple ETL Process Design

### Business Context
Design a basic ETL process to load data from CSV files into a star schema.

### Objectives
1. Understand Extract, Transform, Load phases
2. Design staging tables
3. Create dimension and fact loading procedures

### ETL Architecture
```
Source Files (CSV)
       ↓
   EXTRACT
       ↓
  Staging Tables
       ↓
   TRANSFORM
       ↓
Dimension Tables → Fact Tables
       ↓
    LOAD
```

### Staging Table Design
```sql
-- Staging table mirrors source structure
CREATE TABLE stg_sales (
    load_id INT,
    load_timestamp DATETIME DEFAULT GETDATE(),
    -- Source columns (all as VARCHAR for initial load)
    transaction_id VARCHAR(50),
    transaction_date VARCHAR(50),
    product_code VARCHAR(50),
    store_code VARCHAR(50),
    quantity VARCHAR(50),
    unit_price VARCHAR(50),
    total_amount VARCHAR(50),
    -- Metadata
    source_file VARCHAR(200),
    row_number INT,
    is_processed BIT DEFAULT 0
);
```

### Dimension Load Procedure
```sql
CREATE PROCEDURE load_dim_product
AS
BEGIN
    -- Insert new products
    INSERT INTO dim_product (product_id, product_name, category, unit_price)
    SELECT DISTINCT
        s.product_code,
        s.product_name,
        s.category,
        CAST(s.unit_price AS DECIMAL(10,2))
    FROM stg_sales s
    WHERE NOT EXISTS (
        SELECT 1 FROM dim_product d 
        WHERE d.product_id = s.product_code
    );
END;
```

### Deliverables
- [ ] ETL architecture diagram
- [ ] Staging table DDL
- [ ] Dimension load procedures
- [ ] Fact load procedure
- [ ] Error handling approach
- [ ] Load logging mechanism

---

## Assignment B13: Data Quality Rules

### Business Context
Implement data quality checks for incoming data before loading into the warehouse.

### Objectives
1. Define data quality dimensions
2. Create validation rules
3. Implement quality checks in SQL

### Data Quality Dimensions
1. **Completeness** - No missing required values
2. **Accuracy** - Values match expected patterns
3. **Consistency** - Values consistent across systems
4. **Timeliness** - Data is current
5. **Uniqueness** - No unwanted duplicates
6. **Validity** - Values within expected ranges

### Quality Check Implementation
```sql
-- Create quality log table
CREATE TABLE dq_validation_log (
    log_id INT IDENTITY(1,1) PRIMARY KEY,
    check_timestamp DATETIME DEFAULT GETDATE(),
    table_name VARCHAR(100),
    rule_name VARCHAR(100),
    rule_type VARCHAR(50),
    records_checked INT,
    records_failed INT,
    failure_rate DECIMAL(5,2),
    status VARCHAR(20)
);

-- Completeness check
CREATE PROCEDURE dq_check_completeness
    @table_name VARCHAR(100),
    @column_name VARCHAR(100)
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX);
    DECLARE @total INT, @nulls INT;
    
    SET @sql = N'SELECT @total = COUNT(*), 
                        @nulls = SUM(CASE WHEN ' + @column_name + ' IS NULL THEN 1 ELSE 0 END)
                 FROM ' + @table_name;
    
    EXEC sp_executesql @sql, 
         N'@total INT OUTPUT, @nulls INT OUTPUT', 
         @total OUTPUT, @nulls OUTPUT;
    
    INSERT INTO dq_validation_log (table_name, rule_name, rule_type, records_checked, records_failed, failure_rate, status)
    VALUES (
        @table_name,
        'NULL_CHECK_' + @column_name,
        'COMPLETENESS',
        @total,
        @nulls,
        @nulls * 100.0 / NULLIF(@total, 0),
        CASE WHEN @nulls = 0 THEN 'PASSED' ELSE 'FAILED' END
    );
END;

-- Uniqueness check
CREATE PROCEDURE dq_check_uniqueness
    @table_name VARCHAR(100),
    @column_name VARCHAR(100)
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX);
    DECLARE @total INT, @duplicates INT;
    
    SET @sql = N'SELECT @total = COUNT(*), 
                        @duplicates = COUNT(*) - COUNT(DISTINCT ' + @column_name + ')
                 FROM ' + @table_name;
    
    EXEC sp_executesql @sql, 
         N'@total INT OUTPUT, @duplicates INT OUTPUT', 
         @total OUTPUT, @duplicates OUTPUT;
    
    INSERT INTO dq_validation_log (table_name, rule_name, rule_type, records_checked, records_failed, failure_rate, status)
    VALUES (
        @table_name,
        'UNIQUE_CHECK_' + @column_name,
        'UNIQUENESS',
        @total,
        @duplicates,
        @duplicates * 100.0 / NULLIF(@total, 0),
        CASE WHEN @duplicates = 0 THEN 'PASSED' ELSE 'FAILED' END
    );
END;

-- Valid range check
CREATE PROCEDURE dq_check_range
    @table_name VARCHAR(100),
    @column_name VARCHAR(100),
    @min_value DECIMAL(18,2),
    @max_value DECIMAL(18,2)
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX);
    DECLARE @total INT, @out_of_range INT;
    
    SET @sql = N'SELECT @total = COUNT(*), 
                        @out_of_range = SUM(CASE WHEN ' + @column_name + ' < @min OR ' + @column_name + ' > @max THEN 1 ELSE 0 END)
                 FROM ' + @table_name;
    
    EXEC sp_executesql @sql, 
         N'@total INT OUTPUT, @out_of_range INT OUTPUT, @min DECIMAL(18,2), @max DECIMAL(18,2)', 
         @total OUTPUT, @out_of_range OUTPUT, @min_value, @max_value;
    
    INSERT INTO dq_validation_log (table_name, rule_name, rule_type, records_checked, records_failed, failure_rate, status)
    VALUES (
        @table_name,
        'RANGE_CHECK_' + @column_name,
        'VALIDITY',
        @total,
        @out_of_range,
        @out_of_range * 100.0 / NULLIF(@total, 0),
        CASE WHEN @out_of_range = 0 THEN 'PASSED' ELSE 'FAILED' END
    );
END;
```

### Deliverables
- [ ] Data quality rule definitions
- [ ] Quality check stored procedures
- [ ] Validation logging system
- [ ] Quality dashboard queries
- [ ] Exception handling process

---

## Assignment B14: Basic OLAP Queries

### Business Context
Write analytical queries against the star schema to answer business questions.

### Objectives
1. Write aggregation queries
2. Implement grouping and filtering
3. Use window functions for analytics

### Sample Queries

**1. Sales Summary by Region and Category**
```sql
SELECT 
    s.region,
    p.category,
    SUM(f.net_amount) as total_sales,
    SUM(f.quantity_sold) as total_quantity,
    AVG(f.unit_price) as avg_price
FROM fact_sales f
JOIN dim_store s ON f.store_key = s.store_key
JOIN dim_product p ON f.product_key = p.product_key
GROUP BY s.region, p.category
ORDER BY s.region, total_sales DESC;
```

**2. Year-over-Year Comparison**
```sql
SELECT 
    d.year_number,
    d.month_name,
    SUM(f.net_amount) as monthly_sales,
    LAG(SUM(f.net_amount)) OVER (PARTITION BY d.month_number ORDER BY d.year_number) as prev_year_sales,
    SUM(f.net_amount) - LAG(SUM(f.net_amount)) OVER (PARTITION BY d.month_number ORDER BY d.year_number) as yoy_change
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
GROUP BY d.year_number, d.month_number, d.month_name
ORDER BY d.year_number, d.month_number;
```

**3. Running Total**
```sql
SELECT 
    d.full_date,
    SUM(f.net_amount) as daily_sales,
    SUM(SUM(f.net_amount)) OVER (ORDER BY d.full_date) as running_total
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
GROUP BY d.full_date
ORDER BY d.full_date;
```

**4. Ranking Products**
```sql
SELECT 
    p.product_name,
    p.category,
    SUM(f.net_amount) as total_sales,
    RANK() OVER (PARTITION BY p.category ORDER BY SUM(f.net_amount) DESC) as category_rank,
    DENSE_RANK() OVER (ORDER BY SUM(f.net_amount) DESC) as overall_rank
FROM fact_sales f
JOIN dim_product p ON f.product_key = p.product_key
GROUP BY p.product_name, p.category
ORDER BY p.category, category_rank;
```

### Deliverables
- [ ] 10 analytical queries covering various patterns
- [ ] Queries using window functions
- [ ] Time-based comparisons
- [ ] Ranking and percentile queries
- [ ] Pivot-style queries

---

## Assignment B15: Beginner Capstone - Retail Analytics DWH

### Business Context
Design and implement a complete data warehouse for a small retail chain with 5 stores.

### Requirements
**Business Questions:**
1. What are daily/weekly/monthly sales by store?
2. Which products are best sellers?
3. What is the average transaction value by store?
4. How do sales compare across regions?
5. What are peak selling hours?

### Deliverables
- [ ] Complete ER diagram for source system
- [ ] Star schema design
- [ ] DDL scripts for all tables
- [ ] Sample data (1000+ transactions)
- [ ] ETL procedures
- [ ] 10 analytical queries
- [ ] Data quality checks
- [ ] Documentation

### Grading Criteria
| Component | Weight |
|-----------|--------|
| Schema Design | 25% |
| DDL Scripts | 15% |
| ETL Procedures | 20% |
| Analytical Queries | 20% |
| Data Quality | 10% |
---

# Level 2: Intermediate (Dimensional Modeling & ETL)

## Learning Goals
- Master dimensional modeling techniques
- Implement Slowly Changing Dimensions
- Design snowflake and galaxy schemas
- Build robust ETL pipelines
- Understand data staging strategies

---

## Assignment I1: Slowly Changing Dimension Type 1

### Business Context
A telecommunications company needs to track customer information, but only cares about the current state.

### Objectives
1. Understand SCD Type 1 (Overwrite)
2. Implement Type 1 updates
3. Handle update scenarios

### Implementation
```sql
-- Customer dimension with SCD Type 1
CREATE TABLE dim_customer_scd1 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20) UNIQUE NOT NULL,
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    address VARCHAR(200),
    city VARCHAR(50),
    customer_segment VARCHAR(20),
    last_updated DATETIME
);

-- SCD Type 1 Update Procedure
CREATE PROCEDURE usp_scd1_customer_update
AS
BEGIN
    -- Update existing customers (Type 1 - overwrite)
    UPDATE d
    SET 
        d.customer_name = s.customer_name,
        d.email = s.email,
        d.phone = s.phone,
        d.address = s.address,
        d.city = s.city,
        d.customer_segment = s.customer_segment,
        d.last_updated = GETDATE()
    FROM dim_customer_scd1 d
    INNER JOIN stg_customers s ON d.customer_id = s.customer_id
    WHERE 
        ISNULL(d.customer_name, '') <> ISNULL(s.customer_name, '') OR
        ISNULL(d.email, '') <> ISNULL(s.email, '');
    
    -- Insert new customers
    INSERT INTO dim_customer_scd1 (customer_id, customer_name, email, phone, 
        address, city, customer_segment, last_updated)
    SELECT s.customer_id, s.customer_name, s.email, s.phone,
        s.address, s.city, s.customer_segment, GETDATE()
    FROM stg_customers s
    WHERE NOT EXISTS (
        SELECT 1 FROM dim_customer_scd1 d WHERE d.customer_id = s.customer_id
    );
END;
```

### Deliverables
- [ ] SCD Type 1 dimension table design
- [ ] Update stored procedure
- [ ] Test cases with sample data

---

## Assignment I2: Slowly Changing Dimension Type 2

### Business Context
A financial services company must track complete customer history for regulatory compliance.

### Implementation
```sql
-- Customer dimension with SCD Type 2
CREATE TABLE dim_customer_scd2 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20) NOT NULL,
    customer_name VARCHAR(100),
    address VARCHAR(200),
    credit_score_band VARCHAR(20),
    effective_start_date DATE NOT NULL,
    effective_end_date DATE,
    is_current BIT NOT NULL DEFAULT 1,
    version_number INT DEFAULT 1
);

-- SCD Type 2 Update Procedure
CREATE PROCEDURE usp_scd2_customer_update
AS
BEGIN
    DECLARE @today DATE = CAST(GETDATE() AS DATE);
    
    -- Expire old records where changes detected
    UPDATE d SET 
        d.effective_end_date = DATEADD(DAY, -1, @today),
        d.is_current = 0
    FROM dim_customer_scd2 d
    INNER JOIN stg_customers s ON d.customer_id = s.customer_id
    WHERE d.is_current = 1
    AND (ISNULL(d.address,'') <> ISNULL(s.address,'') OR
         ISNULL(d.credit_score_band,'') <> ISNULL(s.credit_score_band,''));
    
    -- Insert new version for changed records
    INSERT INTO dim_customer_scd2 (customer_id, customer_name, address,
        credit_score_band, effective_start_date, is_current, version_number)
    SELECT s.customer_id, s.customer_name, s.address, s.credit_score_band,
        @today, 1, ISNULL((SELECT MAX(version_number) 
        FROM dim_customer_scd2 WHERE customer_id = s.customer_id), 0) + 1
    FROM stg_customers s
    WHERE EXISTS (SELECT 1 FROM dim_customer_scd2 d 
        WHERE d.customer_id = s.customer_id 
        AND d.effective_end_date = DATEADD(DAY, -1, @today));
END;
```

### Deliverables
- [ ] SCD Type 2 dimension design
- [ ] Update procedure with all scenarios
- [ ] Point-in-time query examples

---

## Assignment I3: SCD Type 3 and Type 6 (Hybrid)

### Objectives
1. Implement SCD Type 3 (Add new column for previous value)
2. Implement Type 6 (1+2+3 hybrid)

### Type 3 Implementation
```sql
CREATE TABLE dim_customer_scd3 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20) UNIQUE NOT NULL,
    current_segment VARCHAR(20),
    previous_segment VARCHAR(20),
    segment_change_date DATE
);
```

### Type 6 Implementation
```sql
CREATE TABLE dim_patient_scd6 (
    patient_key INT IDENTITY(1,1) PRIMARY KEY,
    patient_id VARCHAR(20) NOT NULL,
    patient_name VARCHAR(100),           -- Type 1
    address VARCHAR(200),                 -- Type 2
    current_insurance VARCHAR(50),        -- Type 3
    previous_insurance VARCHAR(50),       -- Type 3
    effective_start_date DATE,            -- Type 2
    effective_end_date DATE,              -- Type 2
    is_current BIT DEFAULT 1
);
```

### Deliverables
- [ ] Both SCD type implementations
- [ ] Comparison of when to use each

---

## Assignment I4: Snowflake Schema Design

### Business Context
A retail chain with complex product hierarchies needs a normalized dimensional model.

### Design
```sql
-- Normalized Product Dimension (Snowflake)
CREATE TABLE dim_product_category (
    category_key INT PRIMARY KEY,
    category_name VARCHAR(100)
);

CREATE TABLE dim_product_subcategory (
    subcategory_key INT PRIMARY KEY,
    subcategory_name VARCHAR(100),
    category_key INT REFERENCES dim_product_category(category_key)
);

CREATE TABLE dim_product (
    product_key INT PRIMARY KEY,
    product_name VARCHAR(200),
    subcategory_key INT REFERENCES dim_product_subcategory(subcategory_key),
    unit_price DECIMAL(10,2)
);
```

### Deliverables
- [ ] Complete snowflake schema design
- [ ] Star vs snowflake comparison analysis

---

## Assignment I5: Galaxy Schema (Fact Constellation)

### Business Context
Design multiple fact tables sharing conformed dimensions.

### Design
```sql
-- Conformed Dimensions
CREATE TABLE dim_date (date_key INT PRIMARY KEY, full_date DATE);
CREATE TABLE dim_product (product_key INT PRIMARY KEY, product_name VARCHAR(200));
CREATE TABLE dim_store (store_key INT PRIMARY KEY, store_name VARCHAR(100));

-- Multiple Fact Tables
CREATE TABLE fact_sales (
    date_key INT, product_key INT, store_key INT,
    quantity INT, sales_amount DECIMAL(12,2)
);

CREATE TABLE fact_inventory (
    date_key INT, product_key INT, store_key INT,
    quantity_on_hand INT, inventory_value DECIMAL(12,2)
);

CREATE TABLE fact_purchasing (
    date_key INT, product_key INT, supplier_key INT,
    quantity_ordered INT, total_cost DECIMAL(12,2)
);
```

### Deliverables
- [ ] Galaxy schema diagram
- [ ] Cross-functional analytical queries

---

## Assignment I6: Junk Dimensions

### Business Context
Combine low-cardinality flags into a single dimension.

### Implementation
```sql
CREATE TABLE dim_order_flags (
    order_flag_key INT PRIMARY KEY,
    is_gift BIT, is_expedited BIT, is_first_order BIT,
    payment_type VARCHAR(20), shipping_type VARCHAR(20)
);

-- Pre-populate combinations
INSERT INTO dim_order_flags
SELECT ROW_NUMBER() OVER (ORDER BY g.v, e.v, p.v),
    g.v, e.v, 0, p.v, 'Standard'
FROM (VALUES (0),(1)) g(v)
CROSS JOIN (VALUES (0),(1)) e(v)
CROSS JOIN (VALUES ('Credit'),('Debit'),('PayPal')) p(v);
```

### Deliverables
- [ ] Junk dimension design
- [ ] Population script
- [ ] ETL lookup logic

---

## Assignment I7: Degenerate and Role-Playing Dimensions

### Degenerate Dimensions
```sql
CREATE TABLE fact_orders (
    order_key INT PRIMARY KEY,
    order_number VARCHAR(30),    -- Degenerate dimension (no dim table)
    invoice_number VARCHAR(30),  -- Degenerate dimension
    customer_key INT,
    amount DECIMAL(10,2)
);
```

### Role-Playing Dimensions
```sql
-- Single date dimension, multiple roles
CREATE VIEW dim_order_date AS SELECT date_key AS order_date_key, full_date FROM dim_date;
CREATE VIEW dim_ship_date AS SELECT date_key AS ship_date_key, full_date FROM dim_date;

CREATE TABLE fact_shipments (
    order_date_key INT, ship_date_key INT, delivery_date_key INT,
    quantity INT
);
```

### Deliverables
- [ ] Identify degenerate dimension candidates
- [ ] Role-playing dimension views

---

## Assignment I8: Bridge Tables for Many-to-Many

### Implementation
```sql
CREATE TABLE dim_diagnosis (
    diagnosis_key INT PRIMARY KEY,
    diagnosis_code VARCHAR(10),
    diagnosis_name VARCHAR(200)
);

CREATE TABLE bridge_patient_diagnosis (
    patient_diagnosis_group_key INT,
    diagnosis_key INT REFERENCES dim_diagnosis(diagnosis_key),
    weight_factor DECIMAL(5,4) DEFAULT 1.0,
    is_primary BIT DEFAULT 0,
    PRIMARY KEY (patient_diagnosis_group_key, diagnosis_key)
);

CREATE TABLE fact_patient_visits (
    visit_key INT PRIMARY KEY,
    patient_diagnosis_group_key INT,
    total_charges DECIMAL(12,2)
);

-- Query with weighted allocation
SELECT d.diagnosis_name,
    SUM(f.total_charges * b.weight_factor) as weighted_charges
FROM fact_patient_visits f
JOIN bridge_patient_diagnosis b ON f.patient_diagnosis_group_key = b.patient_diagnosis_group_key
JOIN dim_diagnosis d ON b.diagnosis_key = d.diagnosis_key
GROUP BY d.diagnosis_name;
```

### Deliverables
- [ ] Bridge table design
- [ ] Weight factor implementation

---

## Assignment I9: Factless Fact Tables

### Coverage Table
```sql
CREATE TABLE fact_product_store_coverage (
    product_key INT, store_key INT,
    effective_date_key INT, expiration_date_key INT,
    PRIMARY KEY (product_key, store_key, effective_date_key)
);

-- Find products authorized but never sold
SELECT p.product_name, s.store_name
FROM fact_product_store_coverage c
JOIN dim_product p ON c.product_key = p.product_key
JOIN dim_store s ON c.store_key = s.store_key
WHERE NOT EXISTS (
    SELECT 1 FROM fact_sales f 
    WHERE f.product_key = c.product_key AND f.store_key = c.store_key
);
```

### Deliverables
- [ ] Coverage factless fact table
- [ ] Event tracking factless fact table
- [ ] Negative analysis queries

---

## Assignment I10: ETL Staging Layers

### Multi-Layer Architecture
```sql
-- RAW Layer: Exact copy from source
CREATE SCHEMA raw;
CREATE TABLE raw.customers (
    raw_id INT IDENTITY(1,1),
    load_timestamp DATETIME DEFAULT GETDATE(),
    customer_id VARCHAR(MAX), customer_name VARCHAR(MAX)
);

-- STAGING Layer: Typed and cleansed
CREATE SCHEMA staging;
CREATE TABLE staging.customers (
    staging_id INT IDENTITY(1,1),
    customer_id VARCHAR(20) NOT NULL,
    customer_name VARCHAR(100),
    is_valid BIT DEFAULT 1
);

-- INTEGRATION Layer: Conformed dimensions
CREATE SCHEMA integration;
CREATE TABLE integration.dim_customer (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    customer_id VARCHAR(20) NOT NULL,
    effective_start_date DATE, is_current BIT
);
```

### Deliverables
- [ ] Multi-layer schema design
- [ ] Transformation procedures
- [ ] Error handling and logging

---

## Assignment I11: Incremental Load Strategies

### Watermark-Based Loading
```sql
CREATE TABLE etl.load_watermarks (
    table_name VARCHAR(100) PRIMARY KEY,
    last_load_timestamp DATETIME
);

CREATE PROCEDURE etl_incremental_load
AS
BEGIN
    DECLARE @last_load DATETIME, @current DATETIME = GETDATE();
    SELECT @last_load = ISNULL(last_load_timestamp, '1900-01-01')
    FROM etl.load_watermarks WHERE table_name = 'orders';
    
    INSERT INTO staging.orders
    SELECT * FROM source.orders
    WHERE modified_timestamp > @last_load AND modified_timestamp <= @current;
    
    UPDATE etl.load_watermarks SET last_load_timestamp = @current
    WHERE table_name = 'orders';
END;
```

### Change Detection with Hash
```sql
UPDATE dim_customer SET row_hash = HASHBYTES('SHA2_256', 
    CONCAT(customer_name, '|', email, '|', address));
```

### Deliverables
- [ ] Timestamp-based incremental load
- [ ] Hash-based change detection

---

## Assignment I12: Conformed Dimensions

### Enterprise-Wide Design
```sql
CREATE TABLE dim_customer_conformed (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    crm_customer_id VARCHAR(20),
    ecommerce_customer_id VARCHAR(20),
    customer_name VARCHAR(100) NOT NULL,
    customer_segment VARCHAR(20),
    lifecycle_stage VARCHAR(30),
    source_system VARCHAR(50),
    effective_start_date DATE,
    is_current BIT
);
```

### Deliverables
- [ ] Conformed customer dimension
- [ ] Conformed product dimension  
- [ ] Source system mapping

---

## Assignment I13: Audit Dimensions and Data Lineage

### Implementation
```sql
CREATE TABLE dim_audit (
    audit_key INT PRIMARY KEY,
    load_id INT,
    source_system VARCHAR(100),
    source_file VARCHAR(500),
    load_timestamp DATETIME,
    record_count INT,
    etl_version VARCHAR(20)
);

CREATE TABLE fact_sales (
    sales_key INT PRIMARY KEY,
    audit_key INT REFERENCES dim_audit(audit_key),
    -- other keys and measures
);

-- Data lineage query
SELECT f.*, a.source_system, a.source_file, a.load_timestamp
FROM fact_sales f
JOIN dim_audit a ON f.audit_key = a.audit_key
WHERE f.sales_key = 12345;
```

### Deliverables
- [ ] Audit dimension design
- [ ] Integration with fact tables
- [ ] Lineage tracking queries

---

## Assignment I14: Date and Time Dimensions

### Comprehensive Date Dimension
```sql
CREATE TABLE dim_date (
    date_key INT PRIMARY KEY,
    full_date DATE NOT NULL,
    day_of_week INT, day_name VARCHAR(10),
    month_number INT, month_name VARCHAR(15),
    quarter INT, year INT,
    fiscal_year INT, fiscal_quarter INT,
    is_weekday BIT, is_weekend BIT, is_holiday BIT,
    holiday_name VARCHAR(50)
);

-- Time of Day Dimension
CREATE TABLE dim_time (
    time_key INT PRIMARY KEY,
    full_time TIME NOT NULL,
    hour_24 INT, hour_12 INT,
    minute INT, second INT,
    am_pm VARCHAR(2),
    time_period VARCHAR(20)  -- Morning, Afternoon, Evening, Night
);
```

### Deliverables
- [ ] Date dimension with fiscal calendar
- [ ] Time dimension
- [ ] Population scripts

---

## Assignment I15: Intermediate Capstone - E-Commerce Analytics DWH

### Requirements
Design a complete data warehouse for an e-commerce platform covering:
- Orders and sales analysis
- Customer behavior tracking (SCD Type 2)
- Product catalog with hierarchy
- Multiple date roles (order, ship, delivery)
- Promotional analysis (bridge table)
- Inventory tracking

### Deliverables
- [ ] Complete dimensional model (12+ tables)
- [ ] All SCD implementations
- [ ] ETL procedures with staging
- [ ] 15 analytical queries
- [ ] Incremental load strategy
- [ ] Documentation

### Grading Criteria
| Component | Weight |
|-----------|--------|
| Dimensional Model Design | 20% |
| SCD Implementation | 15% |
| ETL Procedures | 25% |
| Analytical Queries | 20% |
| Data Quality | 10% |
| Documentation | 10% |

---

# Level 3: Advanced (Complex Architectures & Optimization)

## Learning Goals
- Master Data Vault modeling
- Implement advanced ETL patterns
- Optimize query performance
- Design for scalability
- Handle complex business scenarios

---

## Assignment A1: Data Vault 2.0 - Hubs

### Business Context
A large enterprise needs a flexible, auditable data warehouse that can handle changing business requirements.

### Hub Design
```sql
-- Hub: Core business entity (Customer)
CREATE TABLE hub_customer (
    hub_customer_hk BINARY(32) PRIMARY KEY,  -- Hash key
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL,
    -- Business keys
    customer_id VARCHAR(20) NOT NULL
);

-- Hub: Product
CREATE TABLE hub_product (
    hub_product_hk BINARY(32) PRIMARY KEY,
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL,
    sku VARCHAR(30) NOT NULL
);

-- Hub: Order
CREATE TABLE hub_order (
    hub_order_hk BINARY(32) PRIMARY KEY,
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL,
    order_number VARCHAR(30) NOT NULL
);

-- Hash key generation
CREATE FUNCTION dv_hash_key(@business_key VARCHAR(500))
RETURNS BINARY(32)
AS
BEGIN
    RETURN HASHBYTES('SHA2_256', UPPER(TRIM(@business_key)));
END;
```

### Deliverables
- [ ] 5 Hub table designs
- [ ] Hash key generation function
- [ ] Loading procedures

---

## Assignment A2: Data Vault 2.0 - Links

### Link Design (Relationships)
```sql
-- Link: Customer-Order relationship
CREATE TABLE link_customer_order (
    link_customer_order_hk BINARY(32) PRIMARY KEY,
    hub_customer_hk BINARY(32) NOT NULL,
    hub_order_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL,
    FOREIGN KEY (hub_customer_hk) REFERENCES hub_customer(hub_customer_hk),
    FOREIGN KEY (hub_order_hk) REFERENCES hub_order(hub_order_hk)
);

-- Link: Order-Product relationship (with degenerate key)
CREATE TABLE link_order_product (
    link_order_product_hk BINARY(32) PRIMARY KEY,
    hub_order_hk BINARY(32) NOT NULL,
    hub_product_hk BINARY(32) NOT NULL,
    order_line_number INT,  -- Degenerate key
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL
);

-- Same-As Link (for entity resolution)
CREATE TABLE same_as_customer (
    same_as_customer_hk BINARY(32) PRIMARY KEY,
    hub_customer_hk_master BINARY(32) NOT NULL,
    hub_customer_hk_duplicate BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    record_source VARCHAR(100) NOT NULL
);
```

### Deliverables
- [ ] Standard link tables
- [ ] Same-as link for deduplication
- [ ] Link loading procedures

---

## Assignment A3: Data Vault 2.0 - Satellites

### Satellite Design (Descriptive Attributes)
```sql
-- Satellite: Customer descriptive attributes
CREATE TABLE sat_customer_details (
    hub_customer_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    load_end_date DATETIME,
    record_source VARCHAR(100) NOT NULL,
    hash_diff BINARY(32) NOT NULL,
    -- Descriptive attributes
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    address VARCHAR(200),
    city VARCHAR(50),
    PRIMARY KEY (hub_customer_hk, load_date),
    FOREIGN KEY (hub_customer_hk) REFERENCES hub_customer(hub_customer_hk)
);

-- Satellite: Customer status (separate for different change rates)
CREATE TABLE sat_customer_status (
    hub_customer_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    load_end_date DATETIME,
    record_source VARCHAR(100),
    hash_diff BINARY(32),
    customer_status VARCHAR(20),
    loyalty_tier VARCHAR(20),
    credit_limit DECIMAL(12,2),
    PRIMARY KEY (hub_customer_hk, load_date)
);

-- Effectivity Satellite (for link validity)
CREATE TABLE sat_customer_order_eff (
    link_customer_order_hk BINARY(32) NOT NULL,
    load_date DATETIME NOT NULL,
    load_end_date DATETIME,
    record_source VARCHAR(100),
    is_active BIT DEFAULT 1,
    PRIMARY KEY (link_customer_order_hk, load_date)
);
```

### Hash Diff Calculation
```sql
-- Calculate hash diff to detect changes
UPDATE sat_customer_details
SET hash_diff = HASHBYTES('SHA2_256', 
    CONCAT(ISNULL(customer_name,''), '|',
           ISNULL(email,''), '|',
           ISNULL(phone,''), '|',
           ISNULL(address,''), '|',
           ISNULL(city,'')));
```

### Deliverables
- [ ] Descriptive satellites
- [ ] Status satellites
- [ ] Effectivity satellites
- [ ] Hash diff implementation

---

## Assignment A4: DWH Architecture Patterns

### Inmon Architecture (Corporate Information Factory)
```
Source Systems
     ↓
[ ETL ]
     ↓
[ Enterprise Data Warehouse ] (3NF normalized)
     ↓
[ Data Marts ] (Dimensional)
     ↓
[ Reporting/Analytics ]
```

### Kimball Architecture (Dimensional Bus)
```
Source Systems
     ↓
[ ETL ]
     ↓
[ Staging Area ]
     ↓
[ Presentation Layer ] (Dimensional Data Marts)
     ↓
[ Reporting/Analytics ]
```

### Data Vault Architecture
```
Source Systems
     ↓
[ ETL ]
     ↓
[ Raw Vault ] (Hubs, Links, Satellites)
     ↓
[ Business Vault ] (Derived entities)
     ↓
[ Information Marts ] (Dimensional)
     ↓
[ Reporting/Analytics ]
```

### Deliverables
- [ ] Architecture comparison document
- [ ] Decision matrix for pattern selection
- [ ] Hybrid architecture design

---

## Assignment A5: Lambda and Kappa Architectures

### Lambda Architecture (Batch + Real-time)
```sql
-- Batch Layer (Master Dataset)
CREATE TABLE batch_layer.orders (
    order_id BIGINT PRIMARY KEY,
    customer_id INT,
    order_date DATETIME,
    total_amount DECIMAL(12,2),
    processed_date DATETIME
);

-- Speed Layer (Real-time increments)
CREATE TABLE speed_layer.orders_realtime (
    order_id BIGINT,
    customer_id INT,
    order_date DATETIME,
    total_amount DECIMAL(12,2),
    event_timestamp DATETIME,
    processed_timestamp DATETIME
);

-- Serving Layer (Merged View)
CREATE VIEW serving_layer.orders_merged AS
SELECT * FROM batch_layer.orders
WHERE order_date >= DATEADD(DAY, -1, GETDATE())
UNION ALL
SELECT order_id, customer_id, order_date, total_amount, NULL
FROM speed_layer.orders_realtime
WHERE event_timestamp > (SELECT MAX(processed_date) FROM batch_layer.orders);
```

### Deliverables
- [ ] Lambda architecture design
- [ ] Kappa architecture comparison
- [ ] Real-time processing strategy

---

## Assignment A6: Late-Arriving Facts and Dimensions

### Handling Late-Arriving Dimensions
```sql
-- Create placeholder dimension record
INSERT INTO dim_customer (customer_key, customer_id, customer_name, is_inferred)
VALUES (-1, 'UNKNOWN', 'Unknown Customer', 1);

-- Fact load with late-arriving dimension handling
CREATE PROCEDURE load_fact_sales
AS
BEGIN
    INSERT INTO fact_sales (date_key, customer_key, product_key, amount)
    SELECT 
        CONVERT(INT, FORMAT(s.sale_date, 'yyyyMMdd')),
        ISNULL(c.customer_key, -1),  -- Use placeholder if not found
        ISNULL(p.product_key, -1),
        s.amount
    FROM stg_sales s
    LEFT JOIN dim_customer c ON s.customer_id = c.customer_id AND c.is_current = 1
    LEFT JOIN dim_product p ON s.product_id = p.product_id AND p.is_current = 1;
    
    -- Log late-arriving records
    INSERT INTO etl.late_arriving_log (...)
    SELECT ... FROM stg_sales s
    WHERE NOT EXISTS (SELECT 1 FROM dim_customer c WHERE c.customer_id = s.customer_id);
END;

-- Process late-arriving dimension updates
CREATE PROCEDURE process_late_arriving_dimensions
AS
BEGIN
    -- Update inferred records with actual data
    UPDATE d
    SET customer_name = s.customer_name,
        email = s.email,
        is_inferred = 0
    FROM dim_customer d
    JOIN stg_customers s ON d.customer_id = s.customer_id
    WHERE d.is_inferred = 1;
END;
```

### Deliverables
- [ ] Late-arriving dimension handling
- [ ] Late-arriving fact handling
- [ ] Reconciliation procedures

---

## Assignment A7: Aggregate Tables and Materialized Views

### Aggregate Table Design
```sql
-- Daily sales aggregate
CREATE TABLE agg_daily_sales (
    date_key INT,
    product_key INT,
    store_key INT,
    total_quantity INT,
    total_sales DECIMAL(15,2),
    total_cost DECIMAL(15,2),
    transaction_count INT,
    avg_unit_price DECIMAL(10,2),
    last_updated DATETIME,
    PRIMARY KEY (date_key, product_key, store_key)
);

-- Monthly rollup
CREATE TABLE agg_monthly_sales (
    year_month INT,  -- YYYYMM format
    category_key INT,
    region_key INT,
    total_quantity INT,
    total_sales DECIMAL(18,2),
    yoy_growth_pct DECIMAL(8,2),
    PRIMARY KEY (year_month, category_key, region_key)
);

-- Aggregate maintenance procedure
CREATE PROCEDURE refresh_daily_aggregates
    @start_date DATE,
    @end_date DATE
AS
BEGIN
    DELETE FROM agg_daily_sales 
    WHERE date_key BETWEEN CONVERT(INT, FORMAT(@start_date, 'yyyyMMdd'))
                       AND CONVERT(INT, FORMAT(@end_date, 'yyyyMMdd'));
    
    INSERT INTO agg_daily_sales
    SELECT 
        f.date_key, f.product_key, f.store_key,
        SUM(f.quantity), SUM(f.sales_amount), SUM(f.cost_amount),
        COUNT(*), AVG(f.unit_price), GETDATE()
    FROM fact_sales f
    WHERE f.date_key BETWEEN CONVERT(INT, FORMAT(@start_date, 'yyyyMMdd'))
                         AND CONVERT(INT, FORMAT(@end_date, 'yyyyMMdd'))
    GROUP BY f.date_key, f.product_key, f.store_key;
END;
```

### Deliverables
- [ ] Aggregate table hierarchy design
- [ ] Refresh procedures
- [ ] Aggregate navigation strategy

---

## Assignment A8: Partitioning Strategies

### Range Partitioning
```sql
-- Create partition function (by year-month)
CREATE PARTITION FUNCTION pf_sales_monthly (INT)
AS RANGE RIGHT FOR VALUES 
(20230101, 20230201, 20230301, 20230401, 20230501, 20230601,
 20230701, 20230801, 20230901, 20231001, 20231101, 20231201,
 20240101, 20240201, 20240301);

-- Create partition scheme
CREATE PARTITION SCHEME ps_sales_monthly
AS PARTITION pf_sales_monthly
ALL TO ([PRIMARY]);

-- Partitioned fact table
CREATE TABLE fact_sales_partitioned (
    sales_key BIGINT IDENTITY(1,1),
    date_key INT NOT NULL,
    customer_key INT,
    product_key INT,
    quantity INT,
    sales_amount DECIMAL(12,2)
) ON ps_sales_monthly(date_key);

-- Partition maintenance
ALTER PARTITION FUNCTION pf_sales_monthly()
SPLIT RANGE (20240401);

-- Partition switching for efficient loading
ALTER TABLE stg_sales_202404 SWITCH TO fact_sales_partitioned PARTITION $partition.pf_sales_monthly(20240401);
```

### Deliverables
- [ ] Partition function design
- [ ] Partition scheme
- [ ] Maintenance procedures
- [ ] Partition switching strategy

---

## Assignment A9: Indexing Strategies

### Columnstore Indexes
```sql
-- Clustered columnstore for fact tables
CREATE CLUSTERED COLUMNSTORE INDEX cci_fact_sales
ON fact_sales;

-- Nonclustered columnstore for mixed workloads
CREATE NONCLUSTERED COLUMNSTORE INDEX ncci_dim_customer
ON dim_customer (customer_key, customer_name, city, customer_segment);
```

### B-Tree Indexes for Dimensions
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

### Deliverables
- [ ] Columnstore index strategy
- [ ] B-tree index recommendations
- [ ] Index maintenance plan

---

## Assignment A10: Query Optimization

### Query Tuning Techniques
```sql
-- Avoid SELECT * - specify columns
-- BAD:
SELECT * FROM fact_sales f JOIN dim_product p ON f.product_key = p.product_key;

-- GOOD:
SELECT f.date_key, f.quantity, f.sales_amount, p.product_name, p.category
FROM fact_sales f JOIN dim_product p ON f.product_key = p.product_key;

-- Use proper join hints when needed
SELECT f.*, p.product_name
FROM fact_sales f
INNER LOOP JOIN dim_product p ON f.product_key = p.product_key
WHERE f.date_key = 20240101;

-- Avoid functions on indexed columns
-- BAD:
WHERE YEAR(order_date) = 2024

-- GOOD:
WHERE order_date >= '2024-01-01' AND order_date < '2025-01-01'

-- Use EXISTS instead of IN for large subqueries
-- BAD:
WHERE product_key IN (SELECT product_key FROM dim_product WHERE category = 'Electronics')

-- GOOD:
WHERE EXISTS (SELECT 1 FROM dim_product p 
              WHERE p.product_key = f.product_key AND p.category = 'Electronics')
```

### Deliverables
- [ ] Query optimization guidelines
- [ ] Execution plan analysis
- [ ] Performance benchmarks

---

## Assignment A11: Change Data Capture (CDC)

### SQL Server CDC Implementation
```sql
-- Enable CDC on database
EXEC sys.sp_cdc_enable_db;

-- Enable CDC on table
EXEC sys.sp_cdc_enable_table
    @source_schema = 'dbo',
    @source_name = 'customers',
    @role_name = 'cdc_admin',
    @capture_instance = 'dbo_customers',
    @supports_net_changes = 1;

-- Query CDC changes
DECLARE @from_lsn BINARY(10), @to_lsn BINARY(10);
SET @from_lsn = sys.fn_cdc_get_min_lsn('dbo_customers');
SET @to_lsn = sys.fn_cdc_get_max_lsn();

SELECT * 
FROM cdc.fn_cdc_get_all_changes_dbo_customers(@from_lsn, @to_lsn, 'all update old')
ORDER BY __$seqval;

-- Process CDC for incremental load
CREATE PROCEDURE etl_process_cdc_customers
AS
BEGIN
    DECLARE @last_lsn BINARY(10), @current_lsn BINARY(10);
    
    SELECT @last_lsn = last_processed_lsn 
    FROM etl.cdc_tracking WHERE table_name = 'customers';
    
    SET @current_lsn = sys.fn_cdc_get_max_lsn();
    
    -- Process inserts/updates
    MERGE dim_customer AS target
    USING (
        SELECT customer_id, customer_name, email
        FROM cdc.fn_cdc_get_net_changes_dbo_customers(@last_lsn, @current_lsn, 'all')
        WHERE __$operation IN (2, 4)  -- Insert or Update
    ) AS source
    ON target.customer_id = source.customer_id AND target.is_current = 1
    WHEN MATCHED THEN UPDATE SET ...
    WHEN NOT MATCHED THEN INSERT ...;
    
    UPDATE etl.cdc_tracking SET last_processed_lsn = @current_lsn
    WHERE table_name = 'customers';
END;
```

### Deliverables
- [ ] CDC setup and configuration
- [ ] Change processing procedures
- [ ] CDC maintenance procedures

---

## Assignment A12: Data Quality Framework

### Comprehensive DQ Implementation
```sql
-- Data quality rule catalog
CREATE TABLE dq.rule_catalog (
    rule_id INT IDENTITY(1,1) PRIMARY KEY,
    rule_name VARCHAR(100),
    rule_type VARCHAR(50),  -- COMPLETENESS, ACCURACY, CONSISTENCY, etc.
    rule_sql VARCHAR(MAX),
    severity VARCHAR(20),  -- CRITICAL, WARNING, INFO
    threshold DECIMAL(5,2),
    is_active BIT DEFAULT 1
);

-- Data quality execution log
CREATE TABLE dq.execution_log (
    execution_id INT IDENTITY(1,1) PRIMARY KEY,
    rule_id INT,
    execution_time DATETIME DEFAULT GETDATE(),
    records_checked INT,
    records_failed INT,
    pass_rate DECIMAL(5,2),
    status VARCHAR(20),
    details VARCHAR(MAX)
);

-- Generic DQ check executor
CREATE PROCEDURE dq.execute_rule
    @rule_id INT
AS
BEGIN
    DECLARE @sql VARCHAR(MAX), @threshold DECIMAL(5,2), @severity VARCHAR(20);
    DECLARE @total INT, @failed INT, @pass_rate DECIMAL(5,2);
    
    SELECT @sql = rule_sql, @threshold = threshold, @severity = severity
    FROM dq.rule_catalog WHERE rule_id = @rule_id;
    
    -- Execute and capture results
    CREATE TABLE #results (record_id VARCHAR(100), error_detail VARCHAR(500));
    INSERT INTO #results EXEC(@sql);
    
    SELECT @failed = COUNT(*) FROM #results;
    -- Calculate pass rate and log results
    
    INSERT INTO dq.execution_log (rule_id, records_checked, records_failed, pass_rate, status)
    VALUES (@rule_id, @total, @failed, @pass_rate, 
            CASE WHEN @pass_rate >= @threshold THEN 'PASSED' ELSE 'FAILED' END);
END;
```

### Deliverables
- [ ] DQ rule catalog
- [ ] Automated DQ execution
- [ ] DQ dashboard queries
- [ ] Remediation workflows

---

## Assignment A13: Metadata Management

### Technical Metadata Repository
```sql
CREATE TABLE meta.table_catalog (
    table_id INT IDENTITY(1,1) PRIMARY KEY,
    schema_name VARCHAR(50),
    table_name VARCHAR(100),
    table_type VARCHAR(50),  -- DIMENSION, FACT, BRIDGE, etc.
    description VARCHAR(500),
    owner VARCHAR(100),
    created_date DATE,
    row_count BIGINT,
    last_refresh DATETIME
);

CREATE TABLE meta.column_catalog (
    column_id INT IDENTITY(1,1) PRIMARY KEY,
    table_id INT REFERENCES meta.table_catalog(table_id),
    column_name VARCHAR(100),
    data_type VARCHAR(50),
    is_nullable BIT,
    is_primary_key BIT,
    is_foreign_key BIT,
    description VARCHAR(500),
    business_definition VARCHAR(1000),
    source_mapping VARCHAR(500)
);

CREATE TABLE meta.lineage (
    lineage_id INT IDENTITY(1,1) PRIMARY KEY,
    source_table_id INT,
    target_table_id INT,
    source_column_id INT,
    target_column_id INT,
    transformation_logic VARCHAR(MAX),
    etl_process_name VARCHAR(100)
);

-- Auto-populate from system catalogs
INSERT INTO meta.table_catalog (schema_name, table_name, table_type)
SELECT s.name, t.name, 
    CASE WHEN t.name LIKE 'dim_%' THEN 'DIMENSION'
         WHEN t.name LIKE 'fact_%' THEN 'FACT'
         WHEN t.name LIKE 'bridge_%' THEN 'BRIDGE'
         ELSE 'OTHER' END
FROM sys.tables t
JOIN sys.schemas s ON t.schema_id = s.schema_id;
```

### Deliverables
- [ ] Metadata repository design
- [ ] Auto-population procedures
- [ ] Lineage tracking
- [ ] Impact analysis queries

---

## Assignment A14: Temporal Tables and Bi-Temporal Modeling

### System-Versioned Temporal Tables
```sql
-- Create system-versioned temporal table
CREATE TABLE dim_product_temporal (
    product_key INT PRIMARY KEY,
    product_id VARCHAR(20) NOT NULL,
    product_name VARCHAR(200),
    category VARCHAR(100),
    unit_price DECIMAL(10,2),
    valid_from DATETIME2 GENERATED ALWAYS AS ROW START,
    valid_to DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (valid_from, valid_to)
) WITH (SYSTEM_VERSIONING = ON (HISTORY_TABLE = dbo.dim_product_history));

-- Query as of specific time
SELECT * FROM dim_product_temporal
FOR SYSTEM_TIME AS OF '2024-06-15 10:00:00';

-- Query all history
SELECT * FROM dim_product_temporal
FOR SYSTEM_TIME ALL
WHERE product_id = 'P001'
ORDER BY valid_from;
```

### Bi-Temporal Design (Valid Time + Transaction Time)
```sql
CREATE TABLE dim_customer_bitemporal (
    customer_key INT IDENTITY(1,1),
    customer_id VARCHAR(20),
    customer_name VARCHAR(100),
    address VARCHAR(200),
    -- Valid time (business validity)
    valid_from DATE NOT NULL,
    valid_to DATE NOT NULL,
    -- Transaction time (when recorded)
    transaction_from DATETIME2 GENERATED ALWAYS AS ROW START,
    transaction_to DATETIME2 GENERATED ALWAYS AS ROW END,
    PERIOD FOR SYSTEM_TIME (transaction_from, transaction_to),
    PRIMARY KEY (customer_key, valid_from)
) WITH (SYSTEM_VERSIONING = ON);
```

### Deliverables
- [ ] Temporal table implementation
- [ ] Point-in-time queries
- [ ] Bi-temporal design

---

## Assignment A15: Advanced Capstone - Financial Services DWH

### Requirements
Design a complete data warehouse for a bank covering:
- Customer 360 view with bi-temporal tracking
- Transaction processing (high volume)
- Regulatory compliance (data lineage, audit)
- Risk analytics
- Data Vault architecture
- Real-time and batch integration

### Deliverables
- [ ] Data Vault model (Hubs, Links, Satellites)
- [ ] Business Vault derived entities
- [ ] Information Marts
- [ ] Partitioning strategy for transactions
- [ ] CDC implementation
- [ ] Data quality framework
- [ ] Metadata repository
- [ ] 20 complex analytical queries
- [ ] Performance optimization documentation

### Grading Criteria
| Component | Weight |
|-----------|--------|
| Data Vault Design | 20% |
| Performance Optimization | 20% |
| Data Quality Framework | 15% |
| ETL/CDC Implementation | 20% |
| Analytical Queries | 15% |
| Documentation | 10% |

---

# Level 4: Expert (Enterprise Solutions & Real-World Scenarios)

## Learning Goals
- Design enterprise-scale data warehouses
- Handle complex real-world business scenarios
- Implement data governance frameworks
- Architect cloud-native solutions
- Lead DWH modernization initiatives

---

## Assignment E1: Retail Industry - Omnichannel Analytics

### Business Context
A major retailer with 500+ stores, e-commerce, and mobile app needs unified customer and sales analytics.

### Requirements
- Unified customer view across touchpoints
- Inventory visibility across channels
- Customer journey tracking
- Promotion effectiveness analysis
- Store vs online comparison

### Schema Design
```sql
-- Customer 360 View
CREATE TABLE dim_customer_360 (
    customer_key INT IDENTITY(1,1) PRIMARY KEY,
    -- Identity resolution
    master_customer_id VARCHAR(30),
    store_customer_id VARCHAR(20),
    online_customer_id VARCHAR(20),
    mobile_customer_id VARCHAR(20),
    loyalty_card_number VARCHAR(20),
    -- Profile
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    -- Segmentation
    rfm_score INT,
    customer_segment VARCHAR(30),
    lifetime_value DECIMAL(15,2),
    preferred_channel VARCHAR(20),
    -- SCD 2 tracking
    effective_from DATE,
    effective_to DATE,
    is_current BIT
);

-- Omnichannel Fact
CREATE TABLE fact_omnichannel_sales (
    sales_key BIGINT IDENTITY(1,1),
    date_key INT,
    time_key INT,
    customer_key INT,
    product_key INT,
    store_key INT,  -- NULL for online
    channel_key INT,  -- Store, Web, Mobile, Marketplace
    promotion_key INT,
    -- Measures
    quantity INT,
    gross_amount DECIMAL(12,2),
    discount_amount DECIMAL(10,2),
    net_amount DECIMAL(12,2),
    cost_amount DECIMAL(12,2),
    -- Degenerate dimensions
    order_number VARCHAR(30),
    transaction_id VARCHAR(50)
);

-- Customer Journey Tracking
CREATE TABLE fact_customer_journey (
    journey_key BIGINT IDENTITY(1,1),
    session_id VARCHAR(50),
    customer_key INT,
    event_date_key INT,
    event_time_key INT,
    channel_key INT,
    event_type VARCHAR(50),  -- Browse, Add-to-Cart, Purchase, Return
    product_key INT,
    page_key INT,
    event_sequence INT,
    duration_seconds INT
);
```

### Analytical Queries
```sql
-- Customer channel preference analysis
SELECT 
    c.customer_segment,
    ch.channel_name,
    COUNT(DISTINCT f.customer_key) as customers,
    SUM(f.net_amount) as total_sales,
    AVG(f.net_amount) as avg_transaction
FROM fact_omnichannel_sales f
JOIN dim_customer_360 c ON f.customer_key = c.customer_key
JOIN dim_channel ch ON f.channel_key = ch.channel_key
WHERE c.is_current = 1
GROUP BY c.customer_segment, ch.channel_name;

-- Cross-channel customer behavior
SELECT 
    c.customer_key,
    c.customer_name,
    STRING_AGG(DISTINCT ch.channel_name, ', ') as channels_used,
    COUNT(DISTINCT f.order_number) as total_orders,
    SUM(f.net_amount) as total_spend
FROM fact_omnichannel_sales f
JOIN dim_customer_360 c ON f.customer_key = c.customer_key
JOIN dim_channel ch ON f.channel_key = ch.channel_key
WHERE c.is_current = 1
GROUP BY c.customer_key, c.customer_name
HAVING COUNT(DISTINCT ch.channel_key) > 1;
```

### Deliverables
- [ ] Complete omnichannel schema (15+ tables)
- [ ] Customer 360 integration logic
- [ ] Cross-channel attribution model
- [ ] 10 analytical queries
- [ ] Performance optimization for high volume

---

## Assignment E2: Healthcare Industry - Patient Analytics

### Business Context
A healthcare network needs HIPAA-compliant patient analytics with clinical outcomes tracking.

### Requirements
- Patient demographic and encounter tracking
- Diagnosis and procedure analysis (ICD-10, CPT)
- Provider performance metrics
- Readmission analysis
- Cost and revenue by service line

### Schema Design
```sql
-- Patient Dimension (PHI Considerations)
CREATE TABLE dim_patient (
    patient_key INT IDENTITY(1,1) PRIMARY KEY,
    patient_id VARCHAR(20),  -- MRN
    -- Tokenized/Masked PHI
    patient_hash BINARY(32),  -- For de-identification
    -- Non-PHI demographics
    birth_year INT,
    age_band VARCHAR(20),
    gender VARCHAR(10),
    zip_code_3digit VARCHAR(3),  -- Partial for privacy
    -- Clinical attributes
    primary_payer VARCHAR(50),
    risk_score DECIMAL(5,2),
    chronic_condition_count INT,
    -- SCD Type 2
    effective_from DATE,
    effective_to DATE,
    is_current BIT
);

-- Encounter Fact (Accumulating Snapshot)
CREATE TABLE fact_patient_encounter (
    encounter_key BIGINT IDENTITY(1,1) PRIMARY KEY,
    patient_key INT,
    provider_key INT,
    facility_key INT,
    department_key INT,
    payer_key INT,
    admission_date_key INT,
    discharge_date_key INT,
    -- Bridge to diagnoses (M:M)
    diagnosis_group_key INT,
    procedure_group_key INT,
    -- Measures
    length_of_stay INT,
    total_charges DECIMAL(15,2),
    total_payments DECIMAL(15,2),
    drg_weight DECIMAL(5,3),
    -- Flags
    is_readmission BIT,
    readmission_category VARCHAR(20),
    mortality_flag BIT
);

-- Quality Metrics Fact (Periodic Snapshot)
CREATE TABLE fact_quality_metrics_monthly (
    snapshot_date_key INT,
    provider_key INT,
    department_key INT,
    measure_key INT,
    numerator INT,
    denominator INT,
    rate DECIMAL(8,4),
    benchmark DECIMAL(8,4),
    goal DECIMAL(8,4),
    PRIMARY KEY (snapshot_date_key, provider_key, department_key, measure_key)
);
```

### Deliverables
- [ ] HIPAA-compliant schema design
- [ ] Diagnosis and procedure bridge tables
- [ ] Readmission analytics
- [ ] Quality metrics framework
- [ ] Data masking strategy

---

## Assignment E3: Finance Industry - Risk Analytics DWH

### Business Context
A bank needs comprehensive risk and regulatory reporting (Basel III, IFRS 9).

### Requirements
- Credit risk exposure tracking
- Loan portfolio analysis
- Regulatory capital calculations
- Stress testing support
- Anti-money laundering data model

### Schema Design
```sql
-- Account Dimension (SCD Type 6)
CREATE TABLE dim_account (
    account_key INT IDENTITY(1,1) PRIMARY KEY,
    account_number VARCHAR(20),
    customer_key INT,
    -- Current attributes
    current_product_type VARCHAR(50),
    current_risk_rating VARCHAR(10),
    current_status VARCHAR(20),
    -- Previous attributes (Type 3)
    previous_risk_rating VARCHAR(10),
    risk_rating_change_date DATE,
    -- Type 2 tracking
    effective_from DATE,
    effective_to DATE,
    is_current BIT,
    -- Regulatory
    basel_asset_class VARCHAR(50)
);

-- Credit Exposure Fact (Daily Snapshot)
CREATE TABLE fact_credit_exposure_daily (
    snapshot_date_key INT,
    account_key INT,
    customer_key INT,
    product_key INT,
    -- Exposure measures
    outstanding_balance DECIMAL(18,2),
    committed_amount DECIMAL(18,2),
    unutilized_amount DECIMAL(18,2),
    collateral_value DECIMAL(18,2),
    exposure_at_default DECIMAL(18,2),
    -- Risk parameters
    probability_of_default DECIMAL(8,6),
    loss_given_default DECIMAL(8,6),
    expected_loss DECIMAL(18,2),
    risk_weighted_assets DECIMAL(18,2),
    PRIMARY KEY (snapshot_date_key, account_key)
);

-- Transaction Monitoring (AML)
CREATE TABLE fact_transaction_monitoring (
    transaction_key BIGINT IDENTITY(1,1),
    transaction_date_key INT,
    transaction_time_key INT,
    source_account_key INT,
    dest_account_key INT,
    customer_key INT,
    channel_key INT,
    transaction_type VARCHAR(30),
    amount DECIMAL(18,2),
    currency_key INT,
    amount_usd DECIMAL(18,2),
    -- Risk flags
    risk_score DECIMAL(5,2),
    is_suspicious BIT,
    alert_id VARCHAR(30)
);
```

### Deliverables
- [ ] Credit risk data model
- [ ] Regulatory reporting mart
- [ ] AML transaction tracking
- [ ] Historical exposure tracking
- [ ] Stress testing data structures

---

## Assignment E4: E-Commerce - Real-Time Analytics Platform

### Business Context
A high-volume e-commerce platform needs real-time analytics for personalization and fraud detection.

### Requirements
- Real-time sales dashboard
- Clickstream analytics
- Personalization data model
- Fraud detection signals
- A/B testing framework

### Lambda Architecture Implementation
```sql
-- Speed Layer: Real-time aggregates
CREATE TABLE realtime.session_metrics (
    session_id VARCHAR(50) PRIMARY KEY,
    customer_key INT,
    session_start DATETIME,
    page_views INT,
    products_viewed INT,
    cart_additions INT,
    cart_value DECIMAL(12,2),
    last_activity DATETIME,
    conversion_flag BIT,
    expiry_timestamp DATETIME
);

-- Speed Layer: Real-time sales
CREATE TABLE realtime.sales_minute (
    minute_key INT,  -- YYYYMMDDHHMM
    product_key INT,
    order_count INT,
    units_sold INT,
    revenue DECIMAL(15,2),
    PRIMARY KEY (minute_key, product_key)
);

-- Batch Layer: Consolidated Clickstream
CREATE TABLE batch.fact_clickstream (
    click_key BIGINT IDENTITY(1,1),
    event_timestamp DATETIME,
    session_id VARCHAR(50),
    customer_key INT,
    device_key INT,
    page_key INT,
    product_key INT,
    event_type VARCHAR(30),
    referrer_key INT,
    -- Behavioral metrics
    time_on_page_seconds INT,
    scroll_depth_pct INT,
    click_position_x INT,
    click_position_y INT
);

-- Personalization Features
CREATE TABLE ml.customer_features (
    customer_key INT PRIMARY KEY,
    feature_date DATE,
    -- Behavioral features
    avg_session_duration DECIMAL(8,2),
    avg_page_views DECIMAL(8,2),
    preferred_category_1 INT,
    preferred_category_2 INT,
    preferred_brand_1 INT,
    -- Propensity scores
    purchase_propensity DECIMAL(5,4),
    churn_propensity DECIMAL(5,4),
    -- Recommendation context
    last_viewed_products VARCHAR(500),
    last_purchased_products VARCHAR(500)
);
```

### Deliverables
- [ ] Lambda architecture design
- [ ] Real-time aggregation tables
- [ ] Clickstream data model
- [ ] Feature store for ML
- [ ] A/B testing fact table

---

## Assignment E5: Cloud Data Warehouse Architecture

### Business Context
Migrate on-premises DWH to cloud-native architecture (conceptual design for Snowflake/BigQuery/Redshift).

### Multi-Layer Cloud Architecture
```
Data Sources
     ↓
[ Ingestion Layer ] (Kafka, Fivetran, Airbyte)
     ↓
[ Raw/Bronze Layer ] (Landing zone, immutable)
     ↓
[ Staging/Silver Layer ] (Cleansed, conformed)
     ↓
[ Curated/Gold Layer ] (Business-ready, aggregated)
     ↓
[ Consumption Layer ] (Views, Materialized Views, Data Shares)
```

### Snowflake-Style Schema
```sql
-- Database per layer
-- RAW_DB.SOURCE_SCHEMA.TABLE_NAME
-- STAGING_DB.SCHEMA.TABLE_NAME
-- ANALYTICS_DB.SCHEMA.TABLE_NAME

-- Dynamic tables (Snowflake)
CREATE OR REPLACE DYNAMIC TABLE analytics.daily_sales
    TARGET_LAG = '1 hour'
    WAREHOUSE = transform_wh
AS
SELECT 
    date_key,
    product_key,
    store_key,
    SUM(quantity) as total_quantity,
    SUM(amount) as total_amount
FROM staging.fact_sales
GROUP BY date_key, product_key, store_key;

-- Streams for CDC (Snowflake)
CREATE STREAM staging.customers_stream ON TABLE raw.customers;

-- Tasks for automation
CREATE TASK staging.refresh_customers
    WAREHOUSE = etl_wh
    SCHEDULE = 'USING CRON 0 * * * * UTC'
AS
    MERGE INTO staging.dim_customer t
    USING staging.customers_stream s
    ON t.customer_id = s.customer_id
    WHEN MATCHED AND s.metadata$action = 'INSERT' THEN UPDATE ...
    WHEN NOT MATCHED THEN INSERT ...;
```

### Deliverables
- [ ] Multi-layer architecture design
- [ ] Cost optimization strategy
- [ ] Scaling patterns
- [ ] Security and governance
- [ ] Migration planning

---

## Assignment E6: Data Governance Framework

### Business Context
Implement enterprise data governance across the data warehouse.

### Governance Components
```sql
-- Data Classification
CREATE TABLE gov.data_classification (
    classification_id INT PRIMARY KEY,
    table_name VARCHAR(200),
    column_name VARCHAR(100),
    data_category VARCHAR(50),  -- PII, PHI, Financial, Public
    sensitivity_level VARCHAR(20),  -- Confidential, Internal, Public
    retention_period_days INT,
    encryption_required BIT,
    masking_rule VARCHAR(100)
);

-- Data Stewardship
CREATE TABLE gov.data_stewards (
    steward_id INT PRIMARY KEY,
    domain VARCHAR(100),
    steward_name VARCHAR(100),
    steward_email VARCHAR(100),
    backup_steward VARCHAR(100)
);

-- Business Glossary
CREATE TABLE gov.business_glossary (
    term_id INT PRIMARY KEY,
    term_name VARCHAR(100) UNIQUE,
    definition VARCHAR(MAX),
    domain VARCHAR(100),
    synonyms VARCHAR(500),
    related_terms VARCHAR(500),
    owner VARCHAR(100),
    approved_date DATE,
    status VARCHAR(20)
);

-- Data Access Requests
CREATE TABLE gov.access_requests (
    request_id INT IDENTITY(1,1) PRIMARY KEY,
    requestor VARCHAR(100),
    dataset_requested VARCHAR(200),
    business_justification VARCHAR(MAX),
    access_type VARCHAR(20),
    request_date DATETIME,
    approval_status VARCHAR(20),
    approved_by VARCHAR(100),
    expiry_date DATE
);

-- Policy Enforcement
CREATE PROCEDURE gov.apply_column_masking
    @table_name VARCHAR(200),
    @role_name VARCHAR(100)
AS
BEGIN
    DECLARE @sql NVARCHAR(MAX);
    
    SELECT @sql = STRING_AGG(
        'GRANT SELECT ON ' + table_name + '(' + column_name + ') TO ' + @role_name,
        '; '
    )
    FROM gov.data_classification
    WHERE table_name = @table_name
    AND sensitivity_level = 'Public';
    
    EXEC sp_executesql @sql;
END;
```

### Deliverables
- [ ] Classification framework
- [ ] Stewardship model
- [ ] Business glossary
- [ ] Access control procedures
- [ ] Compliance reporting

---

## Assignment E7: Master Data Management Integration

### Business Context
Integrate MDM with the data warehouse for golden record management.

### MDM Integration Pattern
```sql
-- Golden Record Table
CREATE TABLE mdm.customer_master (
    master_customer_id VARCHAR(30) PRIMARY KEY,
    golden_record_source VARCHAR(50),
    confidence_score DECIMAL(5,4),
    -- Golden attributes
    customer_name VARCHAR(100),
    email VARCHAR(100),
    phone VARCHAR(20),
    address_line1 VARCHAR(200),
    city VARCHAR(50),
    -- Match keys
    match_key_name BINARY(32),
    match_key_email BINARY(32),
    match_key_phone BINARY(32),
    -- Audit
    created_date DATETIME,
    last_matched_date DATETIME,
    last_reviewed_date DATETIME
);

-- Cross-Reference Table
CREATE TABLE mdm.customer_xref (
    xref_id INT IDENTITY(1,1) PRIMARY KEY,
    master_customer_id VARCHAR(30),
    source_system VARCHAR(50),
    source_customer_id VARCHAR(30),
    match_confidence DECIMAL(5,4),
    match_rule_applied VARCHAR(100),
    UNIQUE (source_system, source_customer_id)
);

-- Match History
CREATE TABLE mdm.match_history (
    match_id BIGINT IDENTITY(1,1) PRIMARY KEY,
    master_customer_id VARCHAR(30),
    candidate_system VARCHAR(50),
    candidate_id VARCHAR(30),
    match_date DATETIME,
    match_score DECIMAL(5,4),
    match_status VARCHAR(20),
    reviewed_by VARCHAR(100)
);

-- DWH Integration
CREATE PROCEDURE etl.load_dim_customer_with_mdm
AS
BEGIN
    -- Join with MDM golden record
    MERGE dim_customer AS target
    USING (
        SELECT 
            m.master_customer_id,
            m.customer_name,
            m.email,
            x.source_system,
            x.source_customer_id
        FROM mdm.customer_master m
        JOIN mdm.customer_xref x ON m.master_customer_id = x.master_customer_id
    ) AS source
    ON target.source_customer_id = source.source_customer_id
    WHEN MATCHED THEN UPDATE SET 
        target.master_customer_id = source.master_customer_id,
        target.customer_name = source.customer_name;
END;
```

### Deliverables
- [ ] Golden record schema
- [ ] Cross-reference tables
- [ ] Match/merge procedures
- [ ] DWH integration patterns
- [ ] Data quality reconciliation

---

## Assignment E8: Self-Service Analytics Platform

### Business Context
Enable business users with self-service analytics while maintaining governance.

### Semantic Layer Design
```sql
-- Business-Friendly Views
CREATE VIEW analytics.v_sales_summary AS
SELECT 
    -- Friendly names
    d.full_date AS "Sale Date",
    s.store_name AS "Store",
    s.region AS "Region",
    p.product_name AS "Product",
    p.category AS "Category",
    c.customer_name AS "Customer",
    -- Pre-calculated metrics
    f.quantity AS "Units Sold",
    f.net_amount AS "Revenue",
    f.cost_amount AS "Cost",
    f.net_amount - f.cost_amount AS "Gross Profit",
    (f.net_amount - f.cost_amount) / NULLIF(f.net_amount, 0) * 100 AS "Gross Margin %"
FROM fact_sales f
JOIN dim_date d ON f.date_key = d.date_key
JOIN dim_store s ON f.store_key = s.store_key
JOIN dim_product p ON f.product_key = p.product_key
JOIN dim_customer c ON f.customer_key = c.customer_key;

-- Certified Metrics
CREATE TABLE analytics.certified_metrics (
    metric_id INT PRIMARY KEY,
    metric_name VARCHAR(100),
    metric_definition VARCHAR(MAX),
    calculation_logic VARCHAR(MAX),
    data_source VARCHAR(200),
    owner VARCHAR(100),
    certification_date DATE,
    refresh_frequency VARCHAR(50)
);

-- User Sandbox Area
CREATE SCHEMA user_sandbox;

-- Sandbox table template
CREATE TABLE user_sandbox.analysis_template (
    analysis_id INT IDENTITY(1,1) PRIMARY KEY,
    created_by VARCHAR(100),
    created_date DATETIME DEFAULT GETDATE(),
    analysis_name VARCHAR(200),
    source_query VARCHAR(MAX),
    expiry_date DATE
);
```

### Deliverables
- [ ] Semantic layer views
- [ ] Certified metrics catalog
- [ ] User sandbox framework
- [ ] Governance guardrails
- [ ] Usage monitoring

---

## Assignment E9: Data Mesh Architecture

### Business Context
Decentralize data ownership while maintaining interoperability across domains.

### Domain-Oriented Design
```sql
-- Domain: Sales
CREATE SCHEMA sales_domain;

-- Data Product: Daily Sales
CREATE TABLE sales_domain.dp_daily_sales (
    date_key INT,
    product_key INT,
    store_key INT,
    quantity INT,
    revenue DECIMAL(15,2),
    -- Data product metadata
    _dp_version VARCHAR(10) DEFAULT '1.0',
    _dp_created_timestamp DATETIME DEFAULT GETDATE()
);

-- Data Product Contract
CREATE TABLE sales_domain.dp_daily_sales_contract (
    contract_version VARCHAR(10),
    schema_version VARCHAR(10),
    sla_freshness_hours INT DEFAULT 24,
    sla_availability_pct DECIMAL(5,2) DEFAULT 99.9,
    data_owner VARCHAR(100),
    data_steward VARCHAR(100),
    pii_classification VARCHAR(20),
    schema_definition VARCHAR(MAX)
);

-- Domain: Customer
CREATE SCHEMA customer_domain;

CREATE TABLE customer_domain.dp_customer_360 (
    customer_key INT PRIMARY KEY,
    customer_id VARCHAR(20),
    customer_name VARCHAR(100),
    segment VARCHAR(30),
    lifetime_value DECIMAL(15,2),
    _dp_version VARCHAR(10),
    _dp_created_timestamp DATETIME
);

-- Data Product Registry (Central Catalog)
CREATE TABLE catalog.data_products (
    product_id INT PRIMARY KEY,
    domain VARCHAR(100),
    product_name VARCHAR(200),
    product_type VARCHAR(50),
    schema_name VARCHAR(100),
    table_name VARCHAR(200),
    owner VARCHAR(100),
    description VARCHAR(MAX),
    sla_definition VARCHAR(MAX),
    contract_url VARCHAR(500),
    created_date DATE,
    status VARCHAR(20)
);
```

### Deliverables
- [ ] Domain decomposition
- [ ] Data product design
- [ ] Contract specifications
- [ ] Central catalog
- [ ] Federated governance

---

## Assignment E10: Reverse Engineering Legacy DWH

### Business Context
Document and modernize an undocumented legacy data warehouse.

### Reverse Engineering Process
```sql
-- Step 1: Extract schema metadata
SELECT 
    s.name AS schema_name,
    t.name AS table_name,
    t.create_date,
    p.rows AS row_count
FROM sys.tables t
JOIN sys.schemas s ON t.schema_id = s.schema_id
LEFT JOIN sys.partitions p ON t.object_id = p.object_id AND p.index_id IN (0,1)
ORDER BY s.name, t.name;

-- Step 2: Extract column metadata
SELECT 
    s.name AS schema_name,
    t.name AS table_name,
    c.name AS column_name,
    ty.name AS data_type,
    c.max_length,
    c.precision,
    c.scale,
    c.is_nullable,
    c.is_identity
FROM sys.columns c
JOIN sys.tables t ON c.object_id = t.object_id
JOIN sys.schemas s ON t.schema_id = s.schema_id
JOIN sys.types ty ON c.user_type_id = ty.user_type_id
ORDER BY s.name, t.name, c.column_id;

-- Step 3: Extract relationships
SELECT 
    fk.name AS constraint_name,
    ps.name + '.' + pt.name AS parent_table,
    pc.name AS parent_column,
    rs.name + '.' + rt.name AS referenced_table,
    rc.name AS referenced_column
FROM sys.foreign_keys fk
JOIN sys.foreign_key_columns fkc ON fk.object_id = fkc.constraint_object_id
JOIN sys.tables pt ON fkc.parent_object_id = pt.object_id
JOIN sys.schemas ps ON pt.schema_id = ps.schema_id
JOIN sys.columns pc ON fkc.parent_object_id = pc.object_id AND fkc.parent_column_id = pc.column_id
JOIN sys.tables rt ON fkc.referenced_object_id = rt.object_id
JOIN sys.schemas rs ON rt.schema_id = rs.schema_id
JOIN sys.columns rc ON fkc.referenced_object_id = rc.object_id AND fkc.referenced_column_id = rc.column_id;

-- Step 4: Analyze data patterns
SELECT 
    column_name,
    COUNT(*) AS total_rows,
    COUNT(DISTINCT column_value) AS distinct_values,
    SUM(CASE WHEN column_value IS NULL THEN 1 ELSE 0 END) AS null_count
FROM (SELECT column_name, CAST(column_value AS VARCHAR(MAX)) AS column_value 
      FROM table_name UNPIVOT (...)) pivoted
GROUP BY column_name;

-- Step 5: Infer dimension/fact classification
SELECT 
    t.name AS table_name,
    CASE 
        WHEN t.name LIKE 'dim_%' THEN 'DIMENSION'
        WHEN t.name LIKE 'fact_%' THEN 'FACT'
        WHEN EXISTS (SELECT 1 FROM sys.foreign_keys fk 
                     WHERE fk.parent_object_id = t.object_id) 
             AND p.rows > 1000000 THEN 'LIKELY_FACT'
        ELSE 'UNKNOWN'
    END AS inferred_type
FROM sys.tables t
LEFT JOIN sys.partitions p ON t.object_id = p.object_id;
```

### Deliverables
- [ ] Schema documentation
- [ ] ER diagram generation
- [ ] Data dictionary
- [ ] ETL flow documentation
- [ ] Modernization recommendations

---

## Assignment E11: Performance Benchmarking and Capacity Planning

### Business Context
Establish performance baselines and plan for growth.

### Benchmarking Framework
```sql
-- Performance baseline table
CREATE TABLE perf.query_benchmarks (
    benchmark_id INT IDENTITY(1,1) PRIMARY KEY,
    query_name VARCHAR(100),
    query_category VARCHAR(50),
    query_text VARCHAR(MAX),
    baseline_duration_ms BIGINT,
    baseline_logical_reads BIGINT,
    baseline_date DATE,
    target_duration_ms BIGINT,
    sla_met BIT
);

-- Execution tracking
CREATE TABLE perf.query_executions (
    execution_id BIGINT IDENTITY(1,1) PRIMARY KEY,
    benchmark_id INT,
    execution_timestamp DATETIME,
    duration_ms BIGINT,
    logical_reads BIGINT,
    physical_reads BIGINT,
    row_count BIGINT,
    cpu_time_ms BIGINT,
    wait_stats VARCHAR(MAX)
);

-- Automated benchmark execution
CREATE PROCEDURE perf.run_benchmarks
AS
BEGIN
    DECLARE @query_text VARCHAR(MAX), @benchmark_id INT;
    DECLARE @start_time DATETIME2, @end_time DATETIME2;
    
    DECLARE benchmark_cursor CURSOR FOR
        SELECT benchmark_id, query_text FROM perf.query_benchmarks;
    
    OPEN benchmark_cursor;
    FETCH NEXT FROM benchmark_cursor INTO @benchmark_id, @query_text;
    
    WHILE @@FETCH_STATUS = 0
    BEGIN
        SET STATISTICS IO ON;
        SET @start_time = SYSDATETIME();
        
        EXEC sp_executesql @query_text;
        
        SET @end_time = SYSDATETIME();
        
        INSERT INTO perf.query_executions (benchmark_id, execution_timestamp, duration_ms)
        VALUES (@benchmark_id, @start_time, DATEDIFF(MILLISECOND, @start_time, @end_time));
        
        FETCH NEXT FROM benchmark_cursor INTO @benchmark_id, @query_text;
    END;
    
    CLOSE benchmark_cursor;
    DEALLOCATE benchmark_cursor;
END;

-- Capacity projection
SELECT 
    table_name,
    current_row_count,
    avg_daily_growth,
    current_size_gb,
    projected_size_1yr_gb,
    projected_size_3yr_gb
FROM (
    SELECT 
        name AS table_name,
        rows AS current_row_count,
        -- Calculate from historical data
        growth_rate * 365 AS avg_daily_growth,
        size_gb AS current_size_gb,
        size_gb * POWER(1 + growth_rate, 365) AS projected_size_1yr_gb,
        size_gb * POWER(1 + growth_rate, 365*3) AS projected_size_3yr_gb
    FROM storage_analysis
) projections;
```

### Deliverables
- [ ] Benchmark query suite
- [ ] Baseline establishment
- [ ] Growth projection model
- [ ] Capacity planning document
- [ ] Performance SLAs

---

## Assignment E12: Disaster Recovery and High Availability

### Business Context
Design DR and HA strategies for mission-critical data warehouse.

### DR Architecture
```sql
-- Recovery metadata
CREATE TABLE dr.recovery_points (
    recovery_point_id INT IDENTITY(1,1) PRIMARY KEY,
    database_name VARCHAR(100),
    backup_type VARCHAR(20),
    backup_start DATETIME,
    backup_end DATETIME,
    backup_size_gb DECIMAL(10,2),
    backup_location VARCHAR(500),
    is_verified BIT,
    retention_expiry DATE
);

-- RPO/RTO tracking
CREATE TABLE dr.sla_tracking (
    sla_id INT PRIMARY KEY,
    tier VARCHAR(20),  -- Tier 1, 2, 3
    rpo_hours INT,
    rto_hours INT,
    database_list VARCHAR(MAX),
    replication_method VARCHAR(50),
    failover_tested_date DATE
);

-- Failover runbook
CREATE PROCEDURE dr.execute_failover
    @tier VARCHAR(20)
AS
BEGIN
    -- Document all failover steps
    INSERT INTO dr.failover_log (step, status, timestamp)
    VALUES ('Initiate failover', 'STARTED', GETDATE());
    
    -- Step 1: Stop ETL processes
    -- Step 2: Verify replication sync
    -- Step 3: Failover databases
    -- Step 4: Update connection strings
    -- Step 5: Verify application connectivity
    -- Step 6: Resume ETL processes
END;

-- Data validation post-failover
CREATE PROCEDURE dr.validate_data_integrity
AS
BEGIN
    -- Row count comparison
    SELECT 
        table_name,
        primary_count,
        secondary_count,
        CASE WHEN primary_count = secondary_count THEN 'MATCH' ELSE 'MISMATCH' END as status
    FROM (
        SELECT 
            table_name,
            SUM(CASE WHEN server = 'PRIMARY' THEN row_count END) as primary_count,
            SUM(CASE WHEN server = 'SECONDARY' THEN row_count END) as secondary_count
        FROM row_count_snapshot
        GROUP BY table_name
    ) comparison
    WHERE primary_count <> secondary_count;
END;
```

### Deliverables
- [ ] DR architecture design
- [ ] RPO/RTO definitions by tier
- [ ] Failover procedures
- [ ] Testing schedule
- [ ] Validation scripts

---

## Assignment E13: Data Warehouse Security

### Business Context
Implement comprehensive security for sensitive data warehouse.

### Security Implementation
```sql
-- Row-Level Security
CREATE FUNCTION security.fn_region_filter(@region VARCHAR(50))
RETURNS TABLE
WITH SCHEMABINDING
AS
RETURN SELECT 1 AS access
    WHERE @region IN (SELECT region FROM security.user_region_access 
                      WHERE user_name = USER_NAME())
       OR IS_MEMBER('dw_admin') = 1;

CREATE SECURITY POLICY security.region_filter_policy
ADD FILTER PREDICATE security.fn_region_filter(region) ON dbo.fact_sales
WITH (STATE = ON);

-- Dynamic Data Masking
ALTER TABLE dim_customer
ALTER COLUMN email ADD MASKED WITH (FUNCTION = 'email()');

ALTER TABLE dim_customer
ALTER COLUMN phone ADD MASKED WITH (FUNCTION = 'partial(0,"XXX-XXX-",4)');

ALTER TABLE dim_customer
ALTER COLUMN customer_name ADD MASKED WITH (FUNCTION = 'partial(2,"*****",2)');

-- Column-Level Encryption
CREATE COLUMN MASTER KEY MasterKey_DW
WITH (KEY_STORE_PROVIDER_NAME = 'AZURE_KEY_VAULT',
      KEY_PATH = 'https://myvault.vault.azure.net/keys/MasterKey');

CREATE COLUMN ENCRYPTION KEY EncryptionKey_SSN
WITH VALUES (
    COLUMN_MASTER_KEY = MasterKey_DW,
    ALGORITHM = 'RSA_OAEP'
);

-- Audit logging
CREATE SERVER AUDIT DWH_Audit
TO FILE (FILEPATH = 'C:\AuditLogs\', MAXSIZE = 100 MB);

CREATE DATABASE AUDIT SPECIFICATION DWH_DatabaseAudit
FOR SERVER AUDIT DWH_Audit
ADD (SELECT, INSERT, UPDATE, DELETE ON SCHEMA::dbo BY public);
```

### Deliverables
- [ ] Row-level security policies
- [ ] Column masking strategy
- [ ] Encryption implementation
- [ ] Audit framework
- [ ] Access control matrix

---

## Assignment E14: DataOps and CI/CD for DWH

### Business Context
Implement DevOps practices for data warehouse development.

### CI/CD Pipeline Components
```yaml
# Azure DevOps Pipeline Example
trigger:
  branches:
    include:
      - main
      - develop

stages:
  - stage: Build
    jobs:
      - job: ValidateSQL
        steps:
          - task: SqlAzureDacpacDeployment@1
            inputs:
              action: 'Extract'
              
  - stage: Test
    jobs:
      - job: UnitTests
        steps:
          - script: |
              sqlcmd -S $(server) -d $(testdb) -i tests/run_unit_tests.sql
              
      - job: DataQualityTests
        steps:
          - script: |
              python scripts/run_dq_tests.py
              
  - stage: DeployDev
    jobs:
      - job: DeployDev
        steps:
          - task: SqlAzureDacpacDeployment@1
            inputs:
              action: 'Publish'
              
  - stage: DeployProd
    condition: and(succeeded(), eq(variables['Build.SourceBranch'], 'refs/heads/main'))
    jobs:
      - job: DeployProd
        environment: 'production'
```

### Version Control for DWH
```sql
-- Schema version tracking
CREATE TABLE meta.schema_versions (
    version_id INT IDENTITY(1,1) PRIMARY KEY,
    version_number VARCHAR(20),
    description VARCHAR(500),
    applied_date DATETIME,
    applied_by VARCHAR(100),
    script_name VARCHAR(200),
    rollback_script VARCHAR(200)
);

-- Migration script template
-- V001__create_dim_customer.sql
CREATE TABLE dim_customer (...);

-- Rollback
-- R001__drop_dim_customer.sql
DROP TABLE dim_customer;
```

### Deliverables
- [ ] CI/CD pipeline design
- [ ] Testing framework
- [ ] Version control strategy
- [ ] Environment management
- [ ] Rollback procedures

---

## Assignment E15: Expert Capstone - Enterprise Data Platform

### Business Context
Design and implement a complete enterprise data platform for a Fortune 500 company.

### Requirements
- Multi-source integration (ERP, CRM, Web, IoT)
- Hybrid cloud architecture
- Real-time and batch processing
- Self-service analytics enablement
- Complete data governance
- Disaster recovery for Tier 1 data
- Machine learning feature store

### Comprehensive Deliverables
- [ ] Enterprise architecture document
- [ ] Data Vault 2.0 Raw Vault (20+ entities)
- [ ] Business Vault with derived entities
- [ ] Multiple domain-specific data marts
- [ ] Real-time streaming integration
- [ ] Master data management integration
- [ ] Complete governance framework
- [ ] Security implementation
- [ ] CI/CD pipeline
- [ ] DR/HA design
- [ ] Performance benchmarks
- [ ] 30 complex analytical queries
- [ ] Self-service semantic layer
- [ ] Documentation package

### Grading Criteria
| Component | Weight |
|-----------|--------|
| Architecture Design | 20% |
| Data Vault Implementation | 15% |
| Governance & Security | 15% |
| ETL/Integration | 15% |
| Performance | 10% |
| Analytics Layer | 10% |
| Operations (CI/CD, DR) | 10% |
| Documentation | 5% |

---

# Appendices

## Appendix A: SQL Quick Reference

### DDL Commands
```sql
-- Table creation with constraints
CREATE TABLE table_name (
    column1 INT PRIMARY KEY,
    column2 VARCHAR(100) NOT NULL,
    column3 DECIMAL(10,2) DEFAULT 0,
    column4 INT REFERENCES other_table(id),
    CONSTRAINT ck_column3 CHECK (column3 >= 0)
);

-- Add/Modify columns
ALTER TABLE table_name ADD new_column VARCHAR(50);
ALTER TABLE table_name ALTER COLUMN column2 VARCHAR(200);
ALTER TABLE table_name DROP COLUMN old_column;

-- Indexes
CREATE INDEX ix_name ON table_name (column1, column2) INCLUDE (column3);
CREATE UNIQUE INDEX uix_name ON table_name (column1);
```

### Window Functions
```sql
-- Ranking
ROW_NUMBER() OVER (PARTITION BY col1 ORDER BY col2)
RANK() OVER (ORDER BY amount DESC)
DENSE_RANK() OVER (PARTITION BY category ORDER BY amount DESC)
NTILE(4) OVER (ORDER BY amount)

-- Aggregation
SUM(amount) OVER (PARTITION BY customer_id ORDER BY date ROWS UNBOUNDED PRECEDING)
AVG(amount) OVER (PARTITION BY category)
COUNT(*) OVER (PARTITION BY region)

-- Navigation
LAG(amount, 1) OVER (ORDER BY date)
LEAD(amount, 1) OVER (ORDER BY date)
FIRST_VALUE(amount) OVER (PARTITION BY category ORDER BY date)
LAST_VALUE(amount) OVER (...)
```

---

## Appendix B: Dimensional Modeling Patterns

### Common Patterns Summary

| Pattern | Use Case | Example |
|---------|----------|---------|
| Star Schema | Simple analytics | Sales analysis |
| Snowflake | Large dimensions | Product hierarchy |
| Galaxy | Multiple facts | Sales + Inventory |
| SCD Type 1 | Current only | Error corrections |
| SCD Type 2 | Full history | Customer tracking |
| SCD Type 3 | Previous value | Segment changes |
| SCD Type 6 | Hybrid | Compliance |
| Bridge Table | M:M relationships | Patient diagnoses |
| Junk Dimension | Low-cardinality flags | Order flags |
| Degenerate | Transaction IDs | Order number |
| Factless | Events/Coverage | Attendance |

---

## Appendix C: Data Quality Dimensions

| Dimension | Definition | Measurement |
|-----------|------------|-------------|
| Completeness | No missing values | % non-null |
| Accuracy | Values match reality | % verified |
| Consistency | Same across systems | % matching |
| Timeliness | Data is current | Latency |
| Uniqueness | No duplicates | % duplicate |
| Validity | Within expected range | % in range |

---

## Appendix D: Industry Data Models

### Retail (Key Entities)
- Customer, Product, Store, Promotion, Transaction

### Healthcare (Key Entities)
- Patient, Provider, Encounter, Diagnosis, Procedure, Payer

### Finance (Key Entities)
- Customer, Account, Transaction, Product, Branch, Risk

### Telecommunications (Key Entities)
- Subscriber, Service, Usage, Network, Bill

---

## Appendix E: Glossary

| Term | Definition |
|------|------------|
| **Dimension** | Descriptive context for facts |
| **Fact** | Measurable business event |
| **Grain** | Level of detail in a fact table |
| **Surrogate Key** | System-generated identifier |
| **Natural Key** | Business-meaningful identifier |
| **Conformed Dimension** | Shared across data marts |
| **ETL** | Extract, Transform, Load |
| **ELT** | Extract, Load, Transform |
| **CDC** | Change Data Capture |
| **SCD** | Slowly Changing Dimension |
| **Data Vault** | Hub, Link, Satellite modeling |
| **OLAP** | Online Analytical Processing |
| **OLTP** | Online Transaction Processing |
| **Data Mart** | Subject-specific data store |
| **ODS** | Operational Data Store |
| **Aggregate** | Pre-summarized data |
| **Grain** | Atomic level of fact table |
| **Bus Matrix** | Dimension-fact mapping |

---

## Curriculum Summary

| Level | Assignments | Key Topics |
|-------|-------------|------------|
| Beginner | 15 | ER diagrams, Normalization, Basic Star Schema |
| Intermediate | 15 | SCDs, Snowflake/Galaxy, ETL Layers, Bridge Tables |
| Advanced | 15 | Data Vault, Performance, CDC, Partitioning |
| Expert | 15 | Enterprise Solutions, Cloud, Governance, Industry |
| **Total** | **60** | |

### Completion Milestones
- **Beginner Certified**: Complete all B1-B15 assignments
- **Intermediate Certified**: Complete all I1-I15 assignments
- **Advanced Certified**: Complete all A1-A15 assignments
- **Expert Certified**: Complete all E1-E15 assignments + Capstone

---

*This curriculum is designed to build mastery progressively. Complete assignments in order, ensuring full understanding before advancing.*
