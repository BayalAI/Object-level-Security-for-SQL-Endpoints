[[_TOC_]]

# Introduction

This documentation will describe how to create and deploy a Database project
Additional documentation can be found on:

SQL Endpoint/Warhouse Projects in Fabric
[Source control with Warehouse (preview) - Microsoft Fabric | Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-warehouse/source-control)
      
SQL projects
[What are SQL database projects? - SQL Server | Microsoft Learn](https://learn.microsoft.com/en-us/sql/tools/sql-database-projects/sql-database-projects?view=sql-server-ver16)



### **1. Setup SQL Project in Azure Data Studio & Deploy Locally**

Azure Data Studio supports SQL projects through the **SQL Database Projects extension**. Here’s how to **set up and build and deploy/publish the project locally**:

#### **Steps**:
1.  **Install SQL Database Projects Extension**:
    *   Go to Extensions (`Ctrl+Shift+X`).
    *   Search for "SQL Database Projects" and install it.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-60cb7e05-eb2e-46d1-9b6c-9f1500229f19.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width="500" height="150"  alt="image.png"/>
2.  **Create SQL Project**:
    *   Click on **File > New Project > SQL Database**. or create project from database by connecting to source sql end point using connection string and authentication.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-5e9f57cb-a7de-4a25-9f4d-0ad523deb190.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width="500" height="150" alt="image.png"/>
    *   Define the project name and location.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-f1516a82-628d-4c26-a2de-cd1b1dfb03d3.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  width="500" height="450" alt="image.png"/>

    *   Add SQL scripts for objects from Database Projects Tab (e.g., roles, post deployment script).
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-39d3dff0-6143-40dc-a67d-6037f261824b.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster"  width="550" height="450" alt="image.png"/>
3.  **Configure Build**:
    *   Right-click on the project name and select **Build**.
    *   The build generates a `.dacpac` file located in the project's `bin/Debug` folder.
4.  **Deploy/Publish to target Fabric SQL End points**:
    *   Right-click on the project name and select **Publish**.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-f8b08f69-91e2-4311-b597-04f9774252c4.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width="550" height="450" alt="image.png"/>
    *   Select and input all required details for deployment and click on **Publish**.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-017fc3a3-1553-4bec-9fdc-b56e7168f255.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width="400" height="450" alt="image.png"/>

### **2. Setup Empty projects, add scripts and Deploy using VSCode**
#### **Steps**:
1.  **Install SQL Database Projects Extension if not installed already**:
    *   Go to Extensions tab.
    *   Search for "SQL Database Projects" and install it.

![image.png](/.attachments/image-26fa8a7f-9a53-4f8e-998a-e6e253c68a70.png)

2.  **Create empty SQL Project**:
    *   Connect to the branch in repo where project needs to be created.
    *   Create a subfolder where project related files need be store.
    *   Go to the Database projects tab in visual studio code and click "**+**" to create new project and select database project type.
![image.png](/.attachments/image-117a87e1-32d0-42c9-8991-9605c49efb6a.png)
    *   Input project name and select location to previously created folder.

3.  **Adding required Scripts to project**:
    *   For tables, create a folder with same name as schema name and a subfolder with name as "Tables". Right-click on Tables subfolder and select "Add script". provide the name as required table name.
![image.png](/.attachments/image-704f2ac7-ce68-4f06-b35d-7d9e3ab63e47.png)
    *   For Roles, create a folder named as "Security" and inside security folder, create a subfolder named as "Roles". Inside Roles subfolder, right-click and add script for role definition.
    *   For Post-Deployment script and publish profile, right-click on project name and select "Add Post-Deployment script" & "Add Publish Profile".

### **3. Automate Deployment with Azure DevOps Pipelines**

Azure DevOps can automate the `.dacpac` deployment process for continuous integration/continuous deployment (CI/CD).

#### **Steps**

1.  **Set Up Your Repository**:
    *   Push the SQL project folder generated by Azure Data Studio (including `.sqlproj`) to a Azure Repo.
2.  **Build Pipeline**:
    *   Create and use a devops pipeline to build the `.dacpac` from the SQL project.

A sample pipeline can be found on:
[Pipelines - Runs for sample-sql-endpoint-deployment](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_build?definitionId=12)

The yaml pipeline files can be found in the repository:
[samplepipeline - Repos](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration?version=GBmain&path=/.azuredevops/samplepipeline)

And the sample database project is located here:
[SAMPLE_DATABASE - Repos](https://dev.azure.com/Atos-Akela/Fabric%20OneLake/_git/octopus-data-integration?version=GBmain&path=/SQL_ENDPOINT_DATABASES/SAMPLE_DATABASE)

A short description for these artefacts can be found on:
[Sample YAML Pipeline for SQL Deployment](/MS-ODP-\(outdated,-kept-for-reference\)/Development-Guidelines-and-Concepts/Deployment-Pipeline-Guidance/Setup-CICD-Pipeline/Sample-YAML-Pipeline-for-SQL-Deployment)

### **4. Key points for consideration**
1.  **Creating Role**:

-   Create a sub folder named as "Roles" inside "Security" folder.
-   Add a script file named as same with new role name to be created. (example: - CustomDBReader.sql) under "Role" sub folder.
-   Add script "CREATE ROLE [CustomDBReader]; GO" into that file and save.

2.  **Assign Permission To Role**:

- Grant or Deny **Schema** level permission to a role with script like 

```sql
GRANT SELECT ON SCHEMA::dbo TO [CustomDBReader]; GO 
DENY SELECT ON SCHEMA::dbo TO [CustomDBReader]; GO
```
- Grant or Deny **Table** level permission to a role with script like 

```sql
GRANT SELECT ON customer.treasurycustomer TO [CustomDBReader]; GO
DENY SELECT ON customer.treasurycustomer TO [CustomDBReader]; GO
```
- **Please note:** 
- - for assigning roles to a schema or a table, those schema and tables should be present in target sql analytics end point.
- - In database projects create schema and create table definition should be present. 
- - in **.sqlproj** file a code block as below needs to be included to make those only for build not for deploy. to do that, right click on top folder of Database project and select "**Edit .sqlproj file**". 
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-f29abb52-18b4-446f-87d9-80d333409fc5.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width=400 height=300 alt="image.png"/>

The code block example which needs to be included is like
```xml
    <Build Include="Customer\Tables\treasurycustomer.sql">

      <BuildOnly>true</BuildOnly>      <!-- Mark the table script as BuildOnly -->

    </Build>

    <Build Include="Security\Customer.sql">

      <BuildOnly>true</BuildOnly>      <!-- Mark the table script as BuildOnly -->

    </Build>
```
3.  **Assign Users/Groups to Role**:

    -  Create a post deployment script by right click on Project name (top folder) and select "**Add Post-Deployment Script**".
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-097e0274-d68b-4c32-aeec-380f82a5194e.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width=400 height=300 alt="image.png"/>
    -  Include script to assign group/user to role as below".
```sql
ALTER ROLE [CustomDBReader_TreasuryAccount] ADD MEMBER [GIT-ODP-MS-Developer];
GO
```
 -  Make sure below code block is available in **.sqlproj** file".
```xml
  <ItemGroup>

    <PostDeploy Include="PostDeployment.sql" />

  </ItemGroup>
```     

### **5. Create and use Publish Profile**

A **publish profile** (`.publish.xml`) is a configuration file used in SQL Server Data Tools (SSDT) or deployment pipelines to define deployment settings for a database project. It provides a centralized and reusable way to specify how a database project should be deployed to a target environment, reducing the need to manually configure deployment settings each time. 

**Key Uses of a Publish Profile**

1.  **Centralized Deployment Settings**:
    *   Store deployment configurations, such as target database, connection strings, and advanced options.
    *   Avoid repetitive setup for deployments to multiple environments (e.g., dev, test, production).
2.  **Customization**:
    *   Control advanced deployment options like:
        *   **Schema changes**: Whether to block deployments with potential data loss.
        *   **Object behaviors**: Retaining or dropping objects not defined in the project.
        *   **Role members and permissions**: Whether to drop role members not in the source.
    *   Specify pre- and post-deployment scripts.
3.  **Ease of Automation**:
    *   Publish profiles can be directly used with tools like SQLPackage, Visual Studio, or DevOps pipelines.
    *   Automate deployments without redefining settings for each run.
4.  **Environment-Specific Configurations**:
    *   Create separate profiles for different environments (e.g., dev, staging, production) with their specific connection strings and settings.

**Key Settings in a Publish Profile**

A typical `.publish.xml` file contains:
*   **Target Database**:
    *   Specify the database name and connection string.
*   **Behavior Settings**:
    *   Configure settings like:
        *   `BlockOnPossibleDataLoss`: Block deployment if schema changes could result in data loss.
        *   `DropObjectsNotInSource`: Remove objects in the database that are not defined in the source project.
        *   `DropRoleMembersNotInSource`: Drop role members not defined in the source.
*   **Pre- and Post-Deployment Scripts**:
    *   Run additional SQL scripts before or after the deployment.

**Sample Publish Profile**
```xml
<Project>
  <PropertyGroup>
    <!-- Connection settings -->
    <TargetDatabaseName>MyDatabase</TargetDatabaseName>
    <TargetConnectionString>Data Source=myserver.database.windows.net;Initial Catalog=MyDatabase;Integrated Security=False;User ID=myuser;Password=mypassword;</TargetConnectionString>

    <!-- Deployment behavior -->
    <BlockOnPossibleDataLoss>True</BlockOnPossibleDataLoss>
    <DropObjectsNotInSource>True</DropObjectsNotInSource>
    <DropRoleMembersNotInSource>False</DropRoleMembersNotInSource>

    <!-- Execution scripts -->
    <PreDeploymentScript>Scripts\PreDeploy.sql</PreDeploymentScript>
    <PostDeploymentScript>Scripts\PostDeploy.sql</PostDeploymentScript>
  </PropertyGroup>
</Project>
```
**Advantages of Using Publish Profiles**

1.  **Consistency**:
    *   Ensures consistent deployments across environments with predefined settings.
2.  **Time-Saving**:
    *   Simplifies the deployment process by removing repetitive configuration steps.
3.  **Error Reduction**:
    *   Minimizes manual errors by encapsulating deployment settings in a file.
4.  **Version Control**:
    *   Since publish profiles are files, they can be versioned in a source control system.

**How to create & Use a Publish Profile**
- In Azure Data Studio, Right-click on project name and select publish.
<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-3bd8477b-0e11-4465-92f9-8c0300298c4b.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" width=400 height=250 alt="image.png"/>

- Connect to the target sql endpoint and select Save As with proper publish profile name.

<IMG  src="https://dev.azure.com/Atos-Akela/b7ffe9ce-c845-418d-8d1f-df38c27f2fd8/_apis/git/repositories/0eec338f-9cf2-4a36-b86f-e78cdb352b69/Items?path=/.attachments/image-689b20e9-f508-4d08-919b-8587a594c324.png&amp;download=false&amp;resolveLfs=true&amp;%24format=octetStream&amp;api-version=5.0-preview.1&amp;sanitize=true&amp;versionDescriptor.version=wikiMaster" Width=400 height=300  alt="image.png"/>

- Use the created publish profile for future deployments.

### **6. Reference Implementation**