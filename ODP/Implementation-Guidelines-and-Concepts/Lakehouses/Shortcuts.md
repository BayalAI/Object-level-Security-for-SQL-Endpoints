Utilize **Shortcuts** in Fabric ODP lakehouse to reference external data without duplicating it.
Shortcuts will be added into our own lakehouse or to the citizen developer lakehouse.
To create and to use shortcuts the user must have read access to the data source. 
Please check dedicated page for lakehouse access control.

**Connection to Octopus**
To connect Fabric with Octopus ADSL2 storage account please use the connection below. The connection is prepared in the power BI gateway.
The authorisation to ADSL2 is managed with the workspace identity. 
- You must generate for the workspace identitity
- You must add the workspace identitity to the Azure AD group GIT-Akela-Reader

Below PBI connection prepared for ADSL2 (Octopus):

1. ADLSGen2_Prd_Wkspc_ID for Octopus production
2. ADLSGen2_stg_Wkspc_ID for Octopus stage

**Connection within Fabric**
1. select source type "Microsoft OneLkae"
2. select the workspace and lakehouse. Pls be careful with prd and stg.
3. select table and modify name if needed 



