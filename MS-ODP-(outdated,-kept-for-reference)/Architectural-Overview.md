# Content

# Architecture
## Overview
![Architecture_HLD_Diagram_v1-MS Fabric HLD global design.drawio.png](/.attachments/Architecture_HLD_Diagram_v1-MS%20Fabric%20HLD%20global%20design.drawio-4301fa50-639b-4a03-b9c2-2cbe367a88c9.png)

- Fabric connects to an currently public Azure Storage Account within the Synapse DLZ. Adaptation towards a network protected Storage Account is possible within Fabric. [Trusted Workspace Access](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Overview/Data-Integration-Patterns/Azure-Storage-Account/Trusted-Workspace-Access)
- Fabric makes use of existing PowerBI gateway to access on-premises data sources
- Fabric makes use of exsiting PowerBI gateway connections. Adaptations e.g. private endpoints to Azure Sql Server are possible [Fabric workspace private endpoint](https://learn.microsoft.com/en-us/fabric/security/security-managed-private-endpoints-overview)
- Fabric will make use of multiple capacties
- Secrets and keys will be stored in Azure KeyVaults. Therefore, Azure KeyVaults will be connected via private endpoints. At runtime secrets will be loaded into Fabric pipelines or notebooks. 
- Fabric will make use of workspace identify (managed service principals) depending if the data source and destination support service principal authorization
- Due to missing CDC connector with application layer access capabilities, SAP data integration will be done via existing Azure Synapse Analytics workspace. 
- SAP data ingestion destination is split:
   - For existing pipelines the existing storage account will be used
   - For new pipelines data will be pushed into the OneLake

## Staging
In total 4 stages will be implemented:
- DEV - Development work of the delivery team
- INT - Technical integration layer 
- UAT - Business validation layer with real business data
- PRD - Business serving layer

Capacity wise 2 stages will be implemented
- STG - For DEV/INT workloads
- PRD - For UAT/PRD workloads

## Capacity Strategy
Atos will start with 2 capacities of the sizing of F64 for reporting and data engineering per stage. This means a total of 4 F64 Capacities.
![image.png](/.attachments/image-1ab2111b-f008-4d68-895d-66c4ead16a41.png)

## Connectors in use

<Atos asked for a detailed overview of which connector is in use for which connection - MSFT will add this overview in Sprint 2>
| Data Source | Connector in use | Identify in use | Destination | Source Permission Set | Destination Permission Set | Connectivity Mode | Workspace | 
|:------------|:----------|:--------|:--------|:---------|:--------|:--------|:------|
| Synapse DLZ (Azure Storage Account) | Microsoft Shortcut | Workspace Identity | n/a | Azure Storage Data Reader | n/a | public OR resource instance | ....|

## Workspace Setup
Workspaces will be split in two sections. Data integration workspaces - called ingest workspaces - and data serving workspaces - called gold

### Data ingest workspace setup:
Data ingest workspaces are data source based e.g. SAP, Salesforce, etc. 
Each data source will have one set of workspaces. 
They will contain bronze and silver layer. Silver lakehouses will be ground source to create the gold layer.
![image.png](/.attachments/image-d9574c32-1adb-487a-abe5-7c5920a0eb4c.png)

### Data serving workspace setup:
Data serving workspaces are Atos business domains oriented e.g. Customer, Employee, etc. 
Each domain will have one set of workspaces. 
They will contain the gold layer and specific data products also known as Facets within Atos. 

![image.png](/.attachments/image-d8d5e4a4-5522-4f2c-b072-e758de9dfb93.png)

## Access Management
### Workspace access management
Workspace access will be managed via Entra ID security groups. Each workspace should come with a set of 4 security groups for admins, contributors, members and viewers. 

### Lakehouse access management 
- If access most be restricted within the data assets lakehouse access management will take place instead of workspace access management. Be reminded that workspace permissions overrule lakehouse access management. 
- For that object level and row level security will be used. Microsoft also announed the support for column level security on the FabCon 2024. 
- All security assignments should be handled by security groups. No direct assignments should be done. 

# Limitations & Risks & Follow Up Activities
- No use of private links means data within lakehouses and OneLake is only protected via EntraID
- Atos will have to adapted over time to manage more then given 4 capacities. Therefore, a operational monitoring model must be developed and implemented.
- Atos sided activities to close the public access on the DLZ Storage Account have to be discussed and implemented when feasible. This also applies to the access management for workspace access. Finally this also applies to the Sql Server connection used in gateways rather then private endpoints.

# Decision Records 
[[ADR 01] SAP Data Integration Pattern [Review]](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Decision-Record/[ADR%2D01]-SAP-Data-Integration-Pattern)
[[ADR 02] Fabric Workspace   Internet Access [Review]](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Decision-Record/[ADR%2D02]-Fabric-Workspace-%2D-Internet-Access-)
[[ADR 03] Fabric Capacity Approach [Review]](/MS-ODP-\(outdated,-kept-for-reference\)/Architectural-Decision-Record/[ADR%2D03]-Fabric-Capacity-Approach)