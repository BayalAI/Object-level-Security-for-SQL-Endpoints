[[_TOC_]]

# Data Source 
**Azure Storage Account** is a cloud-based storage solution provided by Microsoft Azure. It acts as a container that groups all Azure Storage data objects, including blobs, files, queues, and tables.

# Virtual Network (VNet) Integration
VNet Integration ensures secure access to the Azure Storage Account by restricting access to specific virtual networks. Configure the storage account to allow access only from selected VNets. This enhances security by preventing unauthorized access.

#Authorization
[Trusted Workspace Access](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Overview/Data-Integration-Patterns/Azure-Storage-Account/Trusted-Workspace-Access)
[Authenticate with Workspace Identity](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Overview/Data-Integration-Patterns/Azure-Storage-Account/Authenticate-with-Workspace-Identity)

# Power BI Gateway required
A Power BI gateway is a software component that facilitates secure data transfer between on-premises data sources and Power BI services. It ensures that data can be refreshed and accessed securely from the cloud without exposing the on-premises data sources directly to the internet
A Power BI gateway is **not required** for setting up an Azure Storage Account connection in Microsoft Fabric since the data is stored in Azure Storage Account, which is a cloud service, Fabric can directly connect to it without needing an on-premises data gateway.

# Fabric Native Support
Fabric Native Support is available for an Azure Storage Account as fabric has built in capabilities to directly connect and interact with it. 

#Supported Fabric Items
- Dataflow Gen2
- Pipelines
- Notebooks

#Permissions Required for Connection Creation
- Workspace Identity permissions - Blob Data Contributor
- Connection user permissions - Workspace Contributor role in Fabric
- Azure AD Authentication

#Permissions Required for Connection Usage
- Workspace Identity permissions - Storage Blob Data Reader
- Connection user permissions - Storage Blob Data Reader, Storage blob data contributor
- Azure AD Authentication



### Resource Instance - Network topology diagram
![SA_Resource Instance.png](https://dev.azure.com/atos-cdo/6e47612b-a2d5-4467-9448-2ec800d8c383/_apis/wiki/wikis/ecb0490d-78a0-4557-9ad3-278d093d25de/pages/146/comments/attachments/22aeeb24-cf1e-4e15-ac0b-3d7c06ffa9e5)

Todos: Validate notebook support