# architecture of ODP


- Fabric connects to an public Azure Storage Account within the Atos IT data landing zone (DLZ).
- Fabric makes use of existing PowerBI gateway to access on-premises and cloud data sources
- Fabric will make use of multiple capacties
- Secrets and keys stored in Azure KeyVaults. At runtime secrets will be loaded into Fabric pipelines or notebooks. 
- Fabric will make use of workspace identify (managed service principals) depending if the data source and destination support service principal authorization
- Due to missing CDC connector with application layer access capabilities, SAP data integration will be done via existing Azure Synapse Analytics workspace. 
- SAP data ingestion destination is split:
   - For existing Synapse pipelines, data will be loaded from SAP Nessie to Synapse storage account ADSL2 (Bronze/Silver/Gold). The data will be used from ADSL2 parquet files with shortcuts in fabric
   - For new synapse pipelines data will be loaded from SAP Nessie to Synapse storage account ADSL2 Bronze only. Fabric will pick up the Bronze and process the data through Silver and Gold

![Architecture_HLD_Diagram_v1-MS Fabric HLD global design.drawio.png](/.attachments/Architecture_HLD_Diagram_v1-MS%20Fabric%20HLD%20global%20design.drawio-4301fa50-639b-4a03-b9c2-2cbe367a88c9.png =1200x)