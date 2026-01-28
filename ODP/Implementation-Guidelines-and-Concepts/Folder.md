
**Folder in INGEST WORKSPSACE**
As reminder: In the ingest workspace data is loaded from source to Bronze, Bronze to Silver and Silver to Gold.
Bronze and Silver lakehouse will be part of ingest workspace.
Gold lakehouse will be located in domain/sub-domain workspace but loaded with notebooks located in the ingest workspace. 
  

***BRONZE***
BRONZE/PIPELINES
BRONZE/PIPELINES//DOMAIN

BRONZE/NOTEBOOKS
BRONZE/NOTEBOOKS/MAST
BRONZE/NOTEBOOKS/MAST/[DOMAIN]
BRONZE/NOTEBOOKS/TRANS/
BRONZE/NOTEBOOKS/TRANS/[DOMAIN]

' TRANS  = folder to process transctional data 
' MAST   = folder to process master data 
' DOMAIN = ' FIN, CUST, EMP, ....

Optional folder:
BRONZE/PARAM
BRONZE/DDL
BRONZE/API_TRIGGER

***SILVER***
SILVER/PIPELINES
SILVER/PIPELINES//DOMAIN

SILVER/NOTEBOOKS
SILVER/NOTEBOOKS/MAST
SILVER/NOTEBOOKS/MAST/[DOMAIN]
SILVER/NOTEBOOKS/TRANS/
SILVER/NOTEBOOKS/TRANS/[DOMAIN]

' TRANS  = folder to process transctional data 
' MAST   = folder to process master data 
' DOMAIN = ' FIN, CUST, EMP, ....

Optional Folder
SILVER/PARAM
SILVER/DDL
SILVER/API_TRIGGER

***GOLD***

GOLD/PIPELINES
GOLD/PIPELINES//DOMAIN

GOLD/NOTEBOOKS
GOLD/NOTEBOOKS/DIMENSIONS
GOLD/NOTEBOOKS/DIMENSIONS/DOMAIN
GOLD/NOTEBOOKS/FACTS/
GOLD/NOTEBOOKS/FACTS/DOMAIN

' DOMAIN = ' FIN, CUST, EMP, ....


**Folder in Domain / Sub-Domain WORKSPSACE**
In Domain / Sub-Domain workpsace only the lakehouse, semantic model and reports schould exists.
Depending to the number of semantic model and reports folder could be created 


