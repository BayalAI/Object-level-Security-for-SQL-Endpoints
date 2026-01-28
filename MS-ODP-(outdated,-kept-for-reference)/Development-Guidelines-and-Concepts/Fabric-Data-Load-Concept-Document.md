This document provides a detailed overview of data loading strategies in Fabric environments, focusing on the best practices & patterns used for loading and maintaining data efficiently. It will cover history (Full) loading and incremental loading.

Data loading into Fabric encompasses the process of importing data from multiple sources (e.g., databases, APIs, files) into Fabric storage layers such as Lakehouse and Delta Lake. The goal is to ensure the data is ingested efficiently, reliably, and in a way that supports analytical processing.

**Types of Data Loading:**
- _History (Full) Load:_ Entire datasets are loaded at once, typically on a scheduled basis.
- _Incremental Load:_ Only new or changed data is loaded, reducing resource consumption.
- _On-Demand Reprocessing:_ When errors, new requirements, or specific use cases arise, specific portions of previously processed data are reloaded on demand. (**Out of scope in this document**)

<u>***When to Use:***</u>

**History (Full) Load: -**

- When setting up a new environment: You need to populate the system with all historical data before transitioning to incremental loads.

- Moving data from an old system to a new system (e.g., on-premises to cloud) typically involves a full historical load.

- When the entire dataset needs to be reloaded due to schema changes, business logic adjustments, or large-scale data corrections.

Details: - [History/Full Load](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Fabric-Data-Load-Concept-Document/Historical-Data-Loading)


**Incremental Load: -**

- When you are dealing with large datasets, incremental loading is crucial to avoid reprocessing the entire data each time. Instead of loading the entire dataset, you can load only the records that have been added or updated since the last load.

- If the data in your source systems is frequently updated, it’s more efficient to incrementally load just the new or changed data rather than performing a full refresh.

- When managing Slowly Changing Dimensions (SCD Type 2) in a data warehouse, incremental load helps capture the changes to the dimension tables without having to reload the entire table.

- In situations where the system is sensitive to load times or where resource constraints make full data loads impractical, incremental loading helps reduce the amount of data processed, leading to faster loads and less strain on resources.

Details: - [Incremental Load](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Fabric-Data-Load-Concept-Document/Incremental-Data-Loading)

________________________________________________________________________
<mark>
________________________________________________________________________

# Data Loading Strategy

| Strategy Name | Data Requirements | Description/When to Use | Link to Implementation
|:---|:---|:----|:----|
| Full Load|	Complete dataset|	When initial data load is required or during a migration. Best for smaller datasets.|
|Watermark|	Incremental data with timestamp|	When you need to process new records added after the last load without tracking all changes.|
|SQL EXCEPT|	Two datasets for comparison|	When you want to find records present in one dataset but not in another. Best for small to medium dataset.|
|Spark EXCEPT|	Two DataFrames for comparison|	When working with Spark DataFrames to identify differences between two datasets in a distributed manner. Best for large dataset.|
|Change Data Feed (CDF)|	Captured changes to the data|	During incremental load, if rollback is required to a particular version to process correct data.|
|Delta Merge|	Delta table with new and existing records|	When you need to merge updates into an existing dataset efficiently, especially in Delta Lake.|
|SCD Type 2|	Historical and current data|	When you want to maintain a full history of changes for each record, creating new rows for updates.|










# Watermark



