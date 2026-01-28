[[_TOC_]]

# Introduction
The Gold layer reference implementation is a modification/extension of the silver layer reference implementation and can be found in the ODP_FINANCE_DEV_GOLD workspace:
[Finance_Gold](https://app.fabric.microsoft.com/groups/c07b4ca8-d81d-40ec-9c51-c139a1767996/list?experience=power-bi&subfolderId=10846) 

# Finance_Main pipeline
This pipeline will only execute two sub pipelines:
- Dimension Processing
- Fact Processing

# Finance_Dimension_Gold_Process
This pipeline will invoke all dimension processing pipelines

# Finance_FactGold_process
This pipeline will invoke all fact processing pipelines

#Finance_dimXYZ_Gold or Finance_factXYZ_Gold pipelines
All Pipelines are similar, they execute a load/transform/optimization notebook: 
![image.png](/.attachments/image-3396155b-4d3d-4db4-bfcb-677026a685c9.png)

The load and otimization notebook is similar to the silver implementation, therefore this documentation is focused on the transform notebook.

# Finance_dimXYZ_Gold_Transform notebook
This notebook transform data into the final dimension structure

##data dictionary section
In this section the target and source column name are defined, as well as the business key and the surrogate key column name.
```
# Data from the excel mapping created via gpt into dictionary form
#index, target column name, source column name

data_dictionary = [
    (1,"ACCOUNT","ACCOUNT"),
    (2,"ACCOUNT_TEXT","ACCOUNT__TEXT"),
    (3,"ACCOUNT_LTEXT","ACCOUNT__LTEXT"),
...
    (35,"ACC_L04_TEXT","ACC_L04__TEXT"),
    (36,"ACC_L05_ID","ACC_L05_ID"),
    (37,"ACC_L05_TEXT","ACC_L05__TEXT")
]

business_keys = ["ACCOUNT"]
surrogate_key = "ACCOUNT_SK"
modified_column = None
```

##merge section
In this section a merge function will be executed, which also adds a surrogate key to the table.

```
#Performe Surrogate Key Merge
merge_into_or_create_sk(df=source_table_1, business_keys = business_keys, surrogate_key=surrogate_key, path = table_path)
```

# Finance_factXYZ_Gold_Transform notebook
This notebook transform data into the final fact table structure.
It's possible to add surrogate keys to the final table 

##data dictionary section
In this section the index, target_column_name, source_column_name, lookup_table, lookup_column and lookup_return_column are defined, as well as the business key.


```
# Data from the excel mapping created via gpt into dictornary form
#index, target_column_name, source_column_name,lookup_table, lookup_column, lookup_return_column

data_dictionary = [
    (1,"WBS_ELEMENT_SK","WBS_OBJNR","dbo.dim_wbs_element","WBS_ELEMENT_OBJNR","WBS_ELEMENT_SK"),
    (2,"WBS_OBJNR","WBS_OBJNR","","",""),
    (3,"MIGRATED","MIGRATED","","",""),
...
    (33,"DEB_CRED","DEB_CRED","","",""),
    (34,"TBL_PARTITION_NUM","TBL_PARTITION_NUM","","","")
]
```
- index - not used
- target_column_name = name of column in final target table
- source_column_Name = name of column in source temp table
- lookup_table = table where the dimension surrogate key can be found
- lookup_column = column used for lookup
- lookup_return_table = column from which the result of the lookup will be used

# Utilities notebook
All commonly used functions and imports can be found in this notebook.

