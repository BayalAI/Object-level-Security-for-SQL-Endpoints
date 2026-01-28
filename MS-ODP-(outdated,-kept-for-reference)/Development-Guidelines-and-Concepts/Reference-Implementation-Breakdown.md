[[_TOC_]]

# Introduction & Motivation
Here in this wiki page, we will see how to work with the reference implementations provided by Microsoft to ingest raw files in excel to a Lakehouse in Fabric. For this example, we will take the 'ODP_BUP_DEV_INGEST' as a reference.
The Fabric workspace is organized to streamline data ingestion and transformation processes.

# General workspace structure
![image.png](/.attachments/image-eeada20f-250a-45f1-a351-aeb0732a1bd1.png)
The Medallion Architecture, also called the Delta Architecture, organizes data into three layers: Bronze, Silver, and Gold. Each layer has a specific role in ensuring the quality and accessibility of data.

We are following this architecture in our workflow too. 
We first have the bronze layer where we dump our data as it is. It serves as the landing zone for raw data.
Next we have the Silver layer, in here we need to first load the data from bronze to silver in forms of temporary views or tables and then make transformations on them. After necessary transformations are done, we can save them in the silver layer. This becomes an optimized and cleaner version of the data needed. 


#Fabric Workspace
![image.png](/.attachments/image-f0b16323-50ad-459e-8599-e361439b1197.png)

1. Folders: 
   - BUP_Bronze and BUP_Silver: Holds file for loading into bronze and silver layers after necessary transformations.
1. "Main" Pipeline: 
   - The Main pipeline is configured in a way that when run, can be used to invoke all the necessary pipelines that are inside this workspace. For example, here in this workspace we have two ingestion pipelines for 2 files here. When the main pipeline is run the two ingestion pipelines are invoked for the two different files. 
1. "Utilities" notebook: 
   - The *Utilities notebook* in the workspace is designed to be imported into various other notebooks within the workspace. Its primary purpose is to provide *common load functions* that are used during the ingestion of files and data. This helps streamline the ingestion process by centralizing frequently used functions, making them easily accessible and reusable across different notebooks and pipelines.

## Purpose of Bronze folder
The Bronze folder will hold the Bronze Lakehouse where your raw data is loaded. Any other work on the Bronze layer will also be documented here in the Bronze folder.
_The Bronze layer acts as a staging area where raw data from various sources is ingested and stored in its original format. This ensures that the original data is preserved and can be reprocessed if needed. It also provides a single source of truth for raw data._

To load files into Bronze layer
1. Create a Lakehouse by navigating into the Bronze layer folder, selecting the "+ New Item" icon and choosing Lakehouse in it. Name it accordingly. Let's name it Bronze Lakehouse for now

1. To directly upload to the Bronze Lakehouse simply navigate into the Lakehouse, Go to the get data option and choose upload files. Then upload the files after from your local or wherever you have stored them.
![image.png](/.attachments/image-597c6265-60fd-4a1f-86e9-795211972ac0.png)



## Purpose of Silver folder
The Silver folder holds the notebooks where data from Bronze layer is cleaned, optimized and corrected before being loaded into the silver layer. It also holds the Silver Lakehouse where data is finally loaded after being optimized.


# Workflow description
## Data Ingestion
![image.png](/.attachments/image-dbebc631-a808-4c78-905a-9e92cd083396.png)

Go ahead and create a Lakehouse and call it the Silver Layer. This will be the location where you write your files to.
Here you can see multiple notebooks and pipelines. Let's take a look at the ingestion pipeline first
![image.png](/.attachments/image-92ae5a3a-23a9-487f-82c1-03843f4e192a.png)


This is how the file ingestion process will go on. As you can see first session tag is set and then data is loaded, transformed, optimized and quality assurance. 
## Data Transformation
The first thing to do before any transformations to be applied is to set a session tag. 
_The Set SessionTag activity is used to set a session tag for all notebooks. In the notebooks configured here we are using temporary views and tables to perform transformations on the data and then load it into the silver layer. Temporary tables or views are available in one session only and will not exist in new ones. But since the same temp view is needed in the pipeline to perform activities accordingly we assign a session tag that remains same all throughout the life of the pipeline. So as long as the pipeline is running all the notebooks configured with it will be running under the same session. This means temp views created will be available in all the notebooks._
For all ingestion pipelines, the session tag set function remains the same. Now click the first activity after set session tag activity

![image.png](/.attachments/image-1c670c18-f899-495c-908d-21b059f5bcfb.png)

Below go to the settings tab like in the image above. For workspace- select on the workspace you want the pipeline to be configured in and for notebook select the appropriate notebook. Similarly, you can do for all other notebooks too.

### Load Data
As the names suggest, Load Data notebook helps load data from bronze layer to a global temporary View. Temporary views isolate the transformation logic from the original data, ensuring that any changes or errors during the transformation process do not affect the source data. Temporary views can also be reused within the same session, allowing multiple transformations to be applied sequentially without reloading the data each time.
### Transform Data
In the Transform Data notebook, the necessary transformations are made on the Temporary view. It also includes the merge function that writes to the silver layer. 
This allows for flexible and iterative data transformations without altering the raw data. It also helps in isolating the transformation logic, making it easier to manage and debug.
### Optimize Data 
For Table Optimization Notebook, the data is optimized and its retention period is set to ensure efficiency of data 

### Data Quality Checks
# Summary
## What is archived
## Quick starts




_________________________________

















