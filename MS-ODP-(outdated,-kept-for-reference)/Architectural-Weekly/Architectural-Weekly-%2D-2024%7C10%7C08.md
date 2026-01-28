# Participants
@<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B> 
@<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> 
@<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> 
@<8F850DB8-3C61-640A-B7C6-D101A3AC1172> 
@<8EE8E01C-D574-6CB9-AAAC-E3ECB192A1C3> 


# Agenda
| Topic | Issued By | Description | Priority |
|:------|:----------|:------------|:---------|
|Workspace Overview | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | Runthrough the created workspaces and their strategy |
|CI CD Challenges | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | Unsupported items of lakehouse content and data flows |
|Workspace Access Concept | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C> | How are we going to handle the workspace access? |
| Data Sources Ingested | @<8028F629-D116-6CA1-8EA1-C0E7ACC5A839> | What about SAP HR Table definitions Task? |
| Data sources for sprint 2 | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | which data sources we can aim for in sprint 2? |
| SAC Data Access | @<F2DE3148-CBA1-6AFF-B0D2-DE79E6EFE81C>  | How are we connecting to SAC SQL database |
| Architecture Overview | @<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B>  | | 1 |


# Topic: Architectural Overview
- Data source integration diagram as starting point
- Move to architectural diagram
  - Is the subscription for the capacities the same as the synapse workspace?
  - Different resource groups but same subscription @<A26E216D-1956-6CE2-8B9B-3DF2D403AD6B> - Subscriptions are staged in 2 layers
- Storage account for Synapase is currently public - decision is to handle this as a public data source (no private endpoint)
- Final approval on architecture with Dagwin, Jürgen and Archi on Friday

# Topic - Data source for sprint 1
- SAP Ariba -> to sprint 2 as planning
- SAP SAC -> sprint 1 as planning
- SAP HR -> PA 000 1 -> must be imported into synapase first (currently blocked by atos)
- SAP Finance -> Customer Data 
- SAP Time -> (CATSDB)
- Salesforce -> Opportunities

# Topic - Data Source for sprint 2
- SAP Ariba (rest call)
   -> credentials for rest api availabile ->put into keyvault
   -> documentation ariba rest api (through report export api)
   -> spike of api response -> else ADF way which already exists
   -> mapping already existing in teams
- IRIS from Azure SQL Server (rather easy)
   -> Connection "RPA IRIsDataLake Azure Prod" already existing
   -> mapping might be needed to be created
- Fieldclass (from SAP -> Synapse) 
   -> tables we know
   -> extract to storage (adls or onelake) -> into onelake direct
   -> mapping must be created
- Dairie DB onprem Sql Server)
   -> connection "DIARIE" already available 
   ->  
![image.png](/.attachments/image-9478732c-c1c8-4f34-ac26-b3d143b2d0cf.png)




# Topic 1
![image.png](/.attachments/image-f5791108-1afa-40ca-b4d5-01e5a6077e83.png)



# Topic 2
