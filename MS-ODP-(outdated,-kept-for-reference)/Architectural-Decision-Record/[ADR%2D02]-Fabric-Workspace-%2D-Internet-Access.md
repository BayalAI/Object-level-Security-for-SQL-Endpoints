# Data Ingestion Pattern for SAP

- Status: review
- Deciders: Christian Wolff, Archi Gupta, Jürgen Krauth
- Technical Story:

## Context and Problem Statement

The general approach of Atos is to keep all data sources in private networking. There are exceptions for example Salesforce, SAP Analytical Cloud or PowerBI.  

## Decision Drivers <!-- optional -->

- Security guidelines of Atos for data protection
- Best practice for data protection by Microsoft
- Business being able to operate

## Considered Options

- Use Private Link on tenant level
- Keep public access to Fabric assets

## Decision Outcome

Chosen option: 
- Keep public access to Fabric assets

Decision reasoning:
Since Microsoft Fabric currently only supports private link, which shuts down public access to resources, on tenant level, enabling this would have a big impact on the ability of business users and processes to continue using existing PowerBI reports and dashboards. 

### Positive Consequences <!-- optional -->
- Business will be able to continue operate
- A workspace level private link is planned to be shipped by Microsoft by Q4/2024 in public preview - https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#private-link-support-workspace-level
### Negative Consequences <!-- optional -->
- Lakehouses will only be protected by EntraID access management capabilities. 

### Use Private Link on tenant level
- Good, because it removed public access to Atos data assets
- Bad, because its a tenant settings and has a lot of side effects 
- Bad, because we can not asset given side effects in a reasonable time

### Keep public access for Fabric assets
- Good, because business will be able to continue using their PowerBI assets without switching to an internal VPN connection
- Good, because it allows easier access to data assets 
- Bad, because it does not follow either Microsoft nor Atos security guidelines as the Fabric product is still adding major capabilities in terms of data governance and protection.