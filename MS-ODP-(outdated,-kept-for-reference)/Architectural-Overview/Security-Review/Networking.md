[[_TOC_]]

# Fabric Capabitlities

# Network overview current solutiion

<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/Architecture_HLD_Diagram_v1-MS%20Fabric%20HLD%20global%20design.drawio-4301fa50-639b-4a03-b9c2-2cbe367a88c9.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  alt="Architecture_HLD_Diagram_v1-MS Fabric HLD global design.drawio.png"/>

![image.png](/.attachments/image-d275b0ab-cf85-4dd6-a023-3a57ab256b3d.png)

- KeyVaults are connected via private endpoints
- Azure Storage Account via resource access management (private networking via Microsoft Backbone)
- SAP via Synapse Integration Runtime (private networking)
- No private link around Microsoft Fabric as it a SaaS offering
  - Tenant setup for private link would require change management project for business user access to PowerBI Report
  - Workspace level private link incoming. Workspace structure in place to encapsulate data endpoints from public internet while reports stay available in public internet. 

# Private Link 
## Tenant Settings
- Tenant Private Link (https://learn.microsoft.com/en-us/fabric/security/security-private-links-overview)

## Workspace Setting (Preview Q4/24 -> Preview Q1/25)
https://learn.microsoft.com/en-us/fabric/release-plan/admin-governance#private-link-support-workspace-level


