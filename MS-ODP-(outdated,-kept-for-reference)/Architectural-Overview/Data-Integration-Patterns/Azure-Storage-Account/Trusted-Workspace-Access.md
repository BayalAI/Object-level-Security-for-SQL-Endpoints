# Introduction
Fabric allows you to access firewall-enabled Azure Data Lake Storage (ADLS) Gen2 accounts in a secure manner. Fabric workspaces that have a workspace identity can securely access ADLS Gen2 accounts with public network access enabled from selected virtual networks and IP addresses. You can limit ADLS Gen2 access to specific Fabric workspaces.

https://learn.microsoft.com/en-us/fabric/security/security-trusted-workspace-access

## Deployment
You can configure specific Fabric workspaces to access your storage account based on their workspace identity. You can create a resource instance rule by deploying an ARM template with a resource instance rule. To create a resource instance rule:

1. Sign in to the Azure portal and go to Custom deployment.
1. Choose Build your own template in the editor. For a sample ARM template that creates a resource instance rule, see ARM template sample.
1. Create the resource instance rule in the editor. When done, choose Review + Create.
1. On the Basics tab that appears, specify the required project and instance details. When done, choose Review + Create.
1. On the Review + Create tab that appears, review the summary and then select Create. The rule will be submitted for deployment.

1. When deployment is complete, you'll be able to go to the resource.


##Example ARM Template
Required Parameters for Deployment:
Storage Account Resource Group Name

Required ARM Modifications:
Storage Account Name: <storage account name> 
Storage Account Region: <region>
Fabric Workspace Id: <workspace-id>


```
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        {
            "type": "Microsoft.Storage/storageAccounts",
            "apiVersion": "2023-01-01",
            "name": "<storage account name>",
            "location": "<region>",
            "properties": {
                "networkAcls": {
                    "resourceAccessRules": [
                        {
                            "tenantId": "<tenantid>",
                            "resourceId": "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabric/providers/Microsoft.Fabric/workspaces/<workspace-id>"
                        }]
                }
            }
        }
    ]
}
```
