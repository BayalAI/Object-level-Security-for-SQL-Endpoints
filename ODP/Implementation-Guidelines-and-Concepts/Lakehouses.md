## Lakehouses
### Definition ###
A **lakehouse** is a unified data platform that combines the capabilities of a data lake and a data warehouse. It allows you to store, manage, and analyze both structured and unstructured data in a single location. A lakehouse is focused on data storage and analytics, while a workspace is a broader organizational structure that contains and manages various data-related items, including lakehouses.

***At creation use `Lakehouse schemas` is mondatory***

### Format **For Bronze and Silver layer** 
`<layer>_<DataSource>_<INGEST>`

### Example
`BRONZE_SAP_INGEST`
`SILVER_SAP_INGEST`

### Format **For Gold layer** 
`Gold_<DataDomain>_<DataSubDomain>`
### Example
`GOLD_FIN_TRY`
`GOLD_EMP_PA`
`GOLD_CUST_SLS`

### Guidelines **For Gold layer** 
- **Layer**: GOLD for the Gold.
- **DataDomain**: One of the 7 Data Domain name. FIN, EMP, CUST, 
- **DataSub-Domain**: one of the Data sub-Domain Name FIN-**TRY**, FIN-**GL**, CUST-**SLS**, EMP-**PA**

