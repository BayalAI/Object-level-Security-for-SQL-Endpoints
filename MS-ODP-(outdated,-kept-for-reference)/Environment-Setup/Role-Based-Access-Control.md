[[_TOC_]]

# Azure Keyvault RBAC assignments for MS Fabric Workspaces
## Development & Integration Environments
| Name | Environment | Type | Assigned To AKV | Role | Susbscription Name
|--|--|--|--|--|--|
| GIT-ODP-Admin | DEV / INT | Azure Security Group | kv-gitda-dev-bup-gewc<br> kv-gitda-dev-dri-gewc<br> kv-gitda-dev-irs-gewc<br> kv-gitda-dev-sac-gewc<br> kv-gitda-dev-sap-gewc<br> kv-gitda-dev-sfc-gewc<br> kv-gitda-int-bup-gewc<br> kv-gitda-int-dri-gewc<br> kv-gitda-int-irs-gewc<br> kv-gitda-int-sac-gewc<br> kv-gitda-int-sap-gewc<br> kv-gitda-int-sfc-gewc | Key Vault Secrets User, Key Vault Secrets Officer | GIT-DA-Staging |
| GIT-ODP-Developer | DEV / INT | Azure Security Group | kv-gitda-dev-bup-gewc<br> kv-gitda-dev-dri-gewc<br> kv-gitda-dev-irs-gewc<br> kv-gitda-dev-sac-gewc<br> kv-gitda-dev-sap-gewc<br> kv-gitda-dev-sfc-gewc<br> kv-gitda-int-bup-gewc<br> kv-gitda-int-dri-gewc<br> kv-gitda-int-irs-gewc<br> kv-gitda-int-sac-gewc<br> kv-gitda-int-sap-gewc<br> kv-gitda-int-sfc-gewc | Key Vault Secrets User, Key Vault Secrets Officer | GIT-DA-Staging |
| ODP_BUP_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-bup-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_DIARIE_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-dri-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_IRIS_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-irs-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SAC_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-sac-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SAP_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-sap-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SALESFORCE_DEV_INGEST | DEV | MS Fabric Workspace Service Principal | kv-gitda-dev-sfc-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_BUP_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-bup-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_DIARIE_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-dri-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_IRIS_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-irs-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SAC_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-sac-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SAP_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-sap-gewc | Key Vault Secrets User | GIT-DA-Staging |
| ODP_SALESFORCE_INT_INGEST | INT | MS Fabric Workspace Service Principal | kv-gitda-int-sfc-gewc | Key Vault Secrets User | GIT-DA-Staging |

## Production Environment (In Progress)
| Name | Environment | Type | Assigned To AKV | Role | Susbscription Name
|--|--|--|--|--|--|
| GIT-ODP-Admin | PROD | Azure Security Group | kv-gitda-prd-bup-gewc<br> kv-gitda-prd-dri-gewc<br> kv-gitda-prd-irs-gewc<br> kv-gitda-prd-sac-gewc<br> kv-gitda-prd-sap-gewc<br> kv-gitda-prd-sfc-gewc | Key Vault Secrets User, Key Vault Secrets Officer | GIT-DA-Production |
| GIT-ODP-Developer | PROD | Azure Security Group | kv-gitda-prd-bup-gewc<br> kv-gitda-prd-dri-gewc<br> kv-gitda-prd-irs-gewc<br> kv-gitda-prd-sac-gewc<br> kv-gitda-prd-sap-gewc<br> kv-gitda-prd-sfc-gewc | Key Vault Secrets User, Key Vault Secrets Officer | GIT-DA-Production |
| ODP_BUP_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-bup-gewc | Key Vault Secrets User | GIT-DA-Production |
| ODP_DIARIE_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-dri-gewc | Key Vault Secrets User | GIT-DA-Production |
| ODP_IRIS_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-irs-gewc | Key Vault Secrets User | GIT-DA-Production |
| ODP_SAC_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-sac-gewc | Key Vault Secrets User | GIT-DA-Production |
| ODP_SAP_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-sap-gewc | Key Vault Secrets User | GIT-DA-Production |
| ODP_SALESFORCE_INGEST | PROD | MS Fabric Workspace Service Principal | kv-gitda-prd-sfc-gewc | Key Vault Secrets User | GIT-DA-Production |
