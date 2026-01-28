# Data Ingestion Pattern for SAP

- Status: review
- Deciders: Christian Wolff, Archi Gupta, Jürgen Krauth
- Technical Story:

## Context and Problem Statement

This ADR aims to clarify the approach the Octopus Fabric platform will take in terms of Fabric capacity sizing. A solution should be cost effective as well as provide a stable end user experience.

## Decision Drivers <!-- optional -->

- Fabric supports the concept of Bursting and Smoothing. This concept has multiple escalation stages when customers are heavily overusing the capacity ordered within a certain time period. The last escalation stage is shutting down the capacity for 24 hours. 
- Fabric offers 3 kind of activity times. Background ETL, Report/Dashboard usage & Interactive workloads. All there consume capacity units. 
- Reports must be useable at anytime with predictable but changing patterns over a monthly timeperiod.
- Reports must be hosted on a Fabric F64 capacity as minimal SKU as this would remove the need to provide PowerBI Pro licenses to all end users.
- Increasing an Fabric capacity SKU always means a double in pricing and capacity units available

## Considered Options

- One big capacity
- One capacity per workload (reporting & data engineering)
- Capacities per business domain and workload (reporting, interactive, & data engineering)

## Decision Outcome

Chosen option: 
- One capacity per workload and stage

1 F64 for Data Engineering
1 F64 for Reporting
2 Stages which means a total of 4 F64 capacities
![image.png](/.attachments/image-176ec8cb-3513-4cf1-9fcf-6d175462060e.png)
### Decision reasoning

Atos is aware the overall operational overhead with to many capacities at the start. Therefore, a lean approach to capacities will be taken. Microsoft and Atos came to the conclusion that given 4 capacities is a good starting point for the evaluation. Microsoft will support Atos on sizing monitoring. If sizing will have to be adapted one of following 3 strategies will be applied
- Increase existing capacity SKU
- Move workloads to new capacities which are domain focused
- Optimize workloads due to code refactoring 
- Optimize cost by moving specific workloads to smaller Fabric capacity SKUs

### One big capacity
- Good, because easy to maintain at the start
- Good, because PowerBI Pro Licenses for consuming content will be included
- Bad, because noise neighbor problem between workloads which could shutdown report experience.
- Bad, because this will lead very quickly to a very high capacity size with poor utilization
- Bad, because its a single point of failure

### One capacity per workload (reporting & data engineering)
- Good, because it keeps reporting apart from interactive and background tasks. Therefore, the impact of noise neighbors is not gone but mitigated.
- Good, because its still rather lean to implement and manage
- Good, because all provisioned resources will be in use 
- Bad, because it will have follow up tasks to move workloads later on to domain capacities
- Bad, because its not the minimal capacity sizing/cost option


### Capacities per business domain and workload (reporting, interactive, & data engineering)
- Good, because its the less costly option
- Good, because its aligned with the Atos business domains
- Good, because chargeback is easy to implement with already existing Atos cost overview in Azure Portal and Azure Billing API
- Bad, because at the start a lot of capacities will be provisioned but not used as the MVP will only cover a subset of data assets in important business domains
- Bad, because the operational model is the most complex of all options
