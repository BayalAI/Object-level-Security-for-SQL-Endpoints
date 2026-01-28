# Context

To ingest data from existing sources into MS Fabric, we need to define how the Octopus Fabric platform will handle data consumption from a networking perspective, including relevant patterns.

# Network overview current solution

![image.png](/.attachments/image-d275b0ab-cf85-4dd6-a023-3a57ab256b3d.png =1200x)


- KeyVaults are connected via private endpoints
- Azure Storage Account via resource access management (private networking via Microsoft Backbone)
- SAP via Synapse Integration Runtime (private networking)
- No private link around Microsoft Fabric as it a SaaS offering
  - Tenant setup for private link would require change management project for business user access to PowerBI Report
  - Workspace level private link incoming. Workspace structure in place to encapsulate data endpoints from public internet while reports stay available in public internet. 



##Patterns 1

Fabric supports the concept of OneLake shortcuts to seamlessly integrate and unify data from various sources, including Azure Synapse, into a single virtual data lake.

**OneLake Shortcuts:** These are virtual pointers that reference data stored in other locations, such as Azure Data Lake Storage (ADLS) Gen2 or other cloud storage services. They allow you to access and work with data without duplicating it.

Given that Synapse already utilizes the Self Hosted Integration Runtime (SHIR) to retrieve data from external sources, we'll leverage this existing integration process. We’ll connect via Fabric to Synapse using shortcuts. To enable this connectivity, we'll employ the 'Resource Instance' connectivity process from the Synapse ADLS Gen2 storage to facilitate connections to each Fabric workspace.

_Resource Instance description is listed here :_ [Azure Storage Account](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Overview/Data-Integration-Patterns/Azure-Storage-Account)
### Resource Instance - Network topology diagram
![SA_Resource Instance.png](https://dev.azure.com/atos-cdo/6e47612b-a2d5-4467-9448-2ec800d8c383/_apis/wiki/wikis/ecb0490d-78a0-4557-9ad3-278d093d25de/pages/146/comments/attachments/22aeeb24-cf1e-4e15-ac0b-3d7c06ffa9e5 =300x)

##Patterns 2

The integration pattern involves using private endpoints to securely connect Azure KeyVaults with Microsoft Fabric. This setup ensures that the data traffic between these services remains within the Azure network, providing enhanced security and reducing exposure to the public internet.

**Key Components:**

- **Private Endpoints:** These are network interfaces that connect you privately and securely to a service powered by Azure Private Link. The private endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network.

- **Azure KeyVault:** This service is used to securely store and manage sensitive information such as keys, secrets, and certificates. By integrating it with private endpoints, you ensure that access to the KeyVault is restricted to resources within your virtual network.

- **Microsoft Fabric:** This platform supports various workloads, including data exploration and processing, by securely accessing data sources through managed private endpoints. These endpoints allow Fabric workloads to interact with data sources behind firewalls or blocked from public internet access.

**Benefits:**
-
- **Enhanced Security:** By keeping the data traffic within the Azure network, you reduce the risk of exposure to the public internet.
- **Simplified** Network Configuration: Managed private endpoints simplify the network configuration by handling the complexities of secure connections.
- **Improved Performance:** With private endpoints, you can achieve lower latency and higher throughput by avoiding the public internet.

This integration pattern provides a robust and secure way to connect Azure KeyVaults with Microsoft Fabric, ensuring that your sensitive data remains protected while being easily accessible for your workloads.

###KeyVaults connected via private endpoints
![image.png](/.attachments/image-7262be95-2cca-4c08-8c9d-f465b47c6a8e.png =300x)


# Private Link 
## Tenant Settings
- Tenant Private Link (https://learn.microsoft.com/en-us/fabric/security/security-private-links-overview)

## Workspace Setting (Preview Q4/24 -> Preview Q1/25)
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#private-link-support-workspace-level