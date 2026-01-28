[[_TOC_]]

# Introduction
The Use Case Gold layer reference implementation is a modification/extension of the silver layer reference implementation and can be found in the ODP_FINANCE_DEV_GOLD workspace:

[APPC_Gold](https://app.fabric.microsoft.com/groups/c07b4ca8-d81d-40ec-9c51-c139a1767996/list?experience=power-bi&subfolderId=9643)

# APPC_Main pipeline
This pipeline will only execute the sub pipelines for each fact table:
- APPC_PM_Gold

#APPC_PM_Gold pipeline
All Pipelines are similar, they execute a load/transform/optimization notebook: 
![image.png](/.attachments/image-3396155b-4d3d-4db4-bfcb-677026a685c9.png)

The load and otimization notebook is similar to the silver implementation, therefore this documentation is focused on the transform notebook.

# APPC_PM_Gold_Transform notebook
This notebook transform data into the final dimension structure

##data dictionary section
This section index, target_column_name, source_column_name, aggregation, visible settings are defined:

```
data_dictionary = [
    (1,"ACCOUNT_SK","PM_ACCOUNT_SK","groupBy",False),
    (2,"ACCOUNT","PM_ACCOUNT","groupBy",False),
    (3,"IRIS_L06","A_IRIS_L06","groupBy",False),
...
    (9,"PROFIT_CTR_SK","PM_PROFIT_CTR_SK","groupBy",True),
    (10,"PROFIT_CTR","PM_PROFIT_CTR","groupBy",True),
...
    (28,"KPI_VALUE","PM_AMOUNT_EUR_MTH","sum",True),
    (29,"KEY","","",True)
]
```
- index = not used
- target_column_name = column name in the final target table
- source_column_name = column name of the source column, empty if no source column available
- aggregation = aggregation, either "groupBy" or "sum" or empty to identify aggregation columns
- visible = True or False, needed 


```
#source table name to identify rows of this table in target
source = 'PM_ACTUAL'

#join columns for calcualtions
join_columns = ['PROFIT_CTR', 'WBS_OBJ_NR', 'PROJ_OBJ_NR', 'FISC_PER', 'CUSTOMER'] # all groupBy_columns_final collumns will be used for joins if this list is empty
#join_columns = [] # all groupBy_columns_final collumns will be used for joins if this list is empty

#column names
kpi_value_column = 'KPI_VALUE'
key_column = 'KEY'
source_column = 'SOURCE'

business_keys = []
modified_column = None
```
- source = A name for the source as string. This is added in a column to identify the rows from this load
- join_columns = optional, to improve load performance
- column names define the names used for the final dataset

## GroupBy and Aggregate section
A first grouping and aggregation on all groupBy columns to reduce amount of data.
The dataframe is cached for further usage

```
# groupBy and aggregate
source_table_1 = source_table_1.groupBy(*groupBy_columns).agg(*aggregations) \
    .cache()
```


## Basic Calculations
All basic calculations follow the same pattern

```
COD = source_table_1.filter(col('IRIS_L06') == 'I-TOTCST') \      # filter to identify value
        .groupBy(*groupBy_columns_final).agg(*aggregations) \     # groupBy final (dimension) attribute columns 
        .withColumn(key_column, lit('COD')) \                     # add KEY 'COD' as string
        .select(*columns_final)                                   # select columns needed in final table
```


## Get all Unique Keys
distinct_keys = all combinations of (dimension) attributes
columns_to_select_from_joined_table = all needed columns for joining

```
# distinct groupBy columns
distinct_keys = target_table_1.select(groupBy_columns_final).dropDuplicates()

# set columns to select from joined table
columns_to_select_from_joined_table = join_columns + [kpi_value_column]
```


##Extended Calculations
Each calculation is similar from the structure

```
# COSTS = ER - PM
# = COD + COGS
COSTS = distinct_keys \                                          # join all combinations of (dimension) attributes
    .join(                                                    
        COD                                                      # with the first basic calculation (COD)
        .select(*columns_to_select_from_joined_table),           # select only columns needed for join and value
        join_columns,                                            # on join columns 
        'left'                                                   # left join   
    ) \
    .fillna({kpi_value_column: 0}) \                             # replace null values with 0
    .withColumnRenamed(kpi_value_column, 'COD') \                # rename the value column to COD
    .join(                                                       # join with
        COGS                                                     # the second basic calculation (COGS)
        .select(*columns_to_select_from_joined_table),           # select only columns needed for join and value
        join_columns,                                            # on join columns 
        'left'                                                   # left join   
    ) \
    .fillna({kpi_value_column: 0}) \                             # replace null values with 0
    .withColumnRenamed(kpi_value_column, 'COGS') \               # rename the value column to COGS
    .withColumn(kpi_value_column, col('COD') + col('COGS')) \    # calculate COD+COGS and store in KPI_VALUE
    .withColumn(key_column, lit('Costs (ER - PM)')) \            # add KEY 'Costs (ER -PM)' as string
    .select(*columns_final)                                      # select columns needed in final table
```


##Merge Section
The merge function can be executed with extended options.
To avoid overwriting data from other sources you can either use partitioning by a source table information which is stored in a column and the option partionOverwriteMode: dynamic or by a replaceWhere option 

```
# Performe Merge
#overwrite only rows from the source table used in this notebook
# overwrite with where clause
#merge_into_or_create(df=target_table_1, primary_key_columns = business_keys, path = table_path, opts = {"replaceWhere": f"{source_column} == '{source}'"})
# overwrite by partition
merge_into_or_create(df=target_table_1, primary_key_columns = business_keys, path = table_path, partitionby = [source_column], opts = {"partitionOverwriteMode": "dynamic"})
```

