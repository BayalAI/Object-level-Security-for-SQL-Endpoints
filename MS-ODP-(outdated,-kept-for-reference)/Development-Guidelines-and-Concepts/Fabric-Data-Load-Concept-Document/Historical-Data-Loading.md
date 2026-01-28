# **Introduction:**
Historical data loading refers to strategies that enable data platforms to ingest both new and past data while maintaining flexibility in how data is processed and stored. 

In Microsoft Fabric, this involves managing data between layers (Data Lakes) and structured layers (such as Data Warehouses or Lakehouses). 

# **Key Features:**

**Full Loading:** Reloads the entire dataset from scratch as needed.

# When to Use:
- When setting up a new environment: You need to populate the system with all historical data before transitioning to incremental loads.

- Moving data from an old system to a new system (e.g., on-premises to cloud) typically involves a full historical load.

- When the entire dataset needs to be reloaded due to schema changes, business logic adjustments, or large-scale data corrections.

- If there are concerns about data consistency, quality issues, or historical errors in the dataset, you may need to run a full load to ensure the target system is synchronized and accurate.

- If you’re conducting performance optimizations, such as re-indexing tables or re-organizing partitions, you may need to perform a full load to ensure data is restructured optimally.

Microsoft Fabric, with its advanced features such as Delta Lake time travel, Fabric Notebooks, and Pipelines, provides an ideal environment to implement these patterns in a scalable, efficient manner.

**Reference Implementation Link: -**
<A  href="https://app.powerbi.com/groups/43bcdcb8-d446-4105-a4e5-3764426631b7/synapsenotebooks/c859720f-13f6-4128-b760-0b4d5205fc11?experience=power-bi">Historical Load - Power BI</A>





