[[_TOC_]]

# Introduction
------------
### Importance of Data Quality in Data Engineering Projects

1.  **Accuracy and Reliability**:
    * High-quality data ensures the results of data analysis or machine learning models are accurate and reliable. Poor data quality can lead to incorrect insights, bad decisions, and mistrust in the data pipeline.
2.  **Cost Efficiency**:
    *   Fixing data issues downstream is much more expensive than addressing them early in the pipeline. High-quality data minimizes the cost of error rectification.
3.  **Regulatory Compliance**:
    *   Many industries require data to meet specific standards for legal compliance. Ensuring data quality helps in meeting these standards.
4.  **Improved User Experience**:
    *   Clean, accurate data leads to better products and user experiences, especially in customer-facing applications.
5.  **Operational Efficiency**:
    *   High-quality data reduces the need for reprocessing, minimizes downtime, and ensures smooth operations in data pipelines.
6.  **Scalability**:
    *   Poor data quality can make scaling systems and processes difficult. Maintaining data quality ensures the data pipeline is robust enough to handle growth.

### About Great Expectations (GE)

Great Expectations is a powerful, open-source tool for validating, documenting, and profiling your data. It allows users to define expectations about data properties and automatically validate datasets against these expectations. GE integrates seamlessly with various data platforms such as Spark, Pandas, and SQL-based data warehouses, making it versatile for data quality tasks.
Key features of Great Expectations:
*   **Expectations**: Declarative, human-readable assertions about data properties.
    
*   **Validation**: Provides detailed feedback on whether data meets defined expectations.
    
*   **Data Context**: Manages configurations and enables modular workflows.

Great Expectations Tutorial Link : - [Learn | Great Expectations](https://docs.greatexpectations.io/docs/reference/learn/)

This document along with script example performs data quality checks on a dataset using the `great_expectations` (GE) library. The dataset is extracted from a Spark SQL table and validated against specific expectations.

### Why Use **Great Expectations (GE)** for Data Quality?

1.  **Open-Source and Community-Driven**:
    *   GE is an open-source tool with an active community, meaning it is constantly evolving with contributions from users worldwide.
2.  **Declarative and Configurable**:
    *   GE allows users to define data expectations declaratively. You can easily configure tests like schema validation, value ranges, uniqueness, null checks, etc., in human-readable formats.
3.  **Data Validation at Scale**:
    *   GE integrates well with modern data platforms and supports validating large datasets across various environments (data warehouses, cloud storage, databases).
4.  **Integration into Pipelines**:
    *   It integrates seamlessly with ETL/ELT workflows and orchestration tools like Apache Airflow, Prefect, or Dagster, ensuring quality checks are automated in the pipeline.
5.  **Detailed Reporting**:
    *   GE provides comprehensive validation reports, making it easier to identify and resolve data issues. Its Data Docs feature offers HTML reports for transparent auditing.
6.  **Flexible Implementation**:
    *   GE supports various data formats (CSV, Parquet, SQL databases, etc.) and allows custom validation checks via Python, catering to diverse use cases.
7.  **Ease of Adoption**:
    *   The tool is beginner-friendly with good documentation, making it accessible for teams with varying levels of expertise in data engineering.
8.  **Promotes Data Trust**:
    *   By integrating GE into your data engineering projects, stakeholders gain confidence in the quality of the data, as issues are detected and resolved proactively.


# Code Overview
-------------

### Libraries Used

1.  **great_expectations (gx)**: For defining and executing data quality expectations.
    
2.  **pyspark.sql.functions**: For working with Spark DataFrames.
    
3.  **json**: For JSON-related operations.
    

### Dataset

The script extracts the `fact_appc` dataset from the table `ODP_FINANCE_DEV_GOLD.APPC_Gold.dbo.fact_appc` in Spark SQL.

Steps in the Script
-------------------
### 1. Install Great Expectation

    %pip install great_expectations==1.2.4

### 2. Import required libraries.
```python
import great_expectations as gx
import json
from pyspark.sql.functions import current_timestamp, lit
from pyspark.sql.types import StructType, StructField, StringType, BooleanType, IntegerType, DoubleType, ArrayType, MapType, TimestampType
from datetime import datetime
```

### 3. Extracting Data

The dataset is retrieved using the Spark SQL query:

    spark.sql("SELECT * FROM ODP_FINANCE_DEV_GOLD.APPC_Gold.dbo.fact_appc")

### 4. Filtering Data

The dataset is filtered to include only rows where the `KEY` column has the value `ER`:

    df_fact_appc_ER = df_fact_appc.where((df_fact_appc.KEY == 'ER'))

### 5. Initializing Great Expectations

A GE context is created, and a Spark data source is added:

    context = gx.get_context()
    data_source = context.data_sources.add_spark("generic_data_source")
    data_asset = data_source.add_dataframe_asset(name="generic data asset")
    batch_definition = data_asset.add_batch_definition_whole_dataframe("batch definition")

A batch for the filtered dataset (`df_fact_appc_ER`) is defined:

    batch_ER = batch_definition.get_batch(batch_parameters={"dataframe": df_fact_appc_ER})

### 6. Defining Expectations

Four expectations are defined for the `KPI_VALUE` and `IRIS_ACCOUNT` columns:

#### a. Not Null Check

Ensures the `KPI_VALUE` column does not contain null values:

    exp_kpi_value_not_null= gx.expectations.ExpectColumnValuesToNotBeNull(column="KPI_VALUE")

#### b. Greater Than or Equal to Zero Check

Ensures all values in the `KPI_VALUE` column are ≥ 0:

    exp_kpi_value_gt_0= gx.expectations.ExpectColumnValuesToBeBetween(column="KPI_VALUE", min_value=0)

#### c. Data Type Check

Ensures all values in the `KPI_VALUE` column are of type `FloatType` or `DoubleType`:

    exp_kpi_value_datatype= gx.expectations.ExpectColumnValuesToBeInTypeList(column="KPI_VALUE", type_list=["FloatType", "DoubleType"])

#### d. Not Blank Check

Ensures the `IRIS_ACCOUNT` column does not contain blank values:

    exp_iris_account_not_blank= gx.expectations.ExpectColumnValuesToMatchRegex(column="IRIS_ACCOUNT", regex=r"\S")

### 7. Validating Expectations

The defined expectations are validated against the batch:
```python
# For "KPI_VALUE" NotNull
ge_output_kpi_value_not_null = batch_ER.validate(exp_kpi_value_not_null)

# For "KPI_VALUE" >=0
ge_output_kpi_value_gt_0 = batch_ER.validate(exp_kpi_value_gt_0)

# For "KPI_VALUE" Data Type as double
ge_output_kpi_value_datatype = batch_ER.validate(exp_kpi_value_datatype)

# For "IRIS_ACCOUNT" not blank ('')
ge_output_exp_iris_account_not_blank = batch_ER.validate(exp_iris_account_not_blank)
```
* * *

Outputs
-------

Each validation output (`ge_output_kpi_value_not_null`, `ge_output_kpi_value_gt_0 `, `ge_output_kpi_value_datatype`, `ge_output_exp_iris_account_not_blank`) contains details on whether the respective expectation was met and provides diagnostics if it was not met.

* * *

### Save validation output to table
Convert the validation output json to dataframe and save the same to table.

```python
   # List of validations to process

validations = [

    ("KPI_VALUE_NotNull", ge_output_kpi_value_not_null),

    ("KPI_VALUE_GT_0", ge_output_kpi_value_gt_0),

    ("KPI_VALUE_DataType", ge_output_kpi_value_datatype),

    ("IRIS_ACCOUNT_NotBlank", ge_output_exp_iris_account_not_blank),

] 

# Define schema for DataFrame

schema = StructType([

    StructField("success", StringType(), True),

    StructField("type", StringType(), True),

    StructField("column", StringType(), True),

    StructField("total_record_count", StringType(), True),

    StructField("total_unexpected_record_count", StringType(), True),

    StructField("total_unexpected_record_percent", StringType(), True),

    StructField("partial_unexpected_list", StringType(), True),

    StructField("partial_unexpected_counts", StringType(), True),

    StructField("raised_exception", StringType(), True),

    StructField("exception_traceback", StringType(), True),

    StructField("exception_message", StringType(), True),

    StructField("Data_Validation_DateTime", TimestampType(), True),

    StructField("TableName", StringType(), True),

])

# Helper function to serialize a single value

def serialize_value(value):

    if isinstance(value, list):

        return "|".join(map(str, value))

    return str(value) if value is not None else ""

# Iterate over validations and process each

for validation_name, validation_output in validations:

    # Serialize and parse validation result

    validation_result_json = json.dumps(validation_output.to_json_dict())

    parsed_json = json.loads(validation_result_json)


    # Flatten and serialize the JSON structure

    flattened_data = {

        "success": serialize_value(parsed_json.get("success", None)),

        "type": serialize_value(parsed_json.get("expectation_config", {}).get("type", None)),

        "column": serialize_value(parsed_json.get("expectation_config", {}).get("kwargs", {}).get("column", None)),

        "total_record_count": serialize_value(parsed_json.get("result", {}).get("element_count", None)),

        "total_unexpected_record_count": serialize_value(parsed_json.get("result", {}).get("unexpected_count", None)),

        "total_unexpected_record_percent": serialize_value(parsed_json.get("result", {}).get("unexpected_percent", None)),

        "partial_unexpected_list": serialize_value(parsed_json.get("result", {}).get("partial_unexpected_list", None)),

        "partial_unexpected_counts": serialize_value(parsed_json.get("result", {}).get("partial_unexpected_counts", None)),

        "raised_exception": serialize_value(parsed_json.get("exception_info", {}).get("raised_exception", None)),

        "exception_traceback": serialize_value(parsed_json.get("exception_info", {}).get("exception_traceback", None)),

        "exception_message": serialize_value(parsed_json.get("exception_info", {}).get("exception_message", None)),

        "Data_Validation_DateTime": None,  # Placeholder for timestamp

        "TableName": "ODP_FINANCE_DEV_GOLD.APPC_Gold.dbo.fact_appc",

    }

    # Add current timestamp dynamically

    flattened_data["Data_Validation_DateTime"] = datetime.now()

    # Convert to DataFrame

    df = spark.createDataFrame([list(flattened_data.values())], schema=schema)

    # Save DataFrame to Table

    df.write.mode("append").saveAsTable("ODP_FINANCE_DEV_GOLD.APPC_Gold.dbo.DQ")
```
Conclusion
----------

This document ensures step by step guide for data quality by validating the `fact_appc` dataset against specific expectations. 