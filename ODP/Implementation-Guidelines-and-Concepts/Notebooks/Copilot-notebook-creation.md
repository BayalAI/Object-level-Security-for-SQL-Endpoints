## how Copilot to create and enhance pypsark notebooks within fabric UI
Please find recording of the demo here: [recordings](https://atos365.sharepoint.com/:f:/r/sites/100002399/Shared%20Documents/Octopus/03%20Technical%20Architecture/recordings?csf=1&web=1&e=Hw0Sao)
The video about VS code and copilot is stored in the same folder
**pre-requirements**
- You must be a member of GIT-ODP-DEVELOPER. Only for this Azure AD group Copilot is enabled
- You connect connect the notebook with your lakehouse.
- You must run an active session

You could start now the copilot.

![image.png](/.attachments/image-b1263dae-a306-4c3d-a710-d074bf121637.png =1000x)

few remarks and observations:
- Copilot "knows" your lakehouse table
- Copilot "knows" the current content of your notebook/cell
- You could start from scratch to create a notebook
- you could enhance an existing notbook in case you need a specific function
- same prompt not always result in identical code!!
- Copilot was not "understood" whot I want to get!! pls see below examples



**Single prompts:**
`remove leading zero from Account column`
`concat current_month with position 1,4 with "0" with current_month with position 5,2`
`rename columns based an table 
Account SF_Account
period SF_period
customer SF_customer`




**full executable notebook**
Either you could enter prompt by prompt or you could copy and past prepare multiple line of prompts.
Sample of prompts to create a full executable notebook
`Load dim_account with spark read table into a DataFrame
filter on HIER_L07 on value I-TOTREV`
`Load fact_figl_om with spark read table into a DataFrame`
`inner join fact_figl_om_df with dim_account_df using column ACCOUNT`
`drop all columns except HIER_L07, FISC_PERIOD, AMOUNT_DOC, COMPANY`
`rename AMOUNT_DOC to AMOUNT`
`create variable current_month with current date in format YYYYMM`
`concat current_month with position 1,4 with "0" with current_month with position 5,2`
`Create variable last_6_month with current date - 6 month in format YYYYMM`
`concat last_6_month with position 1,4 with "0" with last_6_month with position 5,2`
`filter FISCPER between current_month and last_6_month`
`group by HIER_L07, FISCPER, COMPANY sum AMOUNT`
`pivot on FISCPER`
`save pivoted_df into lakehouse table my_pivoted_table`

**strange samples**
      
**Prompt**:
load table [GOLD_FIN_MD].[dbo].[dim_exchrate] into data frame with spark SQL

**Result**:
spark_df = spark.read.table("dim_exchrate")  
 
max_rows_to_read = 1000  
spark_df = spark_df.limit(max_rows_to_read)

      
**P:**
load result of SQL into data frame
SELECT min ([REPORT_MTH]) as REPORT_MTH, [CURR_FROM], [CURR_TO], [CONV_TYPE]
FROM [GOLD_FIN_MD].[dbo].[dim_exchrate] group by [CURR_FROM], [CURR_TO], [CONV_TYPE]

**R:**
spark_df = spark.read.table("dim_exchrate")  
result_df = spark_df.groupBy("CURR_FROM", "CURR_TO", "CONV_TYPE").agg(min("REPORT_MTH").alias("REPORT_MTH"))  
  
max_rows_to_read = 1000  
result_df = result_df.limit(max_rows_to_read)  
pandas_df = result_df.toPandas()

      
P:
load table with spark SQL statement into data frame SELECT min ([REPORT_MTH]) as REPORT_MTH, [CURR_FROM], [CURR_TO], [CONV_TYPE] FROM [GOLD_FIN_MD].[dbo].[dim_exchrate] group by [CURR_FROM], [CURR_TO], [CONV_TYPE]

R:

'# Perform the SQL query to select data from [GOLD_FIN_MD].[dbo].[dim_exchrate] and load it into a Spark DataFrame  
sql_query = """  
SELECT  
    min(REPORT_MTH) as REPORT_MTH,  
    CURR_FROM,  
    CURR_TO,  
    CONV_TYPE  
FROM   
    dim_exchrate  
GROUP BY   
    CURR_FROM,  
    CURR_TO,  
    CONV_TYPE  
"""  
spark_df = spark.sql(sql_query)  
  
'# To ensure only a reasonable amount of data is being processed at once, limit the rows  
max_rows_to_read = 1000  
spark_df = spark_df.limit(max_rows_to_read)  
  
'# Convert to pandas DataFrame if needed (assuming conversion is required in the user's context)  
pandas_df = spark_df.toPandas()  
  
'# Display the DataFrame (if you want to visualize the data)  
spark_df.show()





