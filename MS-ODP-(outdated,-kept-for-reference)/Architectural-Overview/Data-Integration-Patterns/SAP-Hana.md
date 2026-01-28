[[_TOC_]]

# Introduction
**SAP Change Data Capture (CDC)** is a technology that tracks and captures changes (inserts, updates, and deletes) in SAP data sources. This allows for real-time data integration and synchronization between SAP systems and other platforms, such as Microsoft Fabric.

## Benefits of SAP CDC for Fabric Connection:
- Real-Time Data Integration: SAP CDC enables real-time data updates, ensuring that the data in Microsoft Fabric is always current and accurate.
- Efficiency: By capturing only the changes rather than the entire dataset, SAP CDC reduces the amount of data that needs to be processed and transferred, leading to more efficient data handling.
- Seamless Migration: It allows for seamless migration of data from SAP systems to Microsoft Fabric without the need for extensive reinitialization.
- Scalability: SAP CDC supports large datasets and high-frequency changes, making it suitable for enterprise-level data integration.
- Flexibility: It can be used with various SAP systems, including SAP ECC, SAP S/4HANA, SAP BW, and SAP BW/4HANA.

# Data Source: SAP HANA - CDC Connector
### What is SAP HANA 
An in-memory, column-oriented, relational database management system developed by SAP.
Designed for high-speed data processing and real-time analytics.

### What is CDC 
A technology that tracks and captures changes (inserts, updates, and deletes) in data sources.
Enables real-time data integration and synchronization between systems.


The **SAP HANA - CDC Connector** is a tool that helps integrate SAP HANA with other systems by capturing and transferring only the changes made to the data. This ensures that the connected systems always have the most current data without needing to process the entire dataset. It’s efficient, scalable, and supports real-time data updates, making it ideal for enterprise-level data integration.

# Network: Self Hosted Integration Runtime
A **Self Hosted Integration Runtime** is a component that allows you to connect your on-premises data sources to cloud services securely. It acts as a bridge between your local network and cloud-based services.

The Self Hosted Integration Runtime is a secure bridge that connects our on-premises SAP HANA database to cloud services like Microsoft Fabric. It captures real-time changes in the data and transfers them securely, ensuring that our data remains within our network and is not exposed to the internet. This setup provides flexibility, security, and control over our data integration processes.

# Authorization: Technical User

A technical user account with the necessary permissions to access the SAP HANA database is required. This account will be used to authenticate the connection and perform data operations.


# Power BI Gateway required

The Power BI gateway is a bridge that connects on-premises data sources to Power BI, Power Automate, Power Apps, and Azure Logic Apps. It enables secure data transfer between on-premises data sources and cloud services. The gateway is essential for accessing data that resides within an organization's network and is not directly accessible from the cloud.


For the SAP HANA CDC (Change Data Capture) connector, the Power BI gateway is required because it facilitates the connection between the on-premises SAP HANA database and Power BI. The CDC connector captures changes in the SAP HANA database and ensures that these changes are reflected in Power BI reports and dashboards. The gateway ensures secure and efficient data transfer, enabling both scheduled refresh and DirectQuery capabilities.

  

# Fabric Native Support and Workaround Method

Currently, there is no native support for SAP HANA connected using the CDC (Change Data Capture) connector in Microsoft Fabric. However, there is a workaround available.

  

The workaround involves using the Synapse SAP CDC connector. This method allows you to establish a change data feed from SAP into Delta tables in ADLS Gen2, which can then be integrated with Microsoft Fabric OneLake using Azure Data Factory or Synapse Analytics

  

# Permissions Required for Connection Creation and Usage

To create a connection for the SAP HANA CDC (Change Data Capture) connector, you will need the following permissions:

- Technical User Account: This account should have the necessary permissions to access the SAP HANA database. It will be used to authenticate the connection and perform data operations.
- Self-Hosted Integration Runtime (SHIR): Ensure that the SHIR has the appropriate permissions to access the network and communicate with the SAP HANA database. This includes network access permissions and any firewall rules that need to be configured.
- Power BI Gateway: The gateway should have the necessary permissions to securely transfer data between the on-premises SAP HANA database and Power BI. This includes permissions to access the data source and perform data refresh operations.

 
Here are some supported links for explaining this better

1. [Prerequisites and setup for the SAP CDC connector](https://learn.microsoft.com/en-us/fabric/data-factory/connector-sap-hana)

1. [Set up your SAP HANA database connection](https://learn.microsoft.com/en-us/fabric/data-factory/connector-sap-hana)

 ---- 

# SAP HANA - Batch Loading

### What is batch loading

Batch loading is a process that involves loading large volumes of data into a system in a single operation. This method is often used for initial data migrations, periodic data loads, or when dealing with large datasets that need to be processed efficiently.

  

### Benefits of Batch Loading fot Fabric

Efficiency: Batch loading allows for the efficient transfer of large datasets, reducing the time and resources required for data integration.

Scalability: It supports large volumes of data, making it suitable for enterprise-level data integration.

Flexibility: Batch loading can be used with various SAP systems, including SAP ECC, SAP S/4HANA, SAP BW, and SAP BW/4HANA.

Reliability: Ensures data consistency and integrity during the loading process.

### SAP Hana - Batch Loading

The SAP HANA - Batch Loading process helps integrate SAP HANA with other systems by loading large volumes of data in a single operation. This ensures that the connected systems have the necessary data without needing to process it incrementally. It’s efficient, scalable, and supports large-scale data integration, making it ideal for enterprise-level data handling.

  

# Network: Power BI Gateway

The Power BI gateway is a crucial component for connecting on-premises data sources, such as SAP HANA, to cloud services like Power BI. It acts as a bridge, enabling secure data transfer between your on-premises environment and the cloud.

  

1. The Power BI gateway needs to be installed on a server within your network that has access to the SAP HANA database. This server should be reliable and have a stable network connection to ensure seamless data transfer.

  

1. Once the gateway is installed, you can configure it to connect to your SAP HANA database. This involves setting up the data source within the Power BI service, where you provide the necessary connection details such as the server name, database name, and authentication credentials.

  

1. The gateway ensures that data is transferred securely between the SAP HANA database and Power BI. It uses encryption to protect data during transit, ensuring that sensitive information remains secure.

  

1. With the gateway in place, you can set up scheduled refreshes to keep your Power BI reports and dashboards up-to-date with the latest data from SAP HANA. Additionally, the gateway supports DirectQuery, allowing real-time queries against the SAP HANA database without the need to import data into Power BI.

  
  

# Authorization: Technical User

A technical user account with the necessary permissions to access the SAP HANA database is required. This account will be used to authenticate the connection and perform data operations.

  

# Fabric Native Support

Microsoft Fabric uses Data Factory to facilitate the batch loading process from SAP HANA. This integration allows you to efficiently transfer large datasets from SAP HANA to Microsoft Fabric, leveraging the robust capabilities of Data Factory for data ingestion and transformation.

  

1. Data Factory Integration: Data Factory in Microsoft Fabric uses Power Query connectors to connect to SAP HANA. This setup enables you to create dataflows that can batch load data from SAP HANA into Fabric. The process involves setting up a connection in Dataflow Gen2, which supports various authentication types and ensures secure data transfer.

  

1. Power Query Connectors: The Power Query connectors are designed to handle large volumes of data, making them ideal for batch loading scenarios. These connectors support both copy and Dataflow Gen2 operations, allowing you to efficiently move data from SAP HANA to Fabric.

  

1. Data Transformation and Storage: Once the data is loaded into Fabric, you can use various tools and services within Fabric to transform, analyze, and store the data. This includes leveraging Fabric's data warehousing and lakehouse capabilities to manage and process the data effectively

  

# Supported Fabric Items

Supported fabric items include Dataflow Gen2 and pipelines

  
  
  

# Architectural Considerations

- CDC is not available in Fabric yet. The existing connection towards Synapse setup through DLZ is currently the best option to get the data used in Fabric by shortcutting the Synapse storage account. 