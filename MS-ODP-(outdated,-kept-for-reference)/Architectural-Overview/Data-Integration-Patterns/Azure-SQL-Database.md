[[_TOC_]]

# Introduction & Motivation
Azure SQL Database is a fully managed relational database service designed for developers. This page provides integration patterns, architectural considerations, and best practices for using Azure SQL Database with Microsoft Fabric. You will find different options/pattern to integrate SAP Hana on this page.
Please consider also the chapter "Architectural Considerations" for final decisions!

# Data Sources supported with fabric
- Azure SQL Database: A fully managed cloud database service that integrates seamlessly with Microsoft Fabric, providing high availability, scalability, and security for your data needs.
- Managed SQL Instance: A managed SQL Server instance in Azure that combines the best features of SQL Server with the benefits of a fully managed platform, including automated updates and backups, making it easy to integrate with Fabric. 

Additionally, Microsoft Fabric supports many other data sources, such as Azure Data Explorer, Azure SQL Data Warehouse, and Lakehouse.  
<A  href="https://learn.microsoft.com/en-us/fabric/data-factory/connector-overview">Connector overview - Microsoft Fabric | Microsoft Learn</A>

Here in this document, we will see Azure SQL Database support with Fabric

# Network setup
Using a Workspace Private Endpoint for your Azure SQL Database connection in Microsoft Fabric offers several advantages:
1. Enhanced Security: Private Endpoints ensure that your data traffic remains within the Azure network, reducing exposure to the public internet and minimizing the risk of data breaches.
2. Improved Performance: By keeping the traffic within the Azure backbone, you can achieve lower latency and higher throughput, which is crucial for performance-sensitive applications.
3. Compliance: Many organizations have strict compliance requirements that mandate the use of private network connections to protect sensitive data. Private Endpoints help meet these regulatory standards
4. Simplified Network Architecture: Using Private Endpoints can simplify your network architecture by eliminating the need for complex firewall rules and VPN configurations

For detailed steps on setting up a connection to an Azure SQL Database using a Workspace Private Endpoint, you can refer to the following resources from Microsoft:
- <A  href="https://learn.microsoft.com/en-us/fabric/data-factory/connector-azure-sql-database">Set up your Azure SQL Database connection - Microsoft Fabric | Microsoft Learn</A>
- <A  href="https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-sql-database-tutorial">Tutorial: Configure Microsoft Fabric Mirrored Databases From Azure SQL Database - Microsoft Fabric | Microsoft Learn</A>

These guides provide comprehensive instructions on configuring your Azure SQL Database connections, including authentication methods and network settings

#Authorization using Workspace Identity
Workspace Identity refers to the use of a managed identity provided by Azure Active Directory (Azure AD) to authenticate and authorize access to Azure SQL Database. This approach leverages the built-in identity management capabilities of Azure AD, ensuring secure and streamlined access without the need for storing and managing credentials manually.

Benefits:
- Enhanced Security: By using Azure AD identities, you eliminate the need to store and manage database credentials, reducing the risk of credential theft.
- Simplified Management: Managed identities are automatically managed by Azure, simplifying the process of identity lifecycle management.
- Seamless Integration: Azure AD integration allows for seamless access management across various Azure services, ensuring consistent and secure access control.

#Power BI gateway requirement
A Power BI gateway is a software component that facilitates secure data transfer between on-premises data sources and Power BI services. It ensures that data can be refreshed and accessed securely from the cloud without exposing the on-premises data sources directly to the internet

A Power BI gateway is **not required** for setting up an Azure SQL Database connection in Microsoft Fabric if you are connecting directly to the Azure SQL Database. This is because Azure SQL Database is a cloud-based service, and Power BI can connect to it directly without needing a gateway

#Fabric Native Support
Azure SQL Database is natively supported within Microsoft Fabric, meaning it can be seamlessly integrated and utilized within the Fabric environment. However, it is important to note that while Azure SQL Database is supported, **mirroring is not available** for private networking setups. This means that data replication or mirroring features, which are typically used for high availability and disaster recovery, cannot be used in this context.

#Workaround Method
Instead of using mirroring, which is typically used for high availability and disaster recovery, you need to use **data copy methods** to replicate your data.

**Why Data Copy is Used:**
- Mirroring Limitation: Mirroring is only supported via public access on the SQL server, which is not suitable for private networking due to security and compliance concerns.
- Data Redundancy: Data copy methods ensure that your data is replicated and available in multiple locations, providing redundancy and improving data availability.
- Compliance and Security: Using data copy methods within a private network ensures that your data remains secure and compliant with organizational policies and regulations.

**How to Implement Data Copy:**
To implement data copy as a workaround, you can use various tools and services provided by Azure, such as Azure Data Factory, to automate the process of copying data from one database to another.
<A  href="https://learn.microsoft.com/en-us/fabric/database/mirrored-database/azure-sql-database-limitations">Limitations and Behaviors for Fabric Mirrored Databases From Azure SQL Database - Microsoft Fabric | Microsoft Learn</A>
<A  href="https://learn.microsoft.com/en-us/azure/private-link/tutorial-private-endpoint-sql-portal">Tutorial: Connect to an Azure SQL server using an Azure Private Endpoint - Azure portal | Microsoft Learn</A>

# Supported Fabric Items:
Supported Fabric Items refers to the specific components within Microsoft Fabric that can interact with Azure SQL Database. The supported items are Dataflow Gen2 and Pipelines.

- Dataflow Gen2: This is an advanced data preparation tool that enables you to clean, transform, and load data from various sources into your Azure SQL Database.
- Pipelines: These are used to orchestrate and automate data workflows, ensuring that data is moved and processed efficiently across different stages of your data integration process.

# Permissions Required for Connection Creation:
Permissions Required for Connection Creation refers to the specific permissions that a user must have to establish a connection to the Azure SQL Database within Microsoft Fabric. Typically, these permissions include:

- Database Contributor: This role allows the user to create and manage databases within the Azure SQL Database.
- Network Contributor: This role is necessary if the connection involves configuring network settings, such as setting up private endpoints. 

# Permissions Required for Connection Usage:
Permissions Required for Connection Usage refers to the permissions needed for a user to utilize an existing connection to the Azure SQL Database. These permissions ensure that the user can access and interact with the data stored in the database. Common permissions include:

- Reader: This role allows the user to read data from the Azure SQL Database.
- Data Factory Contributor: This role is necessary if the user needs to run data integration processes using Dataflow Gen2 or Pipelines.



# Architectural Considerations
Mirroring:
- As of today (Sep 2024) Mirroring is only supported via public access on the SQL server. This is not supported by Atos governance. There data must be copied into the OneLake