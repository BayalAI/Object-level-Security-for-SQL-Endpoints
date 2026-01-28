#Introduction
A Fabric workspace identity is an automatically managed service principal that can be associated with a Fabric workspace. You can use the workspace identity as an authentication method when connecting Fabric items in the workspace to resources that support Microsoft Entra authentication. Workspace identity is a secure authentication method as there is no need to manage keys, secrets, and certificates. When you grant the workspace identity with permissions on target resources such as ADLS gen 2, Fabric can use the identity to obtain Microsoft Entra tokens to access the resource.

https://learn.microsoft.com/en-us/fabric/security/workspace-identity-authenticate

## Steps to Configure

1. Create the workspace identity
1. Grant the identity permissions on the storage account
   - Sign in to the Azure portal and navigate to the storage account you want to access from OneLake.
   - Select the Access control (IAM) tab on the left sidebar and select Role assignments.
   - Select the Add button and select Add role assignment.
   - Select the role you want to assign to the identity, such as _Storage Blob Data Reader_ or _Storage Blob Data Contributor_.
**Note - The role must be provided at the Storage account level**
 1. Create the OneLake Shortcut
