# Data Ingestion Pattern for SAP

- Status: review
- Deciders: Christian Wolff, Archi Gupta, Jürgen Krauth
- Technical Story:

## Context and Problem Statement

The main source of data for Atos is SAP on-premises. That data tables should be exported on application level and not SAP Hana Database level. Also some of the SAP tables are quite huge. Currently there is a implementation for some SAP Tables in a Azure Synapase Analytics workspace environment. 

## Decision Drivers <!-- optional -->

- Cost of running ingest pipelines
- Support of application level extraction
- High volume data table extraction

## Considered Options

- Continue using the Azure Synapse Analytics workspace environment 
- Move to Fabric SAP Hana connector
- Move to Azure Data Factory connector

## Decision Outcome

Chosen option: 
- Continue and enhance the Azure Synapse Analytics workspace environment
- Check with Fabric Data Integration PG to have an overview of future integration options for SAP

Decision reasoning:
While the ADF option looks good, the setup of the new environment and addition of another release cycle would be a lot of overhead. The Fabric connectors do not support all functionality like CDC and application level access and therefore do not support customer requirements. Therefore, the Synapse option is the only viable for the moment due to time and budget constrains. 

### Positive Consequences <!-- optional -->
- No changes required to the current ingest of SAP data tables
- No additional ingestion cost occure 
### Negative Consequences <!-- optional -->
- Changes to the SAP ingestion have to be done by the Synapse integration team and depend on their release cycle. 

### Continue using the Azure Synapse Analytics workspace environment 
- Good, because the infrastructure and networking setup is done
- Good, because its a stable process Atos is aware of
- Good, because it supports application level access
- Good, because its CDC based which helps with high volume tables
- Bad, because its PaaS and not SaaS
- Bad, because its not covered by the Fabric Capacity pricing

### Move to Fabric SAP Hana connector
- Good, because its built in
- Good, because its within the Fabric capacity pricing
- Good, because networking is solved via private endpoints
- Bad, because it only support database layer extraction and not application level
- Bad, because it does not support CDC extraction

### Move to Azure Data Factory connector
- Good, because its a slim version of the Synapse workspace solution
- Good, because ADF will be able to be mounted within Fabric and have a overall monitoring view within Fabric
- Bad, because it will raise additional cost for ingestion and/or data pipeline implementation
- Bad, because the Infrastructure and networking most by created.