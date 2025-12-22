# Apache Spark Comprehensive Curriculum

> **150+ Hands-On Assignments** | Beginner → Intermediate → Advanced | Production-Ready Skills

---

## Table of Contents
1. [Sample Datasets & Project Setup](#sample-datasets--project-setup)
2. [Beginner Level (B01-B50)](#beginner-level-b01-b50)
3. [Intermediate Level (I01-I60)](#intermediate-level-i01-i60)
4. [Advanced Level (A01-A60)](#advanced-level-a01-a60)
5. [Capstone Projects (C01-C05)](#capstone-projects-c01-c05)

---

## Sample Datasets & Project Setup

### Dataset 1: E-Commerce Transactions
```
Schema: transactions
├── transaction_id: STRING (PK)
├── customer_id: STRING
├── product_id: STRING
├── category: STRING
├── quantity: INT
├── unit_price: DECIMAL(10,2)
├── total_amount: DECIMAL(10,2)
├── transaction_date: TIMESTAMP
├── payment_method: STRING
├── store_id: STRING
├── region: STRING
└── status: STRING (completed/pending/cancelled)

Volume: 10M rows (~2GB Parquet)
Partitioned by: transaction_date (daily)
```

### Dataset 2: Customer Profiles
```
Schema: customers
├── customer_id: STRING (PK)
├── name: STRING
├── email: STRING
├── phone: STRING
├── registration_date: DATE
├── tier: STRING (bronze/silver/gold/platinum)
├── lifetime_value: DECIMAL(12,2)
├── city: STRING
├── state: STRING
├── country: STRING
└── is_active: BOOLEAN

Volume: 1M rows (~200MB Parquet)
```

### Dataset 3: Product Catalog
```
Schema: products
├── product_id: STRING (PK)
├── name: STRING
├── category: STRING
├── subcategory: STRING
├── brand: STRING
├── supplier_id: STRING
├── cost_price: DECIMAL(10,2)
├── list_price: DECIMAL(10,2)
├── weight_kg: DECIMAL(6,2)
├── is_available: BOOLEAN
└── created_at: TIMESTAMP

Volume: 100K rows (~50MB Parquet)
```

### Dataset 4: Clickstream Events (Streaming)
```
Schema: clickstream
├── event_id: STRING
├── session_id: STRING
├── customer_id: STRING
├── event_type: STRING (view/click/cart/purchase)
├── page_url: STRING
├── product_id: STRING
├── event_timestamp: TIMESTAMP
├── device_type: STRING
├── browser: STRING
└── referrer: STRING

Volume: Continuous stream (~1000 events/second)
Format: JSON from Kafka topic "clickstream"
```

### Project Setup
```python
# requirements.txt
pyspark>=3.5.0
delta-spark>=3.0.0
pytest>=7.0.0
chispa>=0.9.0  # DataFrame testing

# spark_config.py
from pyspark.sql import SparkSession

def get_spark_session(app_name="SparkCurriculum", local=True):
    builder = SparkSession.builder.appName(app_name)
    if local:
        builder = builder.master("local[*]")
    return (builder
        .config("spark.sql.extensions", "io.delta.sql.DeltaSparkSessionExtension")
        .config("spark.sql.catalog.spark_catalog", "org.apache.spark.sql.delta.catalog.DeltaCatalog")
        .config("spark.sql.adaptive.enabled", "true")
        .config("spark.sql.adaptive.coalescePartitions.enabled", "true")
        .getOrCreate())

# Directory structure
project/
├── data/
│   ├── raw/           # CSV/JSON inputs
│   ├── bronze/        # Raw ingested data
│   ├── silver/        # Cleaned data
│   └── gold/          # Aggregated data
├── src/
│   ├── ingestion/
│   ├── transformations/
│   ├── quality/
│   └── streaming/
├── tests/
├── config/
└── notebooks/
```

### Data Generation Script
```python
# generate_sample_data.py
import random
from datetime import datetime, timedelta
from pyspark.sql import SparkSession
from pyspark.sql.functions import *
from pyspark.sql.types import *

def generate_transactions(spark, num_records=10_000_000):
    # Generate synthetic transaction data
    categories = ["Electronics", "Clothing", "Home", "Sports", "Books"]
    regions = ["North", "South", "East", "West", "Central"]
    payment_methods = ["Credit", "Debit", "Cash", "Digital"]
    
    schema = StructType([
        StructField("transaction_id", StringType()),
        StructField("customer_id", StringType()),
        StructField("product_id", StringType()),
        StructField("category", StringType()),
        StructField("quantity", IntegerType()),
        StructField("unit_price", DoubleType()),
        StructField("transaction_date", TimestampType()),
        StructField("payment_method", StringType()),
        StructField("store_id", StringType()),
        StructField("region", StringType()),
        StructField("status", StringType())
    ])
    
    # Use Spark to generate at scale
    df = (spark.range(0, num_records)
        .withColumn("transaction_id", concat(lit("TXN"), lpad(col("id").cast("string"), 12, "0")))
        .withColumn("customer_id", concat(lit("C"), lpad((rand() * 1000000).cast("int").cast("string"), 8, "0")))
        .withColumn("product_id", concat(lit("P"), lpad((rand() * 100000).cast("int").cast("string"), 6, "0")))
        .withColumn("category", element_at(array([lit(c) for c in categories]), (rand() * 5).cast("int") + 1))
        .withColumn("quantity", (rand() * 10).cast("int") + 1)
        .withColumn("unit_price", round(rand() * 500 + 10, 2))
        .withColumn("total_amount", col("quantity") * col("unit_price"))
        .withColumn("transaction_date", date_sub(current_timestamp(), (rand() * 365).cast("int")))
        .withColumn("payment_method", element_at(array([lit(p) for p in payment_methods]), (rand() * 4).cast("int") + 1))
        .withColumn("store_id", concat(lit("S"), lpad((rand() * 500).cast("int").cast("string"), 4, "0")))
        .withColumn("region", element_at(array([lit(r) for r in regions]), (rand() * 5).cast("int") + 1))
        .withColumn("status", when(rand() < 0.9, "completed").when(rand() < 0.95, "pending").otherwise("cancelled"))
        .drop("id"))
    
    return df
```

---

## Beginner Level (B01-B50)

### B01: First SparkSession
**Difficulty**: ⭐ | **Time**: 15 min

**Objectives**: Create SparkSession, understand app name, master URL, verify setup

**Requirements**:
1. Create a SparkSession with app name "MyFirstSparkApp"
2. Print Spark version
3. Print number of cores available
4. Stop the session properly

**Expected Output**:
```
Spark Version: 3.5.0
Available Cores: 8
SparkSession stopped successfully
```

**Validation**: Session creates without errors, version prints correctly

**Pitfalls**: Forgetting to stop session; creating multiple sessions

**Stretch**: Configure custom memory settings

---

### B02: Load CSV Data
**Difficulty**: ⭐ | **Time**: 20 min

**Objectives**: Read CSV files with options, understand schema inference

**Requirements**:
1. Load `transactions.csv` with header=true, inferSchema=true
2. Print schema
3. Show first 5 rows
4. Count total rows

**Expected Output**:
```
root
 |-- transaction_id: string
 |-- customer_id: string
 ...
Total rows: 10000
```

**Validation**: Schema matches expected; row count accurate

**Performance**: Must complete in <5 seconds for 10K rows

**Pitfalls**: Not handling malformed rows; memory issues with large files

**Stretch**: Compare inferSchema vs explicit schema performance

---

### B03: Load JSON Data
**Difficulty**: ⭐ | **Time**: 20 min

**Objectives**: Read JSON files, handle nested structures

**Requirements**:
1. Load `products.json` (contains nested `details` field)
2. Print schema showing nested structure
3. Flatten the nested structure
4. Save as single CSV file

**Expected Output**: Flattened DataFrame with all fields at root level

**Validation**: No null values from incorrect parsing

**Pitfalls**: Multiline JSON handling; nested array explosion

**Stretch**: Handle corrupted JSON records gracefully

---

### B04: Load Parquet Data
**Difficulty**: ⭐ | **Time**: 15 min

**Objectives**: Understand columnar format benefits, predicate pushdown

**Requirements**:
1. Load `transactions.parquet`
2. Select only 3 columns
3. Filter for region='North'
4. Explain the query plan
5. Count filtered rows

**Expected Output**: Query plan showing partition/column pruning

**Validation**: Physical plan shows pushed filters

**Pitfalls**: Loading entire dataset before filtering

**Stretch**: Compare Parquet vs CSV read performance

---

### B05: Basic Column Selection
**Difficulty**: ⭐ | **Time**: 15 min

**Objectives**: select(), col(), column expressions

**Requirements**:
1. Load transactions DataFrame
2. Select transaction_id, customer_id, total_amount using 3 different syntaxes
3. Create new column `amount_with_tax` (total_amount * 1.1)
4. Rename columns to snake_case

**Expected Output**: DataFrame with 4 columns, proper naming

**Validation**: Tax calculation accurate to 2 decimal places

**Pitfalls**: Column name case sensitivity; ambiguous column references

---

### B06: Filtering Rows
**Difficulty**: ⭐ | **Time**: 20 min

**Objectives**: filter(), where(), compound conditions

**Requirements**:
1. Filter transactions where total_amount > 100
2. Filter completed transactions in 'Electronics' category
3. Filter using SQL-style string expression
4. Combine multiple conditions with AND/OR

**Expected Output**: Row counts for each filter

**Validation**: Counts match SQL equivalent queries

**Pitfalls**: Null handling in filters; operator precedence

**Stretch**: Use isin() for multiple value matches

---

### B07: Sorting Data
**Difficulty**: ⭐ | **Time**: 15 min

**Objectives**: orderBy(), sort(), ascending/descending

**Requirements**:
1. Sort transactions by total_amount descending
2. Sort by multiple columns (region ASC, total_amount DESC)
3. Handle null values in sorting (nulls first/last)
4. Get top 10 transactions by amount

**Expected Output**: Sorted DataFrames with correct ordering

**Validation**: First/last rows match expected values

**Pitfalls**: Performance on large datasets; null ordering differences

---

### B08: Distinct and Deduplication
**Difficulty**: ⭐ | **Time**: 20 min

**Objectives**: distinct(), dropDuplicates(), counting unique values

**Requirements**:
1. Find distinct categories
2. Find distinct category-region combinations
3. Count unique customers
4. Remove duplicate transactions (by transaction_id)

**Expected Output**:
```
Unique categories: 5
Unique category-region pairs: 25
Unique customers: 87432
```

**Validation**: Counts match expected cardinality

**Pitfalls**: distinct() on entire row vs specific columns

---

### B09: Basic Aggregations
**Difficulty**: ⭐ | **Time**: 25 min

**Objectives**: count(), sum(), avg(), min(), max()

**Requirements**:
1. Calculate total transaction count
2. Sum of all transaction amounts
3. Average transaction value
4. Min/max transaction amounts
5. All stats in single query

**Expected Output**:
```
Total Transactions: 10000000
Total Amount: $2,345,678,901.23
Average: $234.57
Min: $10.00, Max: $5,234.99
```

**Validation**: Verify with SQL equivalents

**Pitfalls**: Null values in aggregations; precision loss

---

### B10: GroupBy Aggregations
**Difficulty**: ⭐ | **Time**: 30 min

**Objectives**: groupBy(), agg(), multiple aggregations

**Requirements**:
1. Total sales by category
2. Transaction count and avg amount by region
3. Multiple aggregations in single groupBy
4. Rename aggregated columns

**Expected Output**: Aggregated DataFrames with proper column names

**Validation**: Sum of groups equals total

**Pitfalls**: Forgetting to aggregate after groupBy

**Stretch**: Add percentage of total calculation

---

### B11: Working with Nulls
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: isNull(), isNotNull(), na.drop(), na.fill()

**Requirements**:
1. Count null values per column
2. Filter rows with any null values
3. Drop rows with nulls in specific columns
4. Fill nulls with defaults (0 for numeric, "Unknown" for string)
5. Use coalesce() for null replacement

**Expected Output**: Null counts before/after cleaning

**Validation**: No nulls in specified columns after cleaning

**Pitfalls**: Empty string vs null; type mismatches in fill

---

### B12: String Operations
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: String functions - upper, lower, trim, concat, substring

**Requirements**:
1. Uppercase all category names
2. Trim whitespace from customer names
3. Concatenate first_name and last_name
4. Extract year from transaction_id
5. Replace substrings

**Expected Output**: Cleaned string columns

**Validation**: No leading/trailing spaces; consistent casing

**Pitfalls**: Null propagation in string functions

---

### B13: Date and Time Operations
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Date functions - year, month, dayofweek, date_add, datediff

**Requirements**:
1. Extract year, month, day from transaction_date
2. Calculate days since transaction
3. Add 30 days to transaction_date
4. Filter transactions from last 90 days
5. Get transactions by day of week

**Expected Output**: DataFrame with extracted date components

**Validation**: Date calculations match calendar

**Pitfalls**: Timezone handling; date vs timestamp

**Stretch**: Handle multiple date formats in input

---

### B14: Type Casting
**Difficulty**: ⭐⭐ | **Time**: 20 min

**Objectives**: cast(), type conversion, handling conversion errors

**Requirements**:
1. Cast string to integer
2. Cast string to date with format
3. Cast decimal to double
4. Handle invalid cast values (use try_cast or when/otherwise)

**Expected Output**: Properly typed DataFrame

**Validation**: No data loss in conversions

**Pitfalls**: Silent null conversion on errors

---

### B15: Conditional Logic
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: when(), otherwise(), case statements

**Requirements**:
1. Create tier column based on total_amount thresholds
2. Categorize transactions: Small (<50), Medium (50-200), Large (>200)
3. Multiple nested conditions
4. Handle null cases explicitly

**Expected Output**:
```
Tier Distribution:
Small: 45%
Medium: 35%
Large: 20%
```

**Validation**: All rows categorized; no nulls in tier

---

### B16: Save to Parquet
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: write.parquet(), modes, partitioning basics

**Requirements**:
1. Save DataFrame as Parquet
2. Use overwrite mode
3. Partition by transaction_date
4. Verify file structure
5. Verify row counts after save

**Expected Output**: Partitioned Parquet files in date folders

**Validation**: Read back and compare counts

**Pitfalls**: Small files from over-partitioning

**Stretch**: Compare compression codecs (snappy vs gzip)

---

### B17: Save to CSV
**Difficulty**: ⭐⭐ | **Time**: 20 min

**Objectives**: write.csv(), options, single file output

**Requirements**:
1. Save DataFrame as CSV with header
2. Use specific delimiter (pipe)
3. Handle quotes in data
4. Coalesce to single file
5. Add timestamp to filename

**Expected Output**: Single CSV file with proper formatting

**Validation**: File readable in Excel/text editor

**Pitfalls**: coalesce(1) performance; special character escaping

---

### B18: Union DataFrames
**Difficulty**: ⭐⭐ | **Time**: 20 min

**Objectives**: union(), unionByName(), handling schema differences

**Requirements**:
1. Union two DataFrames with same schema
2. Use unionByName for different column orders
3. Handle missing columns with allowMissingColumns
4. Remove duplicates after union

**Expected Output**: Combined DataFrame

**Validation**: Row count = sum of inputs (before dedup)

**Pitfalls**: Schema mismatch errors; duplicate rows

---

### B19: Sample Data
**Difficulty**: ⭐ | **Time**: 15 min

**Objectives**: sample(), takeSample(), reproducibility

**Requirements**:
1. Sample 10% of transactions
2. Sample with seed for reproducibility
3. Sample without replacement
4. Take exact N samples

**Expected Output**: Sampled DataFrame with expected size

**Validation**: Same seed produces same sample

**Pitfalls**: sample() is approximate; takeSample() collects to driver

---

### B20: Basic Joins
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Inner join syntax, join conditions

**Requirements**:
1. Join transactions with customers on customer_id
2. Join transactions with products on product_id
3. Handle duplicate column names
4. Select specific columns from each table

**Expected Output**: Joined DataFrame with customer/product details

**Validation**: No orphan records in inner join

**Pitfalls**: Cartesian product from wrong join condition

---

### B21: Left and Right Joins
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: left_outer, right_outer joins, null handling

**Requirements**:
1. Left join transactions to customers (keep all transactions)
2. Identify transactions with missing customer data
3. Right join to find customers without transactions
4. Count matched vs unmatched records

**Expected Output**: Join statistics showing match rates

**Validation**: Unmatched customer_ids have null customer fields

---

### B22: Explain Query Plans
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: explain(), understanding physical plans

**Requirements**:
1. Write a query with filter, join, and aggregation
2. Call explain() and explain(True)
3. Identify: scan, filter, join strategy, exchange (shuffle)
4. Document what each stage does

**Expected Output**: Annotated query plan explanation

**Validation**: Correctly identify major plan components

**Pitfalls**: Misinterpreting optimized vs unoptimized plans

---

### B23: Create Temp Views
**Difficulty**: ⭐⭐ | **Time**: 20 min

**Objectives**: createOrReplaceTempView(), SQL queries

**Requirements**:
1. Create temp view for transactions
2. Query using spark.sql()
3. Join views using SQL syntax
4. Compare DataFrame API vs SQL results

**Expected Output**: Identical results from both approaches

**Validation**: SQL query returns same count as DataFrame

**Pitfalls**: View scope (session vs global)

---

### B24: SQL Aggregations
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: GROUP BY, HAVING in Spark SQL

**Requirements**:
1. Write SQL for sales by category
2. Filter groups with HAVING (total > 1M)
3. Order results
4. Use aliases properly

**Expected Output**: SQL query results matching DataFrame API

**Validation**: Results match previous DataFrame aggregations

---

### B25: RDD Basics
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Create RDD, map(), filter(), collect()

**Requirements**:
1. Create RDD from list
2. Create RDD from text file
3. Apply map transformation
4. Apply filter transformation
5. Collect results (small dataset only)

**Expected Output**: Transformed RDD results

**Validation**: Results match expected transformations

**Performance**: Never collect() large RDDs

**Pitfalls**: Using collect() on big data; serialization issues

---

### B26: RDD Aggregations
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: reduce(), fold(), aggregate()

**Requirements**:
1. Sum numbers using reduce
2. Find max value
3. Count elements
4. Calculate average using aggregate

**Expected Output**: Aggregation results

**Validation**: Match DataFrame equivalents

**Pitfalls**: Empty RDD handling; associativity requirements

---

### B27: Key-Value RDD Operations
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: reduceByKey(), groupByKey(), mapValues()

**Requirements**:
1. Create pair RDD (category, amount)
2. Sum amounts by category using reduceByKey
3. Compare with groupByKey (understand the difference)
4. Count by key

**Expected Output**: Category totals

**Validation**: Totals match DataFrame groupBy

**Pitfalls**: groupByKey shuffles all data; memory issues

**Stretch**: Implement custom aggregation with combineByKey

---

### B28: DataFrame vs RDD Performance
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Compare performance, understand Catalyst optimizer

**Requirements**:
1. Implement same aggregation in RDD and DataFrame
2. Time both approaches
3. Compare explain plans
4. Document when to use each

**Expected Output**: Performance comparison table

**Validation**: DataFrame faster due to optimization

**Key Learning**: RDDs bypass Catalyst optimizer

---

### B29: Schema Definition
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: StructType, StructField, explicit schemas

**Requirements**:
1. Define schema for transactions dataset
2. Load CSV with explicit schema
3. Compare load time vs inferSchema
4. Handle schema mismatches

**Expected Output**: Properly typed DataFrame

**Validation**: All columns have correct types

**Pitfalls**: Nullable settings; decimal precision

---

### B30: Complex Types - Arrays
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: ArrayType, array functions, explode

**Requirements**:
1. Create column with array of tags
2. Access array elements
3. Check if array contains value
4. Explode array to rows
5. Collect list back to array

**Expected Output**: Exploded and re-aggregated data

**Validation**: Round-trip preserves data

**Pitfalls**: Null arrays; empty arrays

---

### B31: Complex Types - Maps
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: MapType, map functions, key-value access

**Requirements**:
1. Create map column from two columns
2. Access values by key
3. Get all keys/values
4. Explode map to rows
5. Filter by map values

**Expected Output**: Map operations results

**Validation**: Key lookups return expected values

---

### B32: Complex Types - Structs
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Nested structs, dot notation, flattening

**Requirements**:
1. Create nested struct column
2. Access nested fields
3. Flatten nested structure
4. Create struct from columns
5. Handle deeply nested JSON

**Expected Output**: Flattened DataFrame

**Validation**: All nested data accessible

---

### B33: User Defined Functions (UDFs)
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Create and register UDFs, understand overhead

**Requirements**:
1. Create Python UDF to categorize amounts
2. Register UDF for SQL use
3. Apply UDF to DataFrame
4. Handle null inputs in UDF
5. Compare UDF vs built-in function performance

**Expected Output**: UDF applied successfully

**Validation**: Results match expected categorization

**Performance**: UDFs 10-100x slower than built-ins

**Pitfalls**: Serialization overhead; null handling

---

### B34: Caching Basics
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: cache(), persist(), unpersist()

**Requirements**:
1. Cache frequently accessed DataFrame
2. Verify caching in Spark UI (Storage tab)
3. Time queries before/after caching
4. Unpersist when done
5. Check memory usage

**Expected Output**: Performance improvement metrics

**Validation**: Second query significantly faster

**Pitfalls**: Caching before action; memory pressure

---

### B35: Broadcast Variables
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: SparkContext.broadcast(), broadcast joins

**Requirements**:
1. Create broadcast variable for lookup table
2. Use in UDF
3. Compare with regular variable
4. Check broadcast in Spark UI

**Expected Output**: Successful broadcast usage

**Validation**: Single copy sent to executors

**Pitfalls**: Broadcasting large data; updating broadcasts

---

### B36: Accumulators
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: Accumulator for counters, debugging

**Requirements**:
1. Create accumulator for error counting
2. Increment in transformation
3. Read final value after action
4. Use for data quality metrics

**Expected Output**: Accurate error count

**Validation**: Count matches filtered error count

**Pitfalls**: Reading accumulator before action; task retries

---

### B37: Partitions Basics
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: getNumPartitions(), repartition(), coalesce()

**Requirements**:
1. Check partition count of loaded data
2. Repartition to 10 partitions
3. Coalesce to 2 partitions
4. Understand shuffle vs no-shuffle
5. Check partition sizes

**Expected Output**: Partition statistics before/after

**Validation**: Correct partition counts

**Pitfalls**: Over-partitioning; uneven partitions

---

### B38: Writing Tests for Spark
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: pytest with Spark, DataFrame assertions

**Requirements**:
1. Set up pytest with SparkSession fixture
2. Write test for transformation function
3. Assert DataFrame equality
4. Handle floating point comparisons
5. Test edge cases (empty DataFrame, nulls)

**Expected Output**: Passing test suite

**Validation**: All tests pass; good coverage

**Pitfalls**: SparkSession management in tests; slow tests

---

### B39: Error Handling
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: Try/except, handling bad records, mode options

**Requirements**:
1. Handle file not found errors
2. Use PERMISSIVE mode for bad records
3. Capture corrupted records to separate column
4. Use DROPMALFORMED mode
5. Log errors appropriately

**Expected Output**: Clean data + error report

**Validation**: Bad records identified and handled

---

### B40: Configuration and SparkConf
**Difficulty**: ⭐⭐ | **Time**: 25 min

**Objectives**: SparkConf, runtime configuration

**Requirements**:
1. Set executor memory
2. Set number of shuffle partitions
3. Configure serialization
4. Read configurations at runtime
5. Document key configurations

**Expected Output**: Properly configured SparkSession

**Validation**: Configurations applied correctly

---

### B41: Word Count (Classic)
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Complete word count pipeline

**Requirements**:
1. Read text file
2. Split lines into words
3. Clean words (lowercase, remove punctuation)
4. Count word frequencies
5. Get top 20 words

**Expected Output**: Word frequency table

**Validation**: Common words (the, a, is) at top

---

### B42: Log File Analysis
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Parse semi-structured data, regex

**Requirements**:
1. Parse Apache log file format
2. Extract timestamp, IP, status code, URL
3. Count requests by status code
4. Find top 10 IPs
5. Calculate error rate

**Expected Output**: Log analysis metrics

**Validation**: Parsed fields match log entries

---

### B43: Data Profiling
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Summary statistics, data quality metrics

**Requirements**:
1. Calculate count, distinct, nulls per column
2. Min, max, mean, stddev for numeric columns
3. Value distribution for categorical columns
4. Identify potential data quality issues
5. Generate profile report

**Expected Output**: Data profile report

**Validation**: Stats match describe() output

---

### B44: Pivot Tables
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: pivot(), unpivot, cross-tabulation

**Requirements**:
1. Pivot sales by region and category
2. Handle many pivot values
3. Unpivot back to original form
4. Create cross-tabulation

**Expected Output**: Pivot table with regions as columns

**Validation**: Grand totals match original sum

**Pitfalls**: Too many pivot values; memory issues

---

### B45: Rolling Aggregations
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Window functions intro, running totals

**Requirements**:
1. Calculate running total by customer
2. 7-day rolling average of sales
3. Rank transactions by amount per customer
4. Compare window types (rows vs range)

**Expected Output**: DataFrames with window calculations

**Validation**: Running totals match cumulative sum

---

### B46: Data Deduplication
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Identify and remove duplicates

**Requirements**:
1. Find exact duplicates
2. Find duplicates by subset of columns
3. Keep first/last occurrence
4. Handle near-duplicates (fuzzy matching intro)
5. Report deduplication stats

**Expected Output**: Deduplicated DataFrame + stats

**Validation**: No duplicates remain on key columns

---

### B47: Data Standardization
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: Consistent formats, normalization

**Requirements**:
1. Standardize phone number formats
2. Normalize email addresses (lowercase)
3. Standardize date formats
4. Clean category names (trim, proper case)
5. Map variations to standard values

**Expected Output**: Standardized columns

**Validation**: All values in expected formats

---

### B48: Join Multiple Tables
**Difficulty**: ⭐⭐ | **Time**: 35 min

**Objectives**: Multi-way joins, join order

**Requirements**:
1. Join transactions, customers, and products
2. Use appropriate join types
3. Handle null keys
4. Optimize join order
5. Select required columns only

**Expected Output**: Denormalized fact table

**Validation**: Row counts reasonable; no Cartesian products

---

### B49: Export to Database
**Difficulty**: ⭐⭐ | **Time**: 30 min

**Objectives**: JDBC write, batch size, modes

**Requirements**:
1. Configure JDBC connection
2. Write DataFrame to PostgreSQL/MySQL
3. Use appropriate write mode
4. Set batch size for performance
5. Handle failures

**Expected Output**: Data in target database

**Validation**: Row counts match; data types correct

**Pitfalls**: Connection limits; transaction size

---

### B50: Beginner Capstone - Sales Report
**Difficulty**: ⭐⭐ | **Time**: 60 min

**Objectives**: Combine all beginner concepts

**Requirements**:
1. Load transactions, customers, products from CSV
2. Clean and validate data
3. Join all three datasets
4. Calculate:
   - Total sales by category
   - Top 10 customers by lifetime value
   - Monthly sales trend
   - Sales by region and payment method
5. Save results to Parquet
6. Cache intermediate results appropriately

**Expected Output**: Multiple analysis DataFrames saved to disk

**Validation Checks**:
- All joins complete without errors
- Aggregations sum correctly
- No null keys in final output
- Files saved successfully

**Stretch**: Add data quality report; visualize results

---

## Intermediate Level (I01-I60)

### I01: Window Functions - Ranking
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: row_number(), rank(), dense_rank(), ntile()

**Requirements**:
1. Rank customers by total purchase amount
2. Rank products by sales within each category
3. Compare row_number, rank, dense_rank on ties
4. Divide customers into quartiles using ntile(4)
5. Find top 3 products per category

**Expected Output**:
```
Product rankings with all ranking types
Top 3 products per category (15 rows for 5 categories)
```

**Validation**: Rankings consistent; top N per group correct

**Pitfalls**: Partitioning mistakes; orderBy missing

**Stretch**: Implement percentile ranking

---

### I02: Window Functions - Analytics
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: lead(), lag(), first_value(), last_value()

**Requirements**:
1. Calculate days between consecutive purchases (lag)
2. Compare current month sales to next month (lead)
3. Get first purchase date per customer
4. Calculate purchase recency
5. Year-over-year comparison

**Expected Output**: DataFrame with lead/lag analytics

**Validation**: First/last values match when verified manually

**Pitfalls**: Unbounded frame for last_value; null handling

---

### I03: Window Functions - Running Calculations
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Running sum, average, custom frame specs

**Requirements**:
1. Running total sales by customer (ordered by date)
2. 30-day rolling average transaction amount
3. Cumulative distinct product count
4. Moving window (3 rows before to current)
5. Range-based window (last 7 days)

**Expected Output**: Multiple running calculations

**Validation**: Running total at end matches group total

**Pitfalls**: rowsBetween vs rangeBetween; performance on large windows

---

### I04: Advanced Joins - Anti and Semi
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: left_anti, left_semi, understanding use cases

**Requirements**:
1. Find customers with no transactions (anti join)
2. Find products that have been sold (semi join)
3. Compare with NOT IN / EXISTS subqueries
4. Performance comparison with filter after left join

**Expected Output**: Anti/semi join results

**Validation**: Anti join count + matched count = total customers

---

### I05: Advanced Joins - Cross and Self
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: Cross join, self join use cases

**Requirements**:
1. Generate all customer-product pairs (sample data only!)
2. Self-join to find customers in same city
3. Find products frequently bought together
4. Compare prices within category (self join)

**Expected Output**: Cross/self join results

**Validation**: Cross join size = table1 * table2

**Performance**: Never cross join large tables without filters

---

### I06: Handling Skewed Joins
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Identify and mitigate join skew

**Requirements**:
1. Identify skewed key (one key has 50% of data)
2. Implement salting technique for skewed key
3. Split into skewed and non-skewed joins
4. Use broadcast for small skewed dimension
5. Compare execution times

**Expected Output**: Performance comparison before/after

**Validation**: Job completes without executor failures

**Pitfalls**: Over-salting; salt cleanup

---

### I07: Broadcast Joins
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: broadcast() hint, auto broadcast threshold

**Requirements**:
1. Force broadcast join with hint
2. Configure broadcast threshold (10MB default)
3. Verify broadcast in query plan
4. Compare with shuffle join performance
5. Handle too-large broadcast errors

**Expected Output**: Plan showing BroadcastHashJoin

**Validation**: No shuffle exchange in broadcast joins

**Performance**: 10x+ improvement for suitable tables

---

### I08: Join Strategies Deep Dive
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: SortMergeJoin, ShuffleHashJoin, BroadcastNestedLoop

**Requirements**:
1. Force different join strategies with hints
2. Explain when each strategy is optimal
3. Analyze plans for each strategy
4. Measure memory usage differences
5. Document strategy selection criteria

**Expected Output**: Performance comparison table

**Validation**: Plans show expected join strategies

---

### I09: Adaptive Query Execution (AQE)
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Enable AQE, understand optimizations

**Requirements**:
1. Enable AQE and coalesce partitions
2. Demonstrate skew handling with AQE
3. Compare plans with AQE on/off
4. Configure AQE thresholds
5. Monitor AQE decisions in Spark UI

**Expected Output**: Before/after AQE performance metrics

**Validation**: Fewer partitions after coalescing; skew handled

---

### I10: Data Partitioning Strategies
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Hash vs range partitioning, partition pruning

**Requirements**:
1. Partition data by date for time-series queries
2. Partition by region for geographic queries
3. Verify partition pruning in explain plan
4. Calculate optimal partition count
5. Handle partition skew

**Expected Output**: Partitioned data with balanced sizes

**Validation**: Queries scan only relevant partitions

**Formula**: partitions = total_data_size / (128MB to 256MB)

---

### I11: Bucketing
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: bucketBy(), sorted buckets, join optimization

**Requirements**:
1. Create bucketed table by customer_id
2. Join two bucketed tables (no shuffle!)
3. Sort within buckets
4. Verify bucket pruning
5. Compare with non-bucketed join

**Expected Output**: Bucketed tables, optimized joins

**Validation**: No Exchange in bucketed join plan

**Pitfalls**: Bucket count mismatch; sorting requirements

---

### I12: File Size Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Avoid small files, optimal file sizes

**Requirements**:
1. Analyze current file sizes
2. Calculate optimal partition count for 128MB files
3. Use coalesce/repartition appropriately
4. Configure maxRecordsPerFile
5. Implement file compaction job

**Expected Output**: Files between 128MB-1GB

**Validation**: Fewer, larger files after optimization

**Target**: 128MB-256MB per file for Parquet

---

### I13: Schema Evolution
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Handle schema changes, mergeSchema

**Requirements**:
1. Add new column to existing Parquet data
2. Use mergeSchema option
3. Handle missing columns (null filling)
4. Handle type changes (compatible only)
5. Document schema evolution best practices

**Expected Output**: Unified schema from multiple versions

**Validation**: All historical data readable

**Pitfalls**: Incompatible type changes; column renames

---

### I14: Spark SQL Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Catalyst optimizer, optimization rules

**Requirements**:
1. Write suboptimal query
2. Analyze optimized plan
3. Identify predicate pushdown
4. Identify column pruning
5. Use explain("codegen") for physical plan

**Expected Output**: Optimized vs unoptimized plans

**Validation**: Optimizer rewrites visible in plan

---

### I15: UDF Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Vectorized UDFs (Pandas UDFs), performance

**Requirements**:
1. Implement scalar Pandas UDF
2. Implement grouped map Pandas UDF
3. Compare with regular Python UDF
4. Handle nullable data in Pandas UDF
5. Benchmark all approaches

**Expected Output**: Performance comparison (5-100x improvement)

**Validation**: Results identical; speed significantly better

**Pitfalls**: Memory issues with large groups; serialization

---

### I16: Complex Aggregations
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: collect_list, collect_set, custom aggregators

**Requirements**:
1. Collect all products purchased by customer
2. Collect distinct categories per customer
3. Limit collection size
4. Create JSON from aggregated data
5. Implement custom UDAF (advanced)

**Expected Output**: Aggregated arrays/maps per group

**Validation**: Array contents match individual records

**Pitfalls**: Memory explosion with large collections

---

### I17: Handling Large Joins
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Join large tables efficiently

**Requirements**:
1. Join two 10M+ row tables
2. Filter before join (predicate pushdown)
3. Select only needed columns before join
4. Use appropriate join strategy
5. Monitor shuffle read/write

**Expected Output**: Successful large join

**Validation**: Job completes within memory limits

**Performance**: Must complete in <5 minutes

---

### I18: Memory Management
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Spark memory model, tuning

**Requirements**:
1. Understand execution vs storage memory
2. Configure spark.memory.fraction
3. Identify memory issues in Spark UI
4. Use MEMORY_AND_DISK persistence
5. Handle OOM errors

**Expected Output**: Memory configuration recommendations

**Validation**: No OOM errors; efficient memory use

---

### I19: Shuffle Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Minimize shuffles, optimize shuffle partitions

**Requirements**:
1. Identify shuffle operations in plan
2. Set optimal shuffle partition count
3. Use repartition vs coalesce appropriately  
4. Pre-partition data to avoid shuffle
5. Monitor shuffle in Spark UI

**Expected Output**: Optimized job with minimal shuffle

**Validation**: Reduced shuffle read/write bytes

**Formula**: shuffle_partitions = data_size / 200MB

---

### I20: Serialization
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: Kryo serialization, registration

**Requirements**:
1. Enable Kryo serialization
2. Register custom classes
3. Compare with Java serialization
4. Handle serialization errors
5. Benchmark serialization performance

**Expected Output**: Kryo configuration

**Validation**: Smaller serialized size; faster

---

### I21: Spark UI Analysis
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Navigate Spark UI, identify bottlenecks

**Requirements**:
1. Analyze job DAG visualization
2. Identify stages with long runtime
3. Find tasks with skew (max >> median)
4. Analyze shuffle read/write
5. Check for spill to disk
6. Review GC time

**Expected Output**: Performance analysis report

**Validation**: Correctly identify known issues

**Key Metrics**: Task duration, shuffle bytes, spill bytes, GC time

---

### I22: Debugging Failed Jobs
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Read error logs, common failure patterns

**Requirements**:
1. Debug OOM error
2. Debug serialization error
3. Debug null pointer exception
4. Debug container killed by YARN
5. Use driver/executor logs effectively

**Expected Output**: Debugging runbook

**Validation**: Successfully fix each error type

---

### I23: Data Quality Checks
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Implement DQ framework, assertions

**Requirements**:
1. Check for null primary keys
2. Check referential integrity
3. Validate value ranges
4. Check for duplicates
5. Generate DQ report with pass/fail

**Expected Output**: DQ report with metrics

**Validation**: Known issues caught by checks

**Framework Pattern**:
```python
dq_results = {
    "null_keys": df.filter(col("id").isNull()).count(),
    "duplicates": df.count() - df.dropDuplicates(["id"]).count(),
    "invalid_amounts": df.filter(col("amount") < 0).count()
}
```

---

### I24: Incremental Processing
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Process only new/changed data

**Requirements**:
1. Track high-watermark (max timestamp)
2. Filter for records after watermark
3. Handle late-arriving data
4. Update watermark after successful load
5. Make process idempotent

**Expected Output**: Incremental load framework

**Validation**: Only new records processed on re-run

---

### I25: Slowly Changing Dimensions (SCD)
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Implement SCD Type 1 and Type 2

**Requirements**:
1. Implement SCD Type 1 (overwrite)
2. Implement SCD Type 2 (history tracking)
3. Handle effective dates
4. Query point-in-time values
5. Manage current flag

**Expected Output**: SCD implementation

**Validation**: History preserved; current record correct

---

### I26: Reading from Databases
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: JDBC read, parallel fetching

**Requirements**:
1. Read table with single partition
2. Configure parallel reads with partitionColumn
3. Set numPartitions, lowerBound, upperBound
4. Push filters to database
5. Handle connection pooling

**Expected Output**: Parallel JDBC read

**Validation**: Multiple tasks reading simultaneously

**Pitfalls**: Sequential read without partitioning; connection limits

---

### I27: ETL Pipeline Design
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Design modular ETL pipeline

**Requirements**:
1. Separate Extract, Transform, Load modules
2. Implement configuration-driven pipeline
3. Add logging at each stage
4. Handle failures gracefully
5. Make pipeline rerunnable

**Expected Output**: Modular ETL framework

**Validation**: Pipeline runs end-to-end; handles restarts

---

### I28: Spark Submit
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Package and submit Spark applications

**Requirements**:
1. Package Python application with dependencies
2. Write spark-submit command
3. Configure driver and executor resources
4. Pass application arguments
5. Set dynamic allocation

**Expected Output**: spark-submit command and package

**Validation**: Application runs on cluster

**Example**:
```bash
spark-submit \
  --master yarn \
  --deploy-mode cluster \
  --driver-memory 4g \
  --executor-memory 8g \
  --executor-cores 4 \
  --num-executors 10 \
  --conf spark.sql.shuffle.partitions=200 \
  --py-files dependencies.zip \
  main.py --date 2024-01-01
```

---

### I29: Logging and Monitoring
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: Configure logging, capture metrics

**Requirements**:
1. Configure log4j for Spark
2. Add custom logging in application
3. Capture job metrics programmatically
4. Send metrics to monitoring system
5. Set up alerts for failures

**Expected Output**: Logging and monitoring setup

**Validation**: Logs captured; metrics visible

---

### I30: Testing Strategies
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Unit, integration, and data tests

**Requirements**:
1. Unit test transformation functions
2. Integration test with sample data
3. Test edge cases (empty, null, boundary)
4. Test data quality assertions
5. Mock external dependencies

**Expected Output**: Comprehensive test suite

**Validation**: High code coverage; all tests pass

**Framework**: pytest + chispa for DataFrame testing

---

### I31: Structured Streaming Basics
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Read stream, writeStream, basic operations

**Requirements**:
1. Read streaming data from file source
2. Apply transformations to stream
3. Write to file sink
4. Use checkpointing
5. Monitor streaming query

**Expected Output**: Streaming job processing files

**Validation**: Output files created; no data loss

---

### I32: Streaming Aggregations
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Streaming groupBy, complete/update modes

**Requirements**:
1. Count events by category (complete mode)
2. Sum amounts by region (update mode)
3. Understand output modes
4. Handle state storage
5. Monitor memory usage

**Expected Output**: Aggregated streaming results

**Validation**: Counts match batch processing

---

### I33: Streaming Triggers
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: Trigger types, processing time control

**Requirements**:
1. Use default trigger (micro-batch)
2. Use processingTime trigger (every 10 seconds)
3. Use once trigger for batch-like behavior
4. Use availableNow trigger
5. Measure latency differences

**Expected Output**: Comparison of trigger behaviors

**Validation**: Trigger intervals respected

---

### I34: Streaming Windowed Aggregations
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Tumbling and sliding windows

**Requirements**:
1. Count events per 5-minute tumbling window
2. Calculate average per 10-min sliding window (5-min slide)
3. Use event time vs processing time
4. Handle window overlap
5. Output results per window

**Expected Output**: Windowed aggregation results

**Validation**: Window boundaries correct

---

### I35: Watermarks and Late Data
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Handle late-arriving data

**Requirements**:
1. Define watermark (10 minutes)
2. Process late events within threshold
3. Drop events beyond watermark
4. Monitor dropped late events
5. Balance latency vs completeness

**Expected Output**: Watermark configuration

**Validation**: Late events within threshold included

---

### I36: Streaming Joins
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Stream-static and stream-stream joins

**Requirements**:
1. Join stream with static DataFrame
2. Join two streams on key
3. Handle state for stream-stream join
4. Configure state cleanup
5. Handle out-of-order events

**Expected Output**: Joined streaming data

**Validation**: Joins produce expected matches

---

### I37: Streaming Output to Files
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: File sink options, partitioning

**Requirements**:
1. Write stream to Parquet
2. Partition by date
3. Handle small files (use trigger)
4. Configure checkpointing
5. Recover from checkpoint

**Expected Output**: Partitioned Parquet output

**Validation**: Recovery works; no data loss

---

### I38: Streaming Deduplication
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: dropDuplicates in streaming

**Requirements**:
1. Deduplicate on event_id
2. Use watermark to limit state
3. Handle exactly-once semantics
4. Monitor state size
5. Configure state cleanup

**Expected Output**: Deduplicated stream

**Validation**: No duplicate events in output

---

### I39: Kafka Source Basics
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Read from Kafka topic

**Requirements**:
1. Configure Kafka source
2. Parse JSON messages
3. Handle schema for Kafka records
4. Configure consumer group
5. Start from earliest/latest

**Expected Output**: Streaming DataFrame from Kafka

**Validation**: Messages consumed correctly

**Setup**: Requires Kafka cluster (local Docker)

---

### I40: Kafka Sink
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Write to Kafka topic

**Requirements**:
1. Configure Kafka sink
2. Convert DataFrame to key/value
3. Handle serialization
4. Configure producer settings
5. Monitor delivery

**Expected Output**: Data written to Kafka

**Validation**: Messages consumable from topic

---

### I41: Foreach and ForeachBatch
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Custom sinks, batch processing

**Requirements**:
1. Use foreachBatch to write to database
2. Implement custom foreach writer
3. Handle batch processing logic
4. Implement idempotent writes
5. Error handling in custom sinks

**Expected Output**: Custom sink implementation

**Validation**: Data persisted in target system

---

### I42: Delta Lake Basics
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Delta format, ACID transactions

**Requirements**:
1. Write data as Delta table
2. Read Delta table
3. Understand transaction log
4. View table history
5. Time travel queries

**Expected Output**: Delta table with history

**Validation**: Time travel returns correct versions

---

### I43: Delta Merge (Upserts)
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: MERGE INTO for upserts

**Requirements**:
1. Implement upsert (insert or update)
2. Handle insert-only records
3. Handle update-only records
4. Conditional updates
5. Delete with merge

**Expected Output**: Merged Delta table

**Validation**: Upserts applied correctly

---

### I44: Delta Schema Evolution
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Schema evolution options

**Requirements**:
1. Add columns with mergeSchema
2. Overwrite schema completely
3. Handle column type changes
4. Use column mapping
5. Document schema history

**Expected Output**: Evolved schema

**Validation**: Historical data still readable

---

### I45: Delta Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: OPTIMIZE, VACUUM, Z-ORDER

**Requirements**:
1. Compact small files with OPTIMIZE
2. Z-Order for query optimization
3. VACUUM to remove old files
4. Configure retention
5. Measure query improvement

**Expected Output**: Optimized Delta table

**Validation**: Faster queries; reduced file count

---

### I46: Bronze Layer Implementation
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Raw data ingestion pattern

**Requirements**:
1. Ingest raw data with metadata
2. Add ingestion timestamp
3. Add source file information
4. Handle schema inference
5. Preserve original data exactly

**Expected Output**: Bronze Delta table

**Validation**: Raw data identical to source

---

### I47: Silver Layer Implementation
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Cleaned and conformed data

**Requirements**:
1. Read from bronze layer
2. Apply data cleaning
3. Standardize data types
4. Handle deduplication
5. Add quality flags

**Expected Output**: Silver Delta table

**Validation**: All quality checks pass

---

### I48: Gold Layer Implementation
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Business-level aggregations

**Requirements**:
1. Read from silver layer
2. Calculate business metrics
3. Create dimension tables
4. Create fact tables
5. Optimize for query patterns

**Expected Output**: Gold layer tables

**Validation**: Metrics match business requirements

---

### I49: Change Data Capture (CDC)
**Difficulty**: ⭐⭐⭐ | **Time**: 55 min

**Objectives**: Process CDC events

**Requirements**:
1. Parse CDC event types (I/U/D)
2. Apply inserts
3. Apply updates
4. Apply deletes (soft delete preferred)
5. Handle out-of-order events

**Expected Output**: CDC processing pipeline

**Validation**: Final state matches source database

---

### I50: Streaming Delta Writes
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Stream to Delta sink

**Requirements**:
1. Write stream to Delta table
2. Use merge for upserts (foreachBatch)
3. Handle checkpointing
4. Optimize for streaming
5. Monitor write latency

**Expected Output**: Streaming Delta pipeline

**Validation**: Data continuously written; recoverable

---

### I51: Performance Benchmarking
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Measure and compare performance

**Requirements**:
1. Create benchmark framework
2. Measure query time
3. Measure shuffle bytes
4. Compare optimizations
5. Generate performance report

**Expected Output**: Benchmark results

**Validation**: Metrics accurately captured

---

### I52: Cost-Based Optimizer
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: CBO configuration and usage

**Requirements**:
1. Collect table statistics
2. Collect column statistics
3. Enable cost-based optimization
4. Analyze plan changes
5. Compare with rule-based

**Expected Output**: CBO-optimized queries

**Validation**: Better join ordering with CBO

---

### I53: Data Serialization Formats
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Compare Parquet, ORC, Avro

**Requirements**:
1. Write data in all three formats
2. Compare file sizes
3. Compare read performance
4. Compare schema evolution capabilities
5. Document use cases for each

**Expected Output**: Format comparison report

**Validation**: Accurate measurements

---

### I54: Pushdown Optimization
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Predicate and projection pushdown

**Requirements**:
1. Verify predicate pushdown to Parquet
2. Verify column pruning
3. Pushdown through JDBC
4. Analyze data scanned
5. Measure impact

**Expected Output**: Pushdown verification

**Validation**: Plans show pushed predicates

---

### I55: Data Compression
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: Compression codecs comparison

**Requirements**:
1. Compare snappy, gzip, zstd, lz4
2. Measure compression ratio
3. Measure read/write speed
4. Choose based on use case
5. Configure default codec

**Expected Output**: Compression comparison

**Validation**: Measurements match expectations

---

### I56: Retry and Idempotency
**Difficulty**: ⭐⭐⭐ | **Time**: 45 min

**Objectives**: Build reliable data pipelines

**Requirements**:
1. Implement retry logic
2. Make writes idempotent
3. Use unique write paths
4. Handle partial failures
5. Test failure scenarios

**Expected Output**: Robust pipeline with retries

**Validation**: Reruns produce same results

---

### I57: Configuration Management
**Difficulty**: ⭐⭐⭐ | **Time**: 35 min

**Objectives**: External configuration for Spark jobs

**Requirements**:
1. Use configuration files
2. Environment-specific configs
3. Override with command line
4. Secure sensitive values
5. Document configurations

**Expected Output**: Configuration framework

**Validation**: Configs loaded correctly per environment

---

### I58: Dependency Management
**Difficulty**: ⭐⭐⭐ | **Time**: 40 min

**Objectives**: Package Python dependencies

**Requirements**:
1. Create requirements.txt
2. Package with --py-files
3. Use conda environment
4. Handle C library dependencies
5. Test in cluster environment

**Expected Output**: Packaged dependencies

**Validation**: Job runs with all dependencies

---

### I59: Airflow DAG for Spark
**Difficulty**: ⭐⭐⭐ | **Time**: 50 min

**Objectives**: Orchestrate Spark with Airflow

**Requirements**:
1. Create Airflow DAG
2. Use SparkSubmitOperator
3. Pass dynamic parameters
4. Handle dependencies between tasks
5. Configure retries and alerts

**Expected Output**: Airflow DAG file

**Validation**: DAG runs Spark job successfully

---

### I60: Intermediate Capstone - ETL Pipeline
**Difficulty**: ⭐⭐⭐ | **Time**: 90 min

**Objectives**: Complete batch ETL with best practices

**Requirements**:
1. Ingest data from multiple sources (CSV, JSON, JDBC)
2. Implement bronze/silver/gold layers
3. Apply data quality checks (fail job if critical)
4. Optimize for:
   - Partitioning strategy
   - File sizes (128-256MB)
   - No shuffle where possible
5. Handle incremental updates
6. Write comprehensive tests
7. Package for spark-submit
8. Create Airflow DAG

**Expected Output**:
- Three-layer Delta tables
- DQ report
- Performance metrics
- Test suite
- DAG definition

**Validation Checks**:
- No critical DQ failures
- File sizes within range
- Job completes in <10 minutes for 1M rows
- Tests pass
- Rerun produces identical results

**Stretch**: Add data lineage tracking; implement alerting

---

## Advanced Level (A01-A60)

### A01: Production Cluster Configuration
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Configure Spark for production workloads

**Requirements**:
1. Calculate optimal executor count and sizing
2. Configure dynamic allocation
3. Set memory overhead correctly
4. Configure speculation for stragglers
5. Set up external shuffle service
6. Document resource calculations

**Expected Output**: Production spark-defaults.conf

**Validation**: Application runs stable under load

**Formulas**:
```
executor_memory = (node_memory - overhead) / executors_per_node
executor_cores = node_cores / executors_per_node (max 5)
num_executors = (total_cores / executor_cores) - 1 (for driver)
```

---

### A02: Dynamic Resource Allocation
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 45 min

**Objectives**: Auto-scale executors based on workload

**Requirements**:
1. Enable dynamic allocation
2. Configure min/max executors
3. Set idle timeout
4. Configure scheduler settings
5. Monitor allocation decisions

**Expected Output**: Dynamic allocation configuration

**Validation**: Executors scale up/down appropriately

---

### A03: Cluster Mode Deployment
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Deploy in cluster mode on YARN/K8s

**Requirements**:
1. Configure cluster mode submission
2. Handle driver log access
3. Configure application master resources
4. Set up client mode alternative
5. Handle failures in cluster mode

**Expected Output**: Cluster mode deployment guide

**Validation**: App runs successfully in cluster mode

---

### A04: Kubernetes Deployment
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Run Spark on Kubernetes

**Requirements**:
1. Build Spark image for K8s
2. Configure service account
3. Submit to Kubernetes cluster
4. Configure persistent volumes
5. Monitor pods and logs

**Expected Output**: K8s deployment manifests

**Validation**: Job completes on Kubernetes

---

### A05: Custom Partitioners
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Implement custom data distribution

**Requirements**:
1. Understand hash partitioner limitations
2. Implement range partitioner for skewed data
3. Create custom partitioner for geographic data
4. Preserve partitioning through operations
5. Verify partition distribution

**Expected Output**: Custom partitioner implementation

**Validation**: Even data distribution across partitions

---

### A06: Advanced Skew Handling
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Handle extreme data skew

**Requirements**:
1. Identify skew patterns (key, partition)
2. Implement partial broadcast for skewed keys
3. Implement iterative salting
4. Combine multiple skew techniques
5. Compare with AQE skew handling

**Expected Output**: Comprehensive skew handling framework

**Validation**: 90th percentile task time within 2x of median

**Performance**: No task >5x median duration

---

### A07: Stateful Streaming Operations
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: mapGroupsWithState, flatMapGroupsWithState

**Requirements**:
1. Implement session windowing
2. Track user state across events
3. Handle state timeouts
4. Manage state size
5. Implement custom aggregations

**Expected Output**: Stateful streaming application

**Validation**: State correctly maintained across batches

---

### A08: Streaming Exactly-Once Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Ensure end-to-end exactly-once

**Requirements**:
1. Understand exactly-once guarantees
2. Configure idempotent sinks
3. Use transactional writes (Kafka)
4. Handle reprocessing scenarios
5. Verify with failure injection

**Expected Output**: Exactly-once streaming pipeline

**Validation**: No duplicates after simulated failures

---

### A09: Complex Event Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Detect patterns in event streams

**Requirements**:
1. Detect session boundaries
2. Identify fraud patterns (rapid transactions)
3. Calculate time between events
4. Implement sequential pattern detection
5. Generate alerts for anomalies

**Expected Output**: CEP pipeline

**Validation**: Patterns correctly detected in test data

---

### A10: Multi-Stream Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Process multiple streams together

**Requirements**:
1. Read from multiple Kafka topics
2. Union streams with different schemas
3. Join streams with watermarks
4. Handle late data across streams
5. Manage consolidated state

**Expected Output**: Multi-stream processing application

**Validation**: All streams correctly processed

---

### A11: Streaming State Management
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Optimize streaming state

**Requirements**:
1. Monitor state size
2. Configure RocksDB state store
3. Implement state TTL
4. Handle state migration
5. Backup and restore state

**Expected Output**: Optimized state configuration

**Validation**: State size bounded; recoverable

---

### A12: Delta Live Tables (DLT)
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Declarative ETL with DLT (if using Databricks)

**Requirements**:
1. Define DLT pipeline
2. Set data quality expectations
3. Implement bronze/silver/gold tables
4. Handle pipeline failures
5. Monitor pipeline metrics

**Expected Output**: DLT pipeline definition

**Validation**: Pipeline runs with quality checks

---

### A13: Iceberg Tables
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Use Apache Iceberg for table format

**Requirements**:
1. Create Iceberg table
2. Perform ACID operations
3. Time travel queries
4. Schema evolution
5. Compare with Delta Lake

**Expected Output**: Iceberg table implementation

**Validation**: ACID guarantees verified

---

### A14: Hudi Tables
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Use Apache Hudi for upserts

**Requirements**:
1. Create Hudi table (COW vs MOR)
2. Perform upserts
3. Incremental queries
4. Time travel
5. Compare with Delta/Iceberg

**Expected Output**: Hudi table implementation

**Validation**: Upserts correctly applied

---

### A15: MLlib - Feature Engineering
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Build ML feature pipeline

**Requirements**:
1. Use VectorAssembler
2. Implement StringIndexer/OneHotEncoder
3. Normalize/standardize features
4. Handle categorical variables
5. Create reusable Pipeline

**Expected Output**: Feature engineering Pipeline

**Validation**: Features correctly transformed

---

### A16: MLlib - Classification
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Train classification model

**Requirements**:
1. Split data (train/test)
2. Train LogisticRegression or RandomForest
3. Evaluate with MulticlassMetrics
4. Tune hyperparameters
5. Save/load model

**Expected Output**: Trained classifier with metrics

**Validation**: Accuracy >80% on test set

---

### A17: MLlib - Regression
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Train regression model

**Requirements**:
1. Train LinearRegression or GBTRegressor
2. Evaluate with RegressionEvaluator
3. Analyze feature importance
4. Cross-validation
5. Compare models

**Expected Output**: Trained regressor with metrics

**Validation**: RMSE within acceptable range

---

### A18: MLlib - Clustering
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Customer segmentation with clustering

**Requirements**:
1. Prepare features for clustering
2. Train KMeans model
3. Determine optimal K (elbow method)
4. Analyze cluster characteristics
5. Assign customers to clusters

**Expected Output**: Customer segments

**Validation**: Clusters meaningful; stable

---

### A19: MLlib - Model Serving
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Deploy ML model for inference

**Requirements**:
1. Save trained model
2. Load for batch scoring
3. Integrate with streaming
4. Handle model versioning
5. A/B testing setup

**Expected Output**: Model serving pipeline

**Validation**: Predictions match expected

---

### A20: GraphFrames - Basics
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Graph analytics with GraphFrames

**Requirements**:
1. Create graph from DataFrames
2. Query vertices and edges
3. Run graph algorithms (PageRank)
4. Find connected components
5. Shortest paths

**Expected Output**: Graph analysis results

**Validation**: Algorithm results verified

---

### A21: GraphFrames - Network Analysis
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Social network analysis

**Requirements**:
1. Build social network graph
2. Find influencers (PageRank)
3. Detect communities
4. Calculate centrality measures
5. Find triangles

**Expected Output**: Network analysis report

**Validation**: Metrics match expected for test graph

---

### A22: Advanced Window Functions
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Complex window specifications

**Requirements**:
1. Session windows (gap-based)
2. Percentile calculations
3. Median per group
4. First/last non-null value
5. Multiple windows in single query

**Expected Output**: Advanced analytics DataFrame

**Validation**: Calculations verified manually

---

### A23: Query Optimization Techniques
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Optimize slow queries

**Requirements**:
1. Analyze slow query explain plan
2. Rewrite for better performance
3. Use appropriate hints
4. Avoid common anti-patterns
5. Document optimization techniques

**Expected Output**: Optimized queries (2x+ improvement)

**Validation**: Query time reduced significantly

---

### A24: Memory Pressure Debugging
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Debug and fix OOM errors

**Requirements**:
1. Reproduce OOM scenario
2. Analyze task memory usage
3. Identify memory-heavy operations
4. Apply spill-to-disk strategies
5. Tune memory configurations

**Expected Output**: Resolution steps for OOM

**Validation**: Job completes without OOM

---

### A25: GC Tuning
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Optimize garbage collection

**Requirements**:
1. Choose GC algorithm (G1GC recommended)
2. Configure heap regions
3. Monitor GC metrics
4. Reduce object creation
5. Handle long GC pauses

**Expected Output**: GC configuration

**Validation**: GC time <10% of task time

---

### A26: Data Lake Architecture
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Design production data lake

**Requirements**:
1. Design zone architecture
2. Define data contracts
3. Implement metadata management
4. Set up data catalog
5. Implement access control

**Expected Output**: Data lake design document

**Validation**: Design addresses all requirements

---

### A27: Data Lineage Tracking
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Track data transformations

**Requirements**:
1. Capture input/output metadata
2. Log transformation details
3. Build lineage graph
4. Query lineage history
5. Integrate with catalog

**Expected Output**: Lineage tracking system

**Validation**: Lineage accurately captured

---

### A28: Schema Registry Integration
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Centralized schema management

**Requirements**:
1. Integrate with Confluent Schema Registry
2. Serialize with Avro
3. Handle schema evolution
4. Validate schema compatibility
5. Use with Kafka streaming

**Expected Output**: Schema registry integration

**Validation**: Schema validation working

---

### A29: Multi-Tenancy
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Isolate workloads

**Requirements**:
1. Configure fair scheduler
2. Set up resource pools
3. Implement queue-based submission
4. Monitor per-tenant resources
5. Prevent noisy neighbors

**Expected Output**: Multi-tenant configuration

**Validation**: Resources isolated between tenants

---

### A30: Cost Optimization
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Minimize compute costs

**Requirements**:
1. Right-size executors
2. Use spot/preemptible instances
3. Optimize data storage
4. Reduce shuffle data
5. Schedule during off-peak

**Expected Output**: Cost optimization report

**Validation**: Measurable cost reduction

---

### A31: Security - Authentication
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Secure Spark cluster access

**Requirements**:
1. Configure Kerberos authentication
2. Set up SSL/TLS encryption
3. Configure SASL for Kafka
4. Handle keytab management
5. Secure credential storage

**Expected Output**: Secured cluster configuration

**Validation**: Unauthorized access denied

---

### A32: Security - Authorization
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Fine-grained access control

**Requirements**:
1. Configure Apache Ranger/Sentry
2. Table and column-level security
3. Row-level filtering
4. Audit logging
5. Masking sensitive data

**Expected Output**: Authorization policies

**Validation**: Access controls enforced

---

### A33: CI/CD for Spark
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Automated testing and deployment

**Requirements**:
1. Set up CI pipeline (GitHub Actions/Jenkins)
2. Run unit tests in pipeline
3. Integration tests with sample data
4. Package and artifact deployment
5. Environment promotion

**Expected Output**: CI/CD pipeline configuration

**Validation**: Pipeline runs on code changes

---

### A34: Blue-Green Deployment
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Zero-downtime deployments

**Requirements**:
1. Implement blue-green strategy
2. Version streaming checkpoints
3. Handle schema migrations
4. Rollback procedures
5. Traffic switching

**Expected Output**: Deployment strategy document

**Validation**: No data loss during deployment

---

### A35: Monitoring and Alerting
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Production monitoring setup

**Requirements**:
1. Export Spark metrics to Prometheus
2. Create Grafana dashboards
3. Set up alerts for SLA breaches
4. Monitor streaming lag
5. Alert on job failures

**Expected Output**: Monitoring stack configuration

**Validation**: Alerts fire on test incidents

---

### A36: SLA Management
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Meet processing SLAs

**Requirements**:
1. Define SLA metrics
2. Implement SLA tracking
3. Automatic scaling for SLA
4. SLA breach notifications
5. SLA reporting

**Expected Output**: SLA management framework

**Validation**: SLAs tracked and reported

---

### A37: Disaster Recovery
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Business continuity planning

**Requirements**:
1. Design backup strategy
2. Implement checkpoint mirroring
3. Cross-region replication
4. RTO/RPO calculations
5. DR testing procedures

**Expected Output**: DR plan and implementation

**Validation**: Recovery tested successfully

---

### A38: Data Mesh Implementation
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Decentralized data architecture

**Requirements**:
1. Define domain boundaries
2. Create data products
3. Implement federated governance
4. Self-serve infrastructure
5. Discoverability features

**Expected Output**: Data mesh architecture

**Validation**: Domains can operate independently

---

### A39: Real-Time Feature Store
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: ML feature management

**Requirements**:
1. Batch feature computation
2. Streaming feature updates
3. Feature versioning
4. Point-in-time lookups
5. Online/offline consistency

**Expected Output**: Feature store implementation

**Validation**: Features available for training and serving

---

### A40: Event Sourcing with Spark
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 65 min

**Objectives**: Event-driven architecture

**Requirements**:
1. Design event schema
2. Implement event store
3. Rebuild state from events
4. Handle event versioning
5. Compact events periodically

**Expected Output**: Event sourcing system

**Validation**: State correctly rebuilt from events

---

### A41: Lambda Architecture
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Combine batch and streaming

**Requirements**:
1. Implement batch layer (accurate)
2. Implement speed layer (fast)
3. Implement serving layer
4. Handle recomputation
5. Merge batch and speed results

**Expected Output**: Lambda architecture implementation

**Validation**: Results combine correctly

---

### A42: Kappa Architecture
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 65 min

**Objectives**: Stream-only architecture

**Requirements**:
1. Design streaming-first pipeline
2. Handle reprocessing via stream replay
3. State management at scale
4. Handle late arrivals
5. Compare with Lambda approach

**Expected Output**: Kappa architecture implementation

**Validation**: Reprocessing produces correct results

---

### A43: Advanced CDC Patterns
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Complex change data capture

**Requirements**:
1. Handle multi-table CDC
2. Maintain foreign key relationships
3. Order events correctly
4. Handle schema changes
5. CDC as streaming pipeline

**Expected Output**: Production CDC pipeline

**Validation**: Target matches source at all times

---

### A44: Time-Series Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Time-series analytics at scale

**Requirements**:
1. Resample time series
2. Fill missing values
3. Calculate moving statistics
4. Detect anomalies
5. Forecast with MLlib

**Expected Output**: Time-series analysis pipeline

**Validation**: Statistics match pandas equivalent

---

### A45: Geospatial Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Location-based analytics

**Requirements**:
1. Use spatial UDFs (Sedona/GeoSpark)
2. Point-in-polygon queries
3. Distance calculations
4. Spatial joins
5. Geofencing

**Expected Output**: Geospatial analysis pipeline

**Validation**: Spatial queries return correct results

---

### A46: NLP with Spark
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Text processing at scale

**Requirements**:
1. Tokenization and cleaning
2. TF-IDF computation
3. Word2Vec embeddings
4. Sentiment analysis
5. Topic modeling (LDA)

**Expected Output**: NLP pipeline

**Validation**: Text features correctly computed

---

### A47: Image Processing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Image data at scale

**Requirements**:
1. Read images at scale
2. Basic image transformations
3. Feature extraction
4. Integrate with deep learning
5. Handle binary data efficiently

**Expected Output**: Image processing pipeline

**Validation**: Images processed correctly

---

### A48: Recommendation System
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Build recommendation engine

**Requirements**:
1. Implement ALS collaborative filtering
2. Handle implicit feedback
3. Generate recommendations
4. Evaluate with ranking metrics
5. Scale to millions of users

**Expected Output**: Recommendation system

**Validation**: Recommendations are relevant

---

### A49: A/B Testing Framework
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Experiment analysis at scale

**Requirements**:
1. Calculate experiment metrics
2. Statistical significance testing
3. Segment analysis
4. Handle ratio metrics
5. Reporting automation

**Expected Output**: A/B testing analysis pipeline

**Validation**: Statistical calculations verified

---

### A50: Data Quality Framework
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 65 min

**Objectives**: Enterprise data quality

**Requirements**:
1. Define DQ rules declaratively
2. Implement Great Expectations or similar
3. Version DQ expectations
4. Quarantine bad records
5. DQ trend reporting

**Expected Output**: DQ framework implementation

**Validation**: All DQ scenarios handled

---

### A51: Metadata-Driven ETL
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Configuration-driven pipelines

**Requirements**:
1. Define transformations in metadata
2. Generate Spark code from config
3. Handle schema changes automatically
4. Support common patterns
5. Validate configurations

**Expected Output**: Metadata-driven ETL framework

**Validation**: New sources added without code changes

---

### A52: Data Virtualization
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Query multiple sources unified

**Requirements**:
1. Register multiple data sources
2. Unified query interface
3. Push down operations
4. Cache frequently used data
5. Handle heterogeneous schemas

**Expected Output**: Data virtualization layer

**Validation**: Queries span multiple sources

---

### A53: Spark Connect
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Remote Spark access (Spark 3.4+)

**Requirements**:
1. Set up Spark Connect server
2. Connect from thin client
3. Execute remote operations
4. Handle large result sets
5. Authentication setup

**Expected Output**: Spark Connect deployment

**Validation**: Remote queries successful

---

### A54: Photon Engine (Databricks)
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 45 min

**Objectives**: Photon runtime optimization

**Requirements**:
1. Enable Photon engine
2. Identify compatible operations
3. Benchmark against JVM
4. Handle fallback scenarios
5. Optimize for Photon

**Expected Output**: Photon optimization guide

**Validation**: Measurable performance improvement

---

### A55: Delta Sharing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Cross-organization data sharing

**Requirements**:
1. Set up Delta Sharing server
2. Create shares and recipients
3. Query shared tables
4. Handle access revocation
5. Audit sharing access

**Expected Output**: Delta Sharing implementation

**Validation**: Cross-org queries successful

---

### A56: Spark Troubleshooting Toolkit
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 70 min

**Objectives**: Build debugging toolkit

**Requirements**:
1. Automated log analysis
2. Common error detection
3. Performance anomaly detection
4. Runbook automation
5. Root cause analysis

**Expected Output**: Troubleshooting automation

**Validation**: Known issues auto-detected

---

### A57: Capacity Planning
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 60 min

**Objectives**: Plan cluster resources

**Requirements**:
1. Analyze historical usage
2. Project future requirements
3. Model different scenarios
4. Cost trade-off analysis
5. Recommendations report

**Expected Output**: Capacity planning model

**Validation**: Projections match actuals

---

### A58: Performance Regression Testing
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 55 min

**Objectives**: Catch performance regressions

**Requirements**:
1. Define performance baselines
2. Automated performance tests
3. Compare against baselines
4. Alert on regressions
5. Historical tracking

**Expected Output**: Performance test suite

**Validation**: Known regressions detected

---

### A59: Technical Debt Management
**Difficulty**: ⭐⭐⭐⭐ | **Time**: 50 min

**Objectives**: Maintain code quality

**Requirements**:
1. Identify common Spark anti-patterns
2. Automated code analysis
3. Prioritize refactoring
4. Track technical debt metrics
5. Refactoring guidelines

**Expected Output**: Tech debt assessment

**Validation**: Issues identified and prioritized

---

### A60: Advanced Capstone - Production System
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 120 min

**Objectives**: Production-ready data platform

**Requirements**:
1. Design complete data platform
2. Implement ingestion from 3+ sources
3. Bronze/Silver/Gold with Delta Lake
4. Real-time streaming component
5. ML feature store integration
6. Full monitoring stack
7. CI/CD pipeline
8. Security implementation
9. DR strategy
10. Documentation

**Expected Output**: Complete data platform

**Validation Checks**:
- All data flows working
- SLAs defined and met
- Monitoring active
- Security controls in place
- Recovery tested
- Documentation complete

---

## Capstone Projects (C01-C05)

### C01: E-Commerce Analytics Platform
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 4-6 hours

**Scenario**: Build complete analytics for an e-commerce company

**Requirements**:

**Data Ingestion**:
- Load transactions (10M+ rows), customers (1M), products (100K)
- Ingest clickstream data (streaming)
- Handle late-arriving transaction updates

**Processing**:
- Bronze: Raw data with metadata
- Silver: Cleaned, deduplicated, validated
- Gold: Business aggregations

**Analytics Requirements**:
1. Daily/weekly/monthly sales by category, region
2. Customer lifetime value calculation
3. Product affinity analysis (frequently bought together)
4. Conversion funnel from clickstream
5. Real-time dashboard metrics

**Technical Requirements**:
- No collect() on large data
- File sizes 128-256MB
- Incremental processing
- Job completes <15 min for batch
- Streaming latency <1 min

**Deliverables**:
- Complete codebase
- Airflow DAGs
- DQ report
- Performance metrics
- Documentation

---

### C02: Real-Time Fraud Detection
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 4-6 hours

**Scenario**: Detect fraudulent transactions in real-time

**Requirements**:

**Data Sources**:
- Transaction stream from Kafka (1000 events/sec)
- Historical transactions for training
- Customer profile data

**ML Pipeline**:
1. Feature engineering (velocity, patterns, anomalies)
2. Train fraud detection model (MLlib)
3. Deploy for real-time scoring

**Streaming Pipeline**:
1. Ingest from Kafka
2. Enrich with customer data
3. Compute real-time features
4. Score with ML model
5. Alert on high-risk (Delta + alerts)

**Technical Requirements**:
- End-to-end latency <30 seconds
- Exactly-once processing
- Handle 10K events/sec spike
- Model versioning
- Graceful degradation

**Deliverables**:
- Streaming application
- ML training pipeline
- Model serving code
- Monitoring dashboards
- Alert configuration

---

### C03: Lakehouse with Full Lineage
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 5-7 hours

**Scenario**: Build production lakehouse with data governance

**Requirements**:

**Architecture**:
- Multi-zone data lake (raw/bronze/silver/gold)
- Delta Lake with time travel
- Data catalog integration
- Schema registry

**Governance**:
1. Column-level lineage tracking
2. Data quality checks at each layer
3. Access control policies
4. PII detection and masking
5. Audit logging

**Processing**:
- Incremental ETL for all layers
- CDC from source databases
- SCD Type 2 for dimensions
- Aggregation for facts

**Technical Requirements**:
- Metadata-driven transformations
- Zero-downtime deployments
- Full data lineage graph
- Compliance reporting

**Deliverables**:
- Lakehouse implementation
- Lineage tracking system
- DQ framework
- Security policies
- Governance documentation

---

### C04: Performance Optimization Challenge
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 3-4 hours

**Scenario**: Optimize poorly performing Spark jobs

**Given**: Intentionally slow Spark jobs with these issues:
- Extreme data skew (one key has 80% data)
- Small files problem (10,000 files, 1MB each)
- Expensive UDFs instead of built-ins
- Wrong join strategies
- No caching of reused data
- Over-partitioned data
- Collect() on large data
- Suboptimal file format

**Requirements**:
1. Analyze each job using Spark UI
2. Document all identified issues
3. Implement optimizations
4. Achieve minimum 5x improvement
5. Document improvements with evidence

**Deliverables**:
- Before/after Spark UI screenshots
- Optimization report
- Optimized code
- Performance metrics
- Lessons learned

**Validation**:
- Job runtime reduced by 5x+
- Memory usage reduced by 50%+
- Shuffle reduced significantly

---

### C05: Multi-Cloud Data Platform
**Difficulty**: ⭐⭐⭐⭐⭐ | **Time**: 6-8 hours

**Scenario**: Build portable Spark platform across clouds

**Requirements**:

**Infrastructure**:
- Kubernetes-based Spark deployment
- Works on AWS EKS, GCP GKE, Azure AKS
- Infrastructure as Code (Terraform/Pulumi)

**Data Layer**:
- Cloud-agnostic storage abstraction
- Delta Lake on cloud object storage
- Cross-cloud data synchronization

**Processing**:
- Batch and streaming pipelines
- ML model training and serving
- Feature store

**Operations**:
- Unified monitoring across clouds
- Cost management dashboard
- Automated failover

**Technical Requirements**:
- Single codebase for all clouds
- Consistent configurations
- Disaster recovery across regions
- Cost optimization per cloud

**Deliverables**:
- IaC for all three clouds
- Spark application code
- CI/CD pipelines
- Monitoring setup
- Cost analysis
- Architecture documentation

---

## Summary Statistics

| Level | Assignments | Estimated Time |
|-------|-------------|----------------|
| Beginner (B01-B50) | 50 | ~25 hours |
| Intermediate (I01-I60) | 60 | ~45 hours |
| Advanced (A01-A60) | 60 | ~55 hours |
| Capstones (C01-C05) | 5 | ~25 hours |
| **Total** | **175** | **~150 hours** |

---

## Learning Path Recommendations

### Path 1: Data Engineer (Batch Focus)
B01-B50 → I01-I30, I42-I60 → A01-A06, A22-A30, A33-A37, A50-A51 → C01, C03

### Path 2: Streaming Engineer
B01-B30 → I01-I15, I31-I50 → A07-A14, A28, A41-A43 → C02

### Path 3: ML Engineer
B01-B50 → I01-I30 → A15-A21, A39, A46-A49 → C02

### Path 4: Platform Engineer
B01-B20 → I21-I30, I57-I60 → A01-A04, A29-A37, A52-A58 → C04, C05

---



