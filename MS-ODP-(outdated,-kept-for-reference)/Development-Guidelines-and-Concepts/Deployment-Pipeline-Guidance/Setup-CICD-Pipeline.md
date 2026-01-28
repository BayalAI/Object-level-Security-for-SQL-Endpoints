[[_TOC_]]

# Introduction
This documentation describes how to setup a deployment pipeline in Fabric and also in Azure DevOps. 
Additional documentation can be found on:

Fabric Pipelines
[Get started using deployment pipelines, the Fabric Application lifecycle management (ALM) tool - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/en-us/fabric/cicd/deployment-pipelines/get-started-with-deployment-pipelines?tabs=from-fabric%2Cnew%2Cstage-settings-new)
      
Azure Pipelines (we use the modern yaml version)
[Azure Pipelines documentation - Azure DevOps | Microsoft Learn](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops)

# Requirements
- Technical account with MFA
- Service principal 
  - A service principal needs to be created with required permissions to the azure resources.
  - A service connection is required in Azure DevOps for deployment purpose.
  - This service principal needs "Directory Reader permission" to deploy sql user (https://aka.ms/sqlaadsetup)

- Fabric Workspace
  - All required workspaces need to be available like Dev, Test, UAT & Prod.
  - Dev workspace needs to be configured with ADO repo.
- Access to [Workspace name] 
  - All workspaces should have at least contributor access to Service principal.

# Setup Fabric Deployment Pipeline 
**1. Prerequisites**
--------------------

1.  **Workspace Access**:
    *   Ensure you have a Microsoft Fabric workspace with appropriate permissions.
    *   You need at least **Contributor** access to the workspace.
2.  **Artifacts to Deploy**:
    *   Have resources (e.g., Data Pipelines, Reports, or Datasets) in the workspace.
3.  **Deployment Pipeline Feature**:
    *   Confirm the **Deployment Pipelines** feature is enabled in Microsoft Fabric for your tenant.

**2. Create a Deployment Pipeline**
-----------------------------------

1.  **Navigate to Deployment Pipelines**:
    *   Open the **Microsoft Fabric portal**.
    *   Select **Deployment Pipelines** from the menu.
2.  **Create a New Pipeline**:
    *   Click **New Pipeline**.
    *   Provide a **Name** for your pipeline.
    *   Assign the pipeline to a **Workspace** that contains the source artifacts for deployment.
3.  **Add Pipeline Stages**:
    *   Deployment pipelines in Fabric have three stages: **Development**, **Test**, and **Production**.
    *   Map your Fabric workspaces to each stage:
        *   Development: For creating and testing new artifacts.
        *   Test: For staging and validation.
        *   Production: For live data and reporting.

# Setup Deployment Framework in Workspace Dev
- Assign permissions onto workspace level to Service Principal & Technical account
  1.  **Navigate to the Fabric Workspace**:
      *   Open the Microsoft Fabric portal.
      *   Select the **Workspace** you are configuring.
  2.  **Add Service Principal & Technical Account**:
      *   Go to **Manage Access** → **Add people or groups**.
      *   Input **Enter name or email** → Select the **Service Principal** and **Technical Account**.
      *   Assign **Contributor** role for full deployment access.

- Which objects to copy from [Workspace]
- Setup deployment/deployment_config notebook

# Setup the permission and user management sql project
##  **How to Create a SQL Project and connect to DevOps Repo using VSCode**
1.  **Install Visual Studio Code**:
    *   Download and install [Visual Studio Code](https://code.visualstudio.com/) if not installed already.
2.  **Install Required Extensions**:
    *   Install the **SQL Database Projects** extension:
        *   Go to the Extensions view (`Ctrl+Shift+X`).
        *   Search for `SQL Database Projects` and click **Install**.
    *   Install the **Azure Repos** or **Git** extension (optional for Azure Repos integration).
3.  **Set Up Azure Repo**:
    *   Ensure Azure DevOps Repo is configured and accessible:
        *   Ensure ADO repo is setup with all required access permission.
        *   Create a separate folder to store SQL project related artifacts.
        *   Clone the repo to local.
4.  **Open SQL Database Projects Extension**:
    *   Click on the `SQL Database Projects` extension in the Activity Bar.
5.  **Create a New Project**:
    *   Click on **New Project**.
    *   Specify a name for your project (e.g., `MySQLProject`).
    *   Choose a folder location for the project (point to the newly created folder in your local cloned repo location).
    *   Select the target platform (e.g., **Azure SQL Database**).
    *   The project structure will be created, including `MySQLProject.sqlproj`.
6.  **Add Database Objects**:
    *   Right-click the project and choose **Add Script**, **Add Post-Deployment Script**, **Add Publish profile** or any other database object.
    *   Create required folders (like Security, Roles, etc.).
    *   Add required script definition (like CREATE ROLE, GRANT/DENY, etc.) to script files.

**Detailed Document Reference**
[Fabric SQL Analytics End Point Deployment - Overview](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_wiki/wikis/Fabric-OneLake.wiki/121/Fabric-SQL-Analytics-End-Point-Deployment)




# Setup ADO

##  **How to Create a service connection**

   *   Open Azure DevOps.
   *   Select your **Organization** and **Project**.
   *   In the left-hand menu, go to **Project Settings** > **Service connections** (under Pipelines) >  **Create Service Connection** > **select Azure Resource Manager** (in Connection Type) > click **Next**.
![image.png](/.attachments/image-611a8d9f-a8e9-4fd3-b5cd-a2cc15d2fff0.png)

##  **How to create a pipeline**

  *  Go to your Azure DevOps project.
  *  Select **Pipelines** > **New Pipeline**.
![image.png](/.attachments/image-8a1bb720-9a59-4ab4-ae1b-7681891467fc.png)
  *  Choose your repository as Azure Repos Git.
![image.png](/.attachments/image-ad67906e-71a6-4523-bc67-a44fa2767fa0.png)
  *  Select repository.
![image.png](/.attachments/image-b35eeca5-ef95-48b8-a9d0-cc992b366f3b.png)
  *  Select **Starter Pipeline** or create a pipeline using **YAML**.
![image.png](/.attachments/image-81b0a49c-f25c-4495-bcfd-2cda71bf9bca.png)

##  **How to adapt the YAML towards your project**

Adapting a **YAML pipeline** to fit your specific project involves customizing variables, paths, tasks, and configuration to align with your environment, deployment needs, and resource structure.

**1. Understand Your Project Requirements**

   *   **What are you deploying?**  
    Example: SQL endpoints, Fabric data pipelines, Lakehouses, or other resources.
    
   *   **What tools or scripts are required?**  
    Example: SQL Project, Azure CLI, REST API, PowerShell, or custom scripts.
    
   *   **What is your source repository?**  
    Example: Azure Repos, GitHub, or other repositories.
    
   *   **What is your target environment?**  
    Example: Microsoft Fabric workspace

 **2. Identify Key Configurations for Your Project**
-    **Variables**  
    Define variables for values that might change between environments or pipelines.
    Example Script:
```yaml
variables:
  fabricSqlConnection: '<Your-Service-Connection>'
  targetServer: 'your-fabric-endpoint.datawarehouse.fabric.microsoft.com'
  targetDatabase: 'YourDatabaseName'
```
-    **Artifacts and Paths**  
    -    Script files like `.sql` or `.ps1`.
    -    JSON definition files for pipelines, datasets, or lakehouses.
-    **Authentication**
    -    Use a **Service Connection** to manage access to resources like Fabric SQL or Pipelines.
    -    Store secrets (e.g., passwords) in **Azure DevOps pipeline variables.

   
##  **How to run it first**
**1. Ensure the Pipeline is Ready**

Before running the pipeline:
  * Confirm the pipeline YAML file is committed to the repository.
  * Verify that all necessary configurations, like variables, service connections, and permissions, are set up.
  * Make sure your repository is linked to your Azure DevOps project.

**2. Navigate to the Pipelines Section**

  * Log in to the Azure DevOps portal.
  * Select your **Project**.
  * From the left menu, click on **Pipelines**.

**3. Locate Your Pipeline**

*   If you’ve already created the pipeline:
    *   You should see it listed under the **Pipelines** tab.
*   If not:
    *   Click **New Pipeline**, follow the prompts to create it from your repository or a YAML file, and save it.

**4. Run the Pipeline**

To trigger the pipeline for the first time:
  * **Select the Pipeline** from the list.
  * Click on **Run Pipeline**.
  * Review the default configuration:
    *   **Branch**: Ensure it’s pointing to the correct branch (e.g., `main` or `develop`).
    *   **Parameters** (if applicable): Confirm or update input parameters for the pipeline.
  * Click **Run**.
# Summary
*   **Accounts and Permissions**:
    *   Technical account with MFA.
    *   Service principal with required permissions for Azure resources.
    *   Azure DevOps (ADO) service connection setup for deployment.
*   **Fabric Workspaces**:
    *   Workspaces needed: Dev, Test, UAT, and Prod.
    *   Dev workspace must be connected to the ADO repository.
    *   Contributor access for service principal on all workspaces.
*   **Prerequisites**:
    *   Microsoft Fabric workspace with contributor access.
    *   Artifacts (Data Pipelines, Reports, Datasets) available for deployment.
    *   Deployment Pipelines feature enabled in Fabric tenant.
*   **Creating the Pipeline**:
    *   Navigate to Microsoft Fabric > Deployment Pipelines > Create New Pipeline.
    *   Assign the pipeline to a source workspace and map workspaces to stages (Dev, Test, Prod).
*   **Workspace Configuration**:
    *   Assign contributor permissions to service principal and technical account for deployment.
*   **Setup in VSCode**:
    *   Install **SQL Database Projects** and **Azure Repos** extensions.
    *   Configure and clone the ADO repository.
    *   Create a SQL project, organize scripts, and add database objects.
*   **Deployment**:
    *   Configure folders for database objects (e.g., Security, Roles).
    *   Define scripts for roles, permissions, and other database entities.
*   **Create a Service Connection**:
    *   In ADO, go to Project Settings > Service Connections > Add Azure Resource Manager connection.
*   **Create a Pipeline**:
    *   In ADO, navigate to Pipelines > New Pipeline.
    *   Choose the Azure Repos Git repository and configure YAML.
*   **YAML Adaptation**:
    *   Customize variables, paths, and tasks for your project.
*   **Running the Pipeline**:
    *   Ensure the YAML file is committed and repository is linked.
    *   Run the pipeline from ADO, selecting the correct branch and parameters.