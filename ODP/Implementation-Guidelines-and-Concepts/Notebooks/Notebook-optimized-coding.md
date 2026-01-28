Spark Optimization Best Practices
=================================

1. Leverage Spark Caching Wisely
--------------------------------

Use `cache()` or `persist()` only when a DataFrame is reused multiple times, and `unpersist()` it when no longer needed.

df.cache()
# Do operations
df.unpersist()


2. Push Down Filters Early
--------------------------

Apply `filter()`, `select()`, or `drop()` early in the pipeline to reduce data volume early on.
**GOOD:**

df_filtered = df.filter(df["status"] == "active").select("id", "name")

**BAD:**

df_selected = df.select("id", "name")
df_filtered = df_selected.filter(df_selected["status"] == "active")

3. Broadcast Small Lookup Tables
--------------------------------

For small dimension tables used in joins, use **broadcast joins** to avoid shuffling.

from pyspark.sql.functions import broadcast

df_joined = df_large.join(broadcast(df_small), on="id", how="left")

  
4. Use Partitioning Wisely
Repartition DataFrames by key columns to avoid skew and improve parallelism, or coalesce if writing smaller files.

df.repartition("Country", "Division")  # Better parallelism
df.coalesce(1)  # Use with caution when writing to a single file

5. Avoid Collect and toPandas
Don't use collect() or toPandas() on large datasets—they bring data to driver memory and can crash the session.

6. Optimize Data Formats
Prefer Delta Lake or Parquet over CSVs for performance and schema enforcement

7. Use SQL for Heavy Aggregations
SQL queries are often more optimized in Spark under the hood, especially for joins and group by operations.

df.createOrReplaceTempView("sales")
spark.sql("""
SELECT Country, SUM(amount) as total
FROM sales
GROUP BY Country
""")

8. Enable Adaptive Query Execution (AQE)
If not already, make sure AQE is enabled—Azure Fabric usually has this on by default.
spark.conf.set("spark.sql.adaptive.enabled", "true")

Use Spark UI in Azure Fabric to:
*   Monitor stages
*   Spot skewed joins
*   Track shuffle sizes
*   Optimize stage durations

