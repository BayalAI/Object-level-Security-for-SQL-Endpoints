# Naming Convention for Fabric

## Introduction
This document outlines the naming convention for _Fabric_ main items such as `workspaces, folders, lakehouses, pipelines, dataflows gen2, notebooks, security groups, service principals, tables, columns, attributes`.

Consistent naming convention help ensure clarity, ease of management, and collaboration across data projects.

This document describes only the recommended convention for Fabric in the scope of the current Octopus project and therefore is not strictly related to a naming convention for others Azure resources.

You can leverage this article if you need for Azure resources:
 https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/resource-naming

## Recommendations
- **Consistency**: Ensure all team members follow the naming conventions strictly.
- **Review**: Periodically review and update the naming conventions as needed.
- **Keep It Short and Simple**: While being descriptive, try to keep the names as short as possible to avoid overly long identifiers.

## Atos Data Domain
Atos data domain list is referenced in documentation provided by Atos (Atos-Data-Modelling-version communicated to MS 27092024 or newer document). Please refers to the latest documentation from Atos when searching for a new domain name.
At time of writing:
- PARTNERS
- EMPLOYEE
- PORTFOLIO
- CUSTOMER
- FINANCE
- DEI
- SUSTAINABILITY

_DEI is for Diversity, Equity & Inclusion_

`▶      Seven top-level Data Domains covering the whole company scope.`
`▶	Finance, Sustainability and Diversity, Equity & Inclusion are Data Domains specifically related to Enterprise Performance.`

![image.png](/.attachments/image-fac88d61-d362-436e-9c2e-8ccbc10f2556.png)

## Workspaces
### Definition ###
A **workspace** in Microsoft Fabric is a container that holds various items needed for data projects, such as folders, lakehouses, dataflows, Data Factory pipelines, notebooks, Power BI semantic models, and reports. Workspaces help organize and manage these items, providing a collaborative environment for teams to work on data projects.

### Format **For Bronze and Silver layer** 
`<ProjectCode>_<DateSource>_<EnvironmentCode>_INGEST`

### Example **For Bronze and Silver layer** 
`ODP_SAP_DEV_INGEST`

 ![image.png](/.attachments/image-e5a02c9f-308f-446a-8caa-df943ff98a2b.png)

### Guidelines **For Bronze and Silver layer** 
- **ProjectCode**: Use the code for the project. `ODP` is code for Octopus Data Platform project.
- **DataSource**: Use the date source. `SAP` is the data source for all SAP data (time, HR, Finance).
- **EnvironmentCode**: Indicate the environment (e.g., `DEV`, `TST`, `PRD`).
- **INGEST**: Use the word INGEST (for ingestion) for Bronze and Silver layers.

### Format **For Gold layer** 
`<ProjectCode>_<DateDomain>_<EnvironmentCode>_GOLD`

### Example **For Gold layer** 
`ODP_CUSTOMER_DEV_GOLD`

![image.png](/.attachments/image-ab918d34-2d4f-4813-ba37-c2a31c0ea477.png)

### Guidelines **For Bronze and Silver layer** 
- **ProjectCode**: Use the code for the project. `ODP` is code for Octopus Data Platform project.
- **DataDomain**: Use the date domain name from Atos Data Domain. `CUSTOMER` is one of the data domain.
- **EnvironmentCode**: Indicate the environment (e.g., `DEV`, `TST`, `PRD`).
- **GOLD**: Use the word GOLD for GoldLayer.

## Folders
### Definition ###
In Microsoft Fabric, folders are organizational units inside a workspace that enable users to efficiently organize and manage artifacts. They help in grouping and categorizing items based on various criteria such as categories, deployment stages, or data quality.

### Format **For Bronze and Silver layer** 
`<DataSourceFunctionalDomain or DataSource>_<layer>`

### Example
`Time_Bronze`
`Time_Silver`

![image.png](/.attachments/image-7aa05ddd-a6e0-4bf8-a92b-74054775db6b.png)

### Guidelines **For Bronze and Silver layer** 
- **DataSourceFunctionalDomain or DataSource**: When possible, use the sub domain of the data source. `Time`, or `Hr`, or `Finance` are examples of sub domains for data source SAP.
- **Layer**: Indicate the environment (e.g., `Bronze`, `Silver`).

### Format **For Gold layer** 
`<AtosDataMainDomain>_Gold`
### Example
`Customer_Gold`
`Dei_Gold`
`Finance_Gold`

![image.png](/.attachments/image-ca77f0f1-ad08-4f8f-bdc0-16976d509926.png)

### Guidelines **For Gold layer** 
- **AtosDataMainDomain or DataSource**: one of the 7 Atos Top Data Domain Name.
- **Layer**: Gold for the Gold.

## Lakehouses
### Definition ###
A **lakehouse** is a unified data platform that combines the capabilities of a data lake and a data warehouse. It allows you to store, manage, and analyze both structured and unstructured data in a single location. A lakehouse is focused on data storage and analytics, while a workspace is a broader organizational structure that contains and manages various data-related items, including lakehouses.

### Format **For Bronze and Silver layer** 
`<DataSourceFunctionalDomain or DataSource>_<layer>`

### Example
`Time_Bronze`
`Time_Silver`

### Guidelines **For Bronze and Silver layer** 
- **DataSourceFunctionalDomain or DataSource**: When possible, use the sub domain of the data source. `Time`, or `Hr`, or `Finance` are examples of sub domains for data source SAP.
- **Layer**: Indicate the environment (e.g., `Bronze`, `Silver`).

![image.png](/.attachments/image-b93ee882-30eb-4b01-a4bd-9666e709d711.png)

### Format **For Gold layer** 
`<AtosDataMainDomain>_Gold`
### Example
`Customer_Gold`
`Dei_Gold`
`Finance_Gold`

### Guidelines **For Gold layer** 
- **AtosDataMainDomain or DataSource**: one of the 7 Atos Top Data Domain Name.
- **Layer**: Gold for the Gold.

![image.png](/.attachments/image-60127925-14da-4230-ae37-eaa2bd76fabd.png)

## Pipelines
### Format **For Bronze and Silver layer** 
`<DataSourceFunctionalDomain >_<Layer>_<MAINSOURCENAMEAction>`

### Example **For Bronze and Silver layer** 
`Time_Bronze_SAPMain`
`Time_Bronze_SAPCopyData`

![image.png](/.attachments/image-b4d48daf-c104-448e-b0fe-3508b3f1c80b.png)
![image.png](/.attachments/image-d342b1c5-03aa-4da0-8077-c352b213748b.png)

### Guidelines **For Bronze and Silver layer** 
- **DataSourceFunctionalDomain or DataSource**: When possible, use the sub domain of the data source. `Time`, or `Hr`, or `Finance` are examples of sub domains for data source SAP.
- **Layer**: Indicate the environment (e.g., `Bronze`, `Silver`).
- **MAINSOURCENAMEAction**: Main source name (e.g., `SAP`, `SAC`) followed by the action name (e.g., `CopyData`, `Cleaning`, `Main`)

## Dataflow gen2 **For Bronze and Silver layer** 
### Definition ###
Dataflow Gen2 in Microsoft Fabric is an advanced data preparation and transformation tool designed to handle large-scale data processing task. Low-Code Data Preparation: It provides a low-code environment for data preparation, making it accessible to users with varying levels of technical expertise.

### Format **For Bronze and Silver layer** 
`<DataSourceFunctionalDomain >_<Layer>_<MAINSOURCENAMEAction>`

### Example **For Bronze and Silver layer** 
`Time_Bronze_SAPCopyData`

![image.png](/.attachments/image-6bff9de3-c464-4fcc-a954-b1f510d6d346.png)

### Guidelines **For Bronze and Silver layer** 
- **DataSourceFunctionalDomain or DataSource**: When possible, use the sub domain of the data source. `Time`, or `Hr`, or `Finance` are examples of sub domains for data source SAP.
- **Layer**: Indicate the environment (e.g., `Bronze`, `Silver`).
- **MAINSOURCENAMEAction**: Main source name (e.g., `SAP`, `SAC`) followed by the action name (e.g., `CopyData`, `Cleaning`)

## Notebooks **For Bronze and Silver layer** 
### Format
`<DataSourceFunctionalDomain >_<Layer>_<MAINSOURCENAMEAction>`

### Example **For Bronze and Silver layer** 
`Time_Bronze_SAPCleaning`


![image.png](/.attachments/image-6d9eca3f-ac2d-49ed-b9d5-57ae6e56aed0.png)
### Guidelines **For Bronze and Silver layer** 
- **ProjectCode**: Use the code for the project. `ODP` is code for Octopus Data Platform project.
- **Purpose**: Describe the purpose of the notebook (e.g., `DataCleaning`, `Analysis`).

## Security Groups
### Format
`<ORGANISATIONUNITCODE>-<PROJECTCODE>-<TEAMCODE>-<RoleName>`

### Example
`GIT-ODP-Admin`
`GIT-ODP-Developer`

![image.png](/.attachments/image-45e6517d-a00a-4a9a-b55b-74b170cf77cc.png)

### Guidelines
- **ORGANISATIONUNITCODE**: Atos Organisation unit code. `GIT` is an example.
- **PROJECTCODE**: Use the code for the project. `ODP` is code for Octopus Data Platform project.
- **TEAMCODE**: Use the code of the team. `MS` is an example.
- **Population**: Use the target population of the group (e.g. `Admin`, `Developer`). It can be different than the role applied to the group ((e.g. `Developer` but role is `Contributor`).

## Service Principals
### Definition ###
 A service principal in Microsoft Fabric is an application-based security identity that can be assigned permissions to access data sources. It is used to safely connect to data without using a user identity. Service principals are supported in various components of Microsoft Fabric, such as datasets, dataflows (both Dataflow Gen1 and Dataflow Gen2), and datamarts. For example, you can use a service principal to connect to Azure Data Lake Storage Gen2 through Dataflow Gen2 by creating a service principal in Azure, granting it the necessary permissions, and then using it to authenticate to the data source.

### Format
<span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>

### Example
<span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>

### Guidelines
<span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>

## Tables <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
### Format
`<SchemaName>_<Entity>`

### Example <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
For a table in the Sales schema: `Sales_Customers`
For a table in the Marketing schema: `Marketing_Campaigns`

### Guidelines
- **SchemaName**: Same as the project name used in workspaces.
- **Entity**: Describe the entity the table represents (e.g., `Customers`, `Sales`).

## Columns <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
### Format
`<Column>`
- **Clarity**: For column, avoid the use of acronyms except when the meaning of acronym is not known (Ex: use `CustomerIdentity` instead of `CustomerID`). Avoid using space(s) when naming the column (Ex: use `CustomerIdentity` instead of `Customer Identity`). Also, do not use plural form (Ex: use `Customer` instead of `Customers`)

### Example <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
`Customer_ID`, `Customer_Name`

### Guidelines <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
- **Entity**: Use the entity name the column belongs to.
- **Attribute**: Describe the attribute (e.g., `Identity`, `Name`).

## Attributes <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
We can here leverage if needed the data type convention provided by Atos in the Data Model word document.

Table: Customer <span style="background-color: yellow;">TO BE DEFINED WITH Atos</span>
|CustomerIdentifier|CustomerBusinessKey|CustomerName|CustomerCode|CustomerSalary|
|:--|:--|:--|:--|:--|
| 123| HASH(CustomerName+RegistrationDate+BirthDate)|   |   |   |
| 124| 124|


