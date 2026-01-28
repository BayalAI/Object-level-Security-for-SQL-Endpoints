[[_TOC_]]
# Principals
- Use 'ootb' functionality whereever possible, surround with custom process where needed
- Private networking where applicable
- Business continuity must be top priority
- Minimal priviledge access 

# Overview
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/Architecture_HLD_Diagram_v1-MS%20Fabric%20HLD%20global%20design.drawio-4301fa50-639b-4a03-b9c2-2cbe367a88c9.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  alt="Architecture_HLD_Diagram_v1-MS Fabric HLD global design.drawio.png"/>

# Data source integration
// overview of all data sources connected
| Pattern Name | Technical Data System | Connectivity | Identity | Description|
|:-----|:-----|:-----|:-----|:-----|
|SAP Data | SAP HANA, ECC,| Synapase Analytical CDC connector || Already present - no new implementation|
|SAP Data Synapase | Storage Account | Ressource Assignment (Microsoft Backbone) | Workspace Managed Identity| |
|Azure Sql Server | Azure SQL Server/Database| Currently PowerBI Gateway -> Workspace Private Link ||
|Salesforce | Salesforce Cloud SaaS| Public Internet | Technical User without MFA | |



![image.png](/.attachments/image-109d57f9-3015-4879-8d56-f3cf60529592.png)