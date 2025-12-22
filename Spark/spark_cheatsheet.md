# Apache Spark Cheatsheet

> Quick reference for Spark concepts, syntax, and best practices

---

## Table of Contents
1. [SparkSession](#1-sparksession)
2. [Data Loading](#2-data-loading)
3. [DataFrame Operations](#3-dataframe-operations)
4. [Spark SQL](#4-spark-sql)
5. [Window Functions](#5-window-functions)
6. [Joins](#6-joins)
7. [Aggregations](#7-aggregations)
8. [RDD Operations](#8-rdd-operations)
9. [Structured Streaming](#9-structured-streaming)
10. [Delta Lake](#10-delta-lake)
11. [Performance Tuning](#11-performance-tuning)
12. [MLlib](#12-mllib)
13. [Configuration](#13-configuration)
14. [Testing](#14-testing)
15. [Common Patterns](#15-common-patterns)

---

## 1. SparkSession

```python
from pyspark.sql import SparkSession

# Create session
spark = SparkSession.builder \
    .appName("MyApp") \
    .master("local[*]") \
    .config("spark.sql.shuffle.partitions", "200") \
    .config("spark.sql.adaptive.enabled", "true") \
    .getOrCreate()

# Access SparkContext
sc = spark.sparkContext

# Stop session
spark.stop()
```

**Key Configs:**
| Config | Default | Description |
|--------|---------|-------------|
| `spark.sql.shuffle.partitions` | 200 | Partitions for shuffles |
| `spark.sql.adaptive.enabled` | true (3.2+) | Enable AQE |
| `spark.executor.memory` | 1g | Executor heap |
| `spark.driver.memory` | 1g | Driver heap |

---

## 2. Data Loading

### Read Formats
```python
# CSV
df = spark.read.csv("path.csv", header=True, inferSchema=True)
df = spark.read.option("header", "true").csv("path.csv")

# JSON
df = spark.read.json("path.json")
df = spark.read.option("multiLine", "true").json("path.json")

# Parquet
df = spark.read.parquet("path.parquet")

# ORC
df = spark.read.orc("path.orc")

# Delta
df = spark.read.format("delta").load("path")

# JDBC
df = spark.read.format("jdbc") \
    .option("url", "jdbc:postgresql://host:5432/db") \
    .option("dbtable", "schema.table") \
    .option("user", "user") \
    .option("password", "pass") \
    .option("numPartitions", 10) \
    .option("partitionColumn", "id") \
    .option("lowerBound", 1) \
    .option("upperBound", 1000000) \
    .load()
```

### Explicit Schema
```python
from pyspark.sql.types import *

schema = StructType([
    StructField("id", IntegerType(), nullable=False),
    StructField("name", StringType()),
    StructField("amount", DecimalType(10, 2)),
    StructField("created_at", TimestampType())
])

df = spark.read.schema(schema).csv("path.csv", header=True)
```

### Write Formats
```python
# Parquet (default)
df.write.parquet("path", mode="overwrite")

# Partitioned
df.write.partitionBy("date", "region").parquet("path")

# CSV
df.coalesce(1).write.csv("path", header=True, mode="overwrite")

# Delta
df.write.format("delta").mode("overwrite").save("path")

# JDBC
df.write.format("jdbc") \
    .option("url", "jdbc:postgresql://host/db") \
    .option("dbtable", "table") \
    .option("batchsize", 10000) \
    .mode("append").save()
```

**Write Modes:** `overwrite`, `append`, `ignore`, `error` (default)

---

## 3. DataFrame Operations

### Column Selection & Creation
```python
from pyspark.sql.functions import col, lit, when, concat

# Select columns
df.select("col1", "col2")
df.select(col("col1"), df.col2)
df.select(df["col1"])

# Add/rename columns
df.withColumn("new_col", col("old_col") * 2)
df.withColumnRenamed("old_name", "new_name")

# Drop columns
df.drop("col1", "col2")

# Conditional
df.withColumn("tier", 
    when(col("amount") > 1000, "high")
    .when(col("amount") > 100, "medium")
    .otherwise("low")
)
```

### Filtering
```python
# Filter rows
df.filter(col("age") > 25)
df.filter("age > 25")  # SQL style
df.where(col("status") == "active")

# Multiple conditions
df.filter((col("age") > 25) & (col("city") == "NYC"))
df.filter((col("age") > 25) | (col("city") == "NYC"))

# Null handling
df.filter(col("name").isNotNull())
df.filter(col("name").isNull())

# IN clause
df.filter(col("status").isin("active", "pending"))
```

### Sorting
```python
from pyspark.sql.functions import asc, desc

df.orderBy("column")
df.orderBy(col("column").desc())
df.orderBy(asc("col1"), desc("col2"))
df.sort("column")  # alias
```

### Distinct & Dedup
```python
df.distinct()
df.dropDuplicates(["id"])  # dedupe on specific columns

# Keep first occurrence with window
from pyspark.sql.window import Window
w = Window.partitionBy("id").orderBy("timestamp")
df.withColumn("rn", row_number().over(w)).filter(col("rn") == 1)
```

### Null Handling
```python
# Drop nulls
df.na.drop()  # any column has null
df.na.drop(subset=["col1", "col2"])
df.na.drop(how="all")  # all columns null

# Fill nulls
df.na.fill(0)  # all numeric
df.na.fill({"col1": 0, "col2": "unknown"})
df.fillna({"col": "default"})

# Coalesce
from pyspark.sql.functions import coalesce
df.select(coalesce(col("col1"), col("col2"), lit("default")))
```

### String Functions
```python
from pyspark.sql.functions import (
    upper, lower, trim, ltrim, rtrim,
    concat, concat_ws, substring, split,
    regexp_replace, regexp_extract, length
)

df.select(
    upper(col("name")),
    trim(col("desc")),
    concat_ws(" ", col("first"), col("last")),
    substring(col("code"), 1, 3),
    split(col("tags"), ","),
    regexp_replace(col("text"), r"\d+", ""),
    regexp_extract(col("email"), r"@(.+)", 1)
)
```

### Date/Time Functions
```python
from pyspark.sql.functions import (
    current_date, current_timestamp,
    year, month, dayofmonth, dayofweek, hour,
    date_add, date_sub, datediff, months_between,
    to_date, to_timestamp, date_format
)

df.select(
    year(col("created_at")),
    datediff(current_date(), col("order_date")),
    date_add(col("start_date"), 30),
    to_date(col("date_str"), "yyyy-MM-dd"),
    date_format(col("ts"), "yyyy-MM-dd HH:mm")
)
```

### Type Casting
```python
df.select(col("amount").cast("double"))
df.select(col("date_str").cast("date"))
df.withColumn("int_col", col("str_col").cast(IntegerType()))
```

---

## 4. Spark SQL

```python
# Create temp view
df.createOrReplaceTempView("my_table")
df.createGlobalTempView("global_table")

# Query
result = spark.sql("""
    SELECT 
        category,
        SUM(amount) as total,
        COUNT(*) as cnt
    FROM my_table
    WHERE status = 'completed'
    GROUP BY category
    HAVING COUNT(*) > 10
    ORDER BY total DESC
""")

# Access global temp view
spark.sql("SELECT * FROM global_temp.global_table")
```

### Explain Plans
```python
df.explain()           # Physical plan
df.explain(True)       # All plans
df.explain("extended") # Same as True
df.explain("codegen")  # Generated code
df.explain("cost")     # With costs
df.explain("formatted")# Readable format
```

---

## 5. Window Functions

```python
from pyspark.sql.window import Window
from pyspark.sql.functions import (
    row_number, rank, dense_rank, ntile,
    lag, lead, first, last,
    sum, avg, min, max, count
)

# Define window
w = Window.partitionBy("customer_id").orderBy("order_date")

# Ranking
df.select(
    row_number().over(w).alias("row_num"),
    rank().over(w).alias("rank"),
    dense_rank().over(w).alias("dense_rank"),
    ntile(4).over(w).alias("quartile")
)

# Analytics
df.select(
    lag("amount", 1).over(w).alias("prev_amount"),
    lead("amount", 1).over(w).alias("next_amount"),
    first("amount").over(w).alias("first_amount"),
    last("amount").over(w.rowsBetween(Window.unboundedPreceding, Window.unboundedFollowing))
)

# Running calculations
w_running = Window.partitionBy("customer_id").orderBy("date") \
    .rowsBetween(Window.unboundedPreceding, Window.currentRow)

df.withColumn("running_total", sum("amount").over(w_running))

# Rolling window (last 7 rows)
w_rolling = Window.partitionBy("id").orderBy("date") \
    .rowsBetween(-6, Window.currentRow)

df.withColumn("rolling_avg", avg("value").over(w_rolling))
```

**Frame Types:**
- `rowsBetween(start, end)` - Row-based
- `rangeBetween(start, end)` - Value-based

**Constants:** `Window.unboundedPreceding`, `Window.unboundedFollowing`, `Window.currentRow`

---

## 6. Joins

```python
# Inner join (default)
df1.join(df2, df1.id == df2.id)
df1.join(df2, "id")  # Same column name
df1.join(df2, ["id", "name"])  # Multiple columns

# Join types
df1.join(df2, "id", "left")        # left_outer
df1.join(df2, "id", "right")       # right_outer  
df1.join(df2, "id", "outer")       # full_outer
df1.join(df2, "id", "left_semi")   # IN subquery
df1.join(df2, "id", "left_anti")   # NOT IN subquery
df1.join(df2)                       # cross join (dangerous!)

# Broadcast join (for small tables)
from pyspark.sql.functions import broadcast
big_df.join(broadcast(small_df), "id")

# SQL hints
df1.hint("broadcast").join(df2, "id")
df1.hint("merge").join(df2, "id")  # Sort merge
df1.hint("shuffle_hash").join(df2, "id")
```

**Join Strategies:**
| Strategy | When Used | Notes |
|----------|-----------|-------|
| BroadcastHashJoin | Small table (<10MB) | Fastest, no shuffle |
| SortMergeJoin | Large tables | Default for large |
| ShuffleHashJoin | Medium tables | Hash on one side |

---

## 7. Aggregations

```python
from pyspark.sql.functions import (
    count, countDistinct, sum, avg, mean,
    min, max, first, last,
    collect_list, collect_set,
    stddev, variance, approx_count_distinct
)

# Single aggregations
df.agg(
    count("*").alias("total"),
    countDistinct("category").alias("unique_cats"),
    sum("amount").alias("total_amount"),
    avg("amount").alias("avg_amount"),
    approx_count_distinct("user_id").alias("approx_users")
)

# GroupBy
df.groupBy("category").agg(
    count("*").alias("count"),
    sum("amount").alias("total"),
    avg("amount").alias("average")
)

# Multiple groupings
df.groupBy("region", "category").agg(sum("amount"))

# Collect values
df.groupBy("user_id").agg(
    collect_list("product_id").alias("products"),
    collect_set("category").alias("unique_categories")
)

# Pivot
df.groupBy("year").pivot("region").sum("amount")
df.groupBy("year").pivot("region", ["North", "South"]).sum("amount")  # Specified values
```

---

## 8. RDD Operations

```python
# Create RDD
rdd = sc.parallelize([1, 2, 3, 4, 5])
rdd = sc.textFile("file.txt")
rdd = df.rdd  # From DataFrame

# Transformations (lazy)
rdd.map(lambda x: x * 2)
rdd.filter(lambda x: x > 2)
rdd.flatMap(lambda x: x.split(" "))
rdd.distinct()

# Actions (trigger execution)
rdd.collect()  # Return all (AVOID on large data!)
rdd.take(10)   # First N
rdd.count()
rdd.first()
rdd.reduce(lambda a, b: a + b)

# Key-Value operations
pair_rdd = rdd.map(lambda x: (x[0], x[1]))
pair_rdd.reduceByKey(lambda a, b: a + b)  # Preferred!
pair_rdd.groupByKey()  # Avoid - shuffles all data
pair_rdd.mapValues(lambda v: v * 2)
pair_rdd.sortByKey()

# Convert back to DataFrame
df = rdd.toDF(["col1", "col2"])
```

**RDD vs DataFrame:**
| Aspect | RDD | DataFrame |
|--------|-----|-----------|
| Optimization | None | Catalyst optimizer |
| Type safety | Compile-time | Runtime |
| Serialization | Python pickle | Tungsten binary |
| Performance | Slower | Faster |
| Use when | Custom logic | Standard ETL |

---

## 9. Structured Streaming

### File Source
```python
# Read stream
stream_df = spark.readStream \
    .schema(schema) \
    .option("maxFilesPerTrigger", 1) \
    .parquet("input/path")

# Transformations (same as batch)
processed = stream_df.filter(col("value") > 0)

# Write stream
query = processed.writeStream \
    .outputMode("append") \
    .format("parquet") \
    .option("path", "output/path") \
    .option("checkpointLocation", "checkpoint/path") \
    .trigger(processingTime="10 seconds") \
    .start()

query.awaitTermination()
```

### Kafka Source/Sink
```python
# Read from Kafka
kafka_df = spark.readStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "host:9092") \
    .option("subscribe", "topic1,topic2") \
    .option("startingOffsets", "earliest") \
    .load()

# Parse JSON from value
from pyspark.sql.functions import from_json, to_json
parsed = kafka_df.select(
    from_json(col("value").cast("string"), schema).alias("data")
).select("data.*")

# Write to Kafka
query = df.select(
    col("key").cast("string"), 
    to_json(struct("*")).alias("value")
).writeStream \
    .format("kafka") \
    .option("kafka.bootstrap.servers", "host:9092") \
    .option("topic", "output_topic") \
    .option("checkpointLocation", "checkpoint") \
    .start()
```

### Windowing & Watermarks
```python
from pyspark.sql.functions import window

# Tumbling window
df.withWatermark("event_time", "10 minutes") \
    .groupBy(window("event_time", "5 minutes")) \
    .count()

# Sliding window  
df.groupBy(window("event_time", "10 minutes", "5 minutes")) \
    .agg(avg("value"))
```

### Output Modes
| Mode | Description | Use Case |
|------|-------------|----------|
| `append` | New rows only | No aggregations |
| `update` | Changed rows | Aggregations |
| `complete` | All rows | Small aggregations |

### Triggers
```python
.trigger(processingTime="10 seconds")  # Micro-batch every 10s
.trigger(once=True)                     # One batch then stop
.trigger(availableNow=True)             # Process all, then stop
.trigger(continuous="1 second")         # Low-latency (experimental)
```

---

## 10. Delta Lake

```python
# Write Delta table
df.write.format("delta").mode("overwrite").save("path")
df.write.format("delta").saveAsTable("db.table")

# Read
df = spark.read.format("delta").load("path")

# Time travel
df = spark.read.format("delta").option("versionAsOf", 5).load("path")
df = spark.read.format("delta").option("timestampAsOf", "2024-01-01").load("path")

# MERGE (upsert)
from delta.tables import DeltaTable

delta_table = DeltaTable.forPath(spark, "path")
delta_table.alias("target").merge(
    updates_df.alias("source"),
    "target.id = source.id"
).whenMatchedUpdate(set={
    "value": "source.value",
    "updated_at": "source.updated_at"
}).whenNotMatchedInsert(values={
    "id": "source.id",
    "value": "source.value",
    "created_at": "source.created_at"
}).execute()

# Optimize & Vacuum
delta_table.optimize().executeCompaction()
delta_table.optimize().executeZOrderBy("date", "customer_id")
delta_table.vacuum(168)  # Hours to retain
```

### Streaming + Delta
```python
# Read stream from Delta
stream_df = spark.readStream.format("delta").load("source_path")

# Write stream to Delta
stream_df.writeStream \
    .format("delta") \
    .outputMode("append") \
    .option("checkpointLocation", "checkpoint") \
    .start("target_path")

# foreachBatch for merge
def upsert_to_delta(batch_df, batch_id):
    delta_table.alias("t").merge(
        batch_df.alias("s"),
        "t.id = s.id"
    ).whenMatchedUpdateAll().whenNotMatchedInsertAll().execute()

stream_df.writeStream \
    .foreachBatch(upsert_to_delta) \
    .option("checkpointLocation", "checkpoint") \
    .start()
```

---

## 11. Performance Tuning

### Key Configurations
```python
# Parallelism
spark.conf.set("spark.sql.shuffle.partitions", 200)
spark.conf.set("spark.default.parallelism", 200)

# Memory
spark.conf.set("spark.executor.memory", "8g")
spark.conf.set("spark.driver.memory", "4g")
spark.conf.set("spark.memory.fraction", 0.6)  # Execution + storage

# AQE (Spark 3.0+)
spark.conf.set("spark.sql.adaptive.enabled", "true")
spark.conf.set("spark.sql.adaptive.coalescePartitions.enabled", "true")
spark.conf.set("spark.sql.adaptive.skewJoin.enabled", "true")

# Broadcast
spark.conf.set("spark.sql.autoBroadcastJoinThreshold", 10485760)  # 10MB

# Serialization
spark.conf.set("spark.serializer", "org.apache.spark.serializer.KryoSerializer")
```

### Caching
```python
from pyspark import StorageLevel

df.cache()  # MEMORY_AND_DISK
df.persist(StorageLevel.MEMORY_ONLY)
df.persist(StorageLevel.MEMORY_AND_DISK_SER)
df.unpersist()

# Force materialization
df.count()  # Trigger caching
```

### Partitioning
```python
# Check partitions
df.rdd.getNumPartitions()

# Repartition (shuffle)
df.repartition(100)
df.repartition("column")  # Hash partition by column

# Coalesce (no shuffle, only reduce)
df.coalesce(10)

# Optimal partition size: 128MB-256MB
num_partitions = data_size_bytes / (200 * 1024 * 1024)
```

### Skew Handling
```python
# 1. Salting for skewed keys
from pyspark.sql.functions import concat, lit, rand

salt_buckets = 10
df1_salted = df1.withColumn("salt", (rand() * salt_buckets).cast("int"))
df1_salted = df1_salted.withColumn("salted_key", concat(col("key"), lit("_"), col("salt")))

df2_exploded = df2.crossJoin(spark.range(0, salt_buckets).toDF("salt"))
df2_exploded = df2_exploded.withColumn("salted_key", concat(col("key"), lit("_"), col("salt")))

result = df1_salted.join(df2_exploded, "salted_key")

# 2. Broadcast skewed dimension
# 3. Enable AQE skew handling
```

### Anti-Patterns to Avoid
| Anti-Pattern | Problem | Solution |
|--------------|---------|----------|
| `collect()` on large data | OOM on driver | Use `take()`, `limit()`, write to file |
| `groupByKey()` | Full shuffle | Use `reduceByKey()` |
| Python UDFs | Serialization overhead | Use built-in functions, Pandas UDFs |
| Too many partitions | Task overhead | Coalesce, optimal sizing |
| Too few partitions | No parallelism | Repartition |
| Multiple scans | Recomputation | Cache reused DataFrames |

---

## 12. MLlib

### Feature Engineering
```python
from pyspark.ml.feature import (
    VectorAssembler, StringIndexer, OneHotEncoder,
    StandardScaler, MinMaxScaler, Normalizer
)
from pyspark.ml import Pipeline

# Assemble features
assembler = VectorAssembler(
    inputCols=["f1", "f2", "f3"],
    outputCol="features"
)

# Categorical encoding
indexer = StringIndexer(inputCol="category", outputCol="category_idx")
encoder = OneHotEncoder(inputCol="category_idx", outputCol="category_vec")

# Scaling
scaler = StandardScaler(inputCol="features", outputCol="scaled_features")

# Pipeline
pipeline = Pipeline(stages=[indexer, encoder, assembler, scaler])
model = pipeline.fit(train_df)
transformed = model.transform(train_df)
```

### Classification
```python
from pyspark.ml.classification import LogisticRegression, RandomForestClassifier
from pyspark.ml.evaluation import MulticlassClassificationEvaluator

# Train
lr = LogisticRegression(featuresCol="features", labelCol="label", maxIter=10)
model = lr.fit(train_df)

# Predict
predictions = model.transform(test_df)

# Evaluate
evaluator = MulticlassClassificationEvaluator(
    predictionCol="prediction", labelCol="label", metricName="accuracy"
)
accuracy = evaluator.evaluate(predictions)
```

### Hyperparameter Tuning
```python
from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

paramGrid = ParamGridBuilder() \
    .addGrid(lr.regParam, [0.01, 0.1, 1.0]) \
    .addGrid(lr.elasticNetParam, [0.0, 0.5, 1.0]) \
    .build()

cv = CrossValidator(
    estimator=lr,
    estimatorParamMaps=paramGrid,
    evaluator=evaluator,
    numFolds=3
)
cv_model = cv.fit(train_df)
best_model = cv_model.bestModel
```

### Save/Load Models
```python
model.save("path/to/model")
loaded_model = LogisticRegressionModel.load("path/to/model")
```

---

## 13. Configuration

### spark-submit
```bash
spark-submit \
  --master yarn \
  --deploy-mode cluster \
  --driver-memory 4g \
  --executor-memory 8g \
  --executor-cores 4 \
  --num-executors 10 \
  --conf spark.sql.shuffle.partitions=200 \
  --conf spark.dynamicAllocation.enabled=true \
  --conf spark.dynamicAllocation.minExecutors=5 \
  --conf spark.dynamicAllocation.maxExecutors=50 \
  --py-files dependencies.zip \
  main.py --date 2024-01-01
```

### Dynamic Allocation
```python
spark.conf.set("spark.dynamicAllocation.enabled", "true")
spark.conf.set("spark.dynamicAllocation.minExecutors", 5)
spark.conf.set("spark.dynamicAllocation.maxExecutors", 100)
spark.conf.set("spark.dynamicAllocation.executorIdleTimeout", "60s")
spark.conf.set("spark.shuffle.service.enabled", "true")  # Required!
```

### Executor Sizing
```
# General guidelines:
executor-cores = 4-5 (avoid >5 due to HDFS throughput)
executor-memory = (node_memory - overhead) / executors_per_node
memory-overhead = max(384MB, 0.1 * executor-memory)

# Example: 16 core, 64GB node
executors_per_node = 16 / 4 = 4
executor_memory = (64GB - 4GB_overhead) / 4 = 15GB
```

---

## 14. Testing

### pytest with Spark
```python
# conftest.py
import pytest
from pyspark.sql import SparkSession

@pytest.fixture(scope="session")
def spark():
    spark = SparkSession.builder \
        .master("local[2]") \
        .appName("tests") \
        .getOrCreate()
    yield spark
    spark.stop()

# test_transformations.py
def test_filter_nulls(spark):
    data = [("a", 1), ("b", None), ("c", 3)]
    df = spark.createDataFrame(data, ["name", "value"])
    
    result = df.filter(col("value").isNotNull())
    
    assert result.count() == 2

# Using chispa for DataFrame assertions
from chispa import assert_df_equality

def test_transformation(spark):
    input_df = spark.createDataFrame([("a", 1)], ["name", "value"])
    expected_df = spark.createDataFrame([("a", 2)], ["name", "doubled"])
    
    result = transform_function(input_df)
    
    assert_df_equality(result, expected_df, ignore_row_order=True)
```

---

## 15. Common Patterns

### ETL Template
```python
def run_etl(spark, input_path, output_path, date):
    # Extract
    df = spark.read.parquet(f"{input_path}/date={date}")
    
    # Transform
    cleaned = (df
        .filter(col("id").isNotNull())
        .dropDuplicates(["id"])
        .withColumn("processed_at", current_timestamp())
    )
    
    validated = cleaned.filter(col("amount") >= 0)
    
    # Load
    (validated.write
        .mode("overwrite")
        .partitionBy("region")
        .parquet(output_path))
    
    return validated.count()
```

### Incremental Load
```python
def incremental_load(spark, source, target, watermark_col):
    # Get current watermark
    try:
        current_max = spark.read.parquet(target) \
            .agg(max(watermark_col)).collect()[0][0]
    except:
        current_max = "1970-01-01"
    
    # Load only new data
    new_data = spark.read.parquet(source) \
        .filter(col(watermark_col) > current_max)
    
    # Append to target
    new_data.write.mode("append").parquet(target)
    
    return new_data.count()
```

### Data Quality Checks
```python
def run_dq_checks(df, table_name):
    results = {
        "table": table_name,
        "row_count": df.count(),
        "null_id": df.filter(col("id").isNull()).count(),
        "duplicates": df.count() - df.dropDuplicates(["id"]).count(),
        "negative_amounts": df.filter(col("amount") < 0).count()
    }
    
    # Fail on critical issues
    assert results["null_id"] == 0, f"Found {results['null_id']} null IDs"
    assert results["duplicates"] == 0, f"Found {results['duplicates']} duplicates"
    
    return results
```

---

## Quick Reference Cards

### Transformation Types
| Narrow (No Shuffle) | Wide (Shuffle) |
|---------------------|----------------|
| `map`, `filter` | `groupBy`, `reduceByKey` |
| `select`, `withColumn` | `join` |
| `coalesce` (reduce only) | `repartition` |
| `union` | `distinct`, `sort` |

### When to Use What
| Use Case | Choose |
|----------|--------|
| Standard ETL | DataFrame API |
| Complex custom logic | RDD |
| SQL familiarity | Spark SQL |
| Small lookup table | Broadcast |
| Large joins | Sort Merge Join |
| Time-based access | Partition by date |
| Key-based access | Bucket by key |

### Memory Troubleshooting
| Symptom | Cause | Fix |
|---------|-------|-----|
| OOM on executor | Task too large | Increase partitions, reduce executor memory |
| OOM on driver | Collect/broadcast | Avoid collect, limit broadcast size |
| Spill to disk | Not enough memory | Increase memory, reduce cache |
| Long GC pauses | Memory pressure | Use G1GC, reduce object creation |

---

*Last updated: December 2024 | Spark 3.5.x*
